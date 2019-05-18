# 平台记录
- #### 是否有最迟发货时间

    - aliexpress 平台支持 推送有
    
        ```
        // $time = left_send_good_day * 86400 + left_send_good_hour * 3600 + left_send_good_min * 60 
        //send_good_expire = time() + $time;
        $data['uploaded_deadline'] = $v['send_good_expire'];  //send_good_expire s
        
        ```
    
    - amazon 平台支持 推送已改成付款时间后48小时
    
    - wish 平台支持 现推送
    
        ```
        if (!empty($order['hours_to_fulfill'])) {
            $data['uploaded_deadline'] = $order['pay_time'] + $order['hours_to_fulfill'] * 60 * 60;
        } else {
            $data['uploaded_deadline'] = $order['available_for_fulfillment_time'] + 5 * 24 * 60 * 60;
        }        
        ```
        
    - Shopee 平台支持 现推送
    
        ```
        $data['uploaded_deadline'] = $v['create_time']+($v['days_to_ship']+5)*86400;  // days_to_ship 后推5天
        ```
        
    - lazada 接口有字段 promised_shipping_times 但是是空字段，没有值。现推送无最晚发货时间
    
    - MyMall 接口有字段 latest_shipped_time 现推送 
    
        ```
        $data['uploaded_deadline'] = $order_data['order_time'] + 10 * 86400;  //10天
        ```
        
    - jumia 接口字段 PromisedShippingTime 现推送
    
        ```
         $data['uploaded_deadline'] = $order['PromisedShippingTime'] + 28800;
        ```
        
    - funmart 接口不支持 只有付款时间 ，现推送无最晚发货时间， 未上线。
- #### amazon资金核算
    - 部分数据订单号为特殊的 ，排除掉了，设置发货类型为0
        ```
        select * from amazon_settlement_report_detail where id=15040735;
        "order_id": "6aabed65-9a88-4332-a071-1072990bb6be",
        ```
- #### jumia账号
    ```
    sellercenter.jumia.ci
    hgisa56@outlook.com
    
    ehud8374WYE
    
    
    sellercenter.jumia.co.ke
    hgisa56@outlook.com
    
    dhc893WYE2
    
    
    sellercenter.jumia.com.eg
    hgisa56@outlook.com
    
    MEIH8374whe
    
    
    //尼日利亚
    sellercenter.jumia.com.ng
    hgisa56@outlook.com
    
    WEI9488hwy
    
    
    sellercenter.jumia.ma
    hgisa56@outlook.com
    
    DHV8374aws
    ```
    - 公司远程
        ```
        远程服务器名  远程账号  远程密码
        kasiqi  kasiqi-jumia  La100200
        ```



 