- $e^x 的导数是e^x$
	- $\lim_{\Delta x\to 0} \frac{f(x+\Delta x) - f(x)}{\Delta x}$
		$= \lim_{\Delta x\to 0} \frac{e^{x+\Delta x}- e^x}{\Delta x}$
		$= e^x \lim_{\Delta x\to 0 } \frac{e^\Delta x -1}{\Delta x}$
		$= e^x \lim_{u \to 0}\frac{u}{ln(u+1)}\begin{cases}
		u = e^{\Delta x} -1, \Delta x \to 0\\ \Delta x = ln(u+1), u \to 0
		\end{cases}$
		$=  e^x \lim_{u \to 0} \frac{1}{\frac{1}{u}ln(u+1)}$
		$= e^x \lim_{u \to 0}\frac{1}{ln(u+1)^\frac{1}{u}}$
		$\because$ 根据两个重要极限之一 $\lim_{x \to \infty}(1+\frac{1}{x})^x = e$
		$\therefore =e^x\frac{1}{lne}$
		$= e^x$

