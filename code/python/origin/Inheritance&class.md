- ### class

  ```python
  class Fraction:
  
      def __init__(self, top, bottom):
  
          self.num = top
          self.den = bottom
  
      # 定义一个默认的显示类的方法
      def __str__(self):
          return str(self.num)+"/"+str(self.den)
  
      def __add__(self, otherfraction):
          newnum = self.num * otherfraction.den + self.den * otherfraction.num
          newden = self.den * otherfraction.den
          common = gcd(newnum, newden)
          return Fraction(newnum / common, newden / common)
  
      def __eq__(self, otherfraction):
          return self.num * otherfraction.den == otherfraction.num * self.den
  
      def __mul__(self, otherfraction):
          newNum = self.num * otherfraction.num
          newDen = self.den * otherfraction.den
          return Fraction(newNum, newDen)
  
      def __truediv__(self, otherfraction):
          newNum = self.num * otherfraction.den
          newDen = self.den * otherfraction.num
          common = gcd(newNum, newDen)
          return Fraction(newNum / common, newDen / common)
  
      def __radd__(self, otherfraction):
          return self + otherfraction
  
      def __iadd__(self, other):
          self = self + other
          return self
  
  
  def gcd(m, n):
      if n == 0:
          return m
      r = m % n
      return(gcd(n, r))
  
  
  # myf = Fraction(3, 5)
  # print(myf)
  # print("I ate", myf, "of the pizza")
  # print(myf.__str__())
  # print(str(myf))
  # myf = Fraction(1, 4) + Fraction(1, 2)
  # print(myf)
  print(Fraction(1, 3) .__radd__(Fraction(1, 3)))
  
  ```

  

- inheritance

	```python
	class LogicGate:
	
	    def __init__(self, n):
	        self.label = n
	        self.output = None
	
	    def getLabel(self):
	        return self.label
	
	    def getOutput(self):
	        self.output = self.performGateLogic()
	        return self.output
	
	    def performGateLogic(self):
	        return 0
	
	
	class BinaryGate(LogicGate):
	
	    def __init__(self, n):
	
	        LogicGate.__init__(self, n)
	
	        self.pinA = None
	        self.pinB = None
	
	    def getPinA(self):
	        if self.pinA is None:
	            return int(input("Enter Pin A input for gate " +
	                             self.getLabel()+"-->"))
	        else:
	            return self.pinA.getFrom().getOutput()
	
	    def getPinB(self):
	        if self.pinB is None:
	            return int(input("Enter Pin B input for gate " +
	                             self.getLabel()+"-->"))
	        else:
	            return self.pinB.getFrom().getOutput()
	
	    def setNextPin(self, source):
	        if self.pinA is None:
	            self.pinA = source
	        else:
	            if self.pinB is None:
	                self.pinB = source
	            else:
	                raise RuntimeError("Error: NO EMPTY PINS")
	
	
	class UnaryGate(LogicGate):
	
	    def __init__(self, n):
	
	        LogicGate.__init__(self, n)
	
	        self.pin = None
	
	    def getPin(self):
	        if self.pin is None:
	            return int(input("Enter Pin input for gate " +
	                             self.getLabel()+"-->"))
	        else:
	            return self.pin.getFrom().getOutput()
	
	    def setNextPin(self, source):
	        if self.pin is None:
	            self.pin = source
	        else:
	            print("Cannot Connect: NO EMPTY PINS on this gate")
	
	
	class AndGate(BinaryGate):
	    def __init__(self, n):
	        BinaryGate.__init__(self, n)
	
	    def performGateLogic(self):
	
	        a = self.getPinA()
	        b = self.getPinB()
	        if a == 1 and b == 1:
	            return 1
	        else:
	            return 0
	
	
	class OrGate(BinaryGate):
	
	    def __init__(self, n):
	        BinaryGate.__init__(self, n)
	
	    def performGateLogic(self):
	
	        a = self.getPinA()
	        b = self.getPinB()
	        if a == 1 or b == 1:
	            return 1
	        else:
	            return 0
	
	
	class NotGate(UnaryGate):
	
	    def __init__(self, n):
	        UnaryGate.__init__(self, n)
	
	    def performGateLogic(self):
	
	        if self.getPin():
	            return 0
	        else:
	            return 1
	
	
	class Connector:
	
	    def __init__(self, fgate, tgate):
	        self.fromgate = fgate
	        self.togate = tgate
	
	        tgate.setNextPin(self)
	
	    def getFrom(self):
	        return self.fromgate
	
	    def getTo(self):
	        return self.togate
	
	
	def main():
	    g1 = AndGate("G1")
	    # print(g1.getOutput())
	    # exit()
	    g2 = AndGate("G2")
	    g3 = OrGate("G3")
	    g4 = NotGate("G4")
	    Connector(g1, g3)
	    Connector(g2, g3)
	    Connector(g3, g4)
	    print(g4.getOutput())
	
	
	main()
	
	```

	