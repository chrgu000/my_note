- ### amazon 退款详细
    - ##### http://172.18.8.242/amazon-refund 
    - ##### get
    - ##### 参数
        1. page
        2. pageSize
        3. site
        4. account_id  账号id
        5. seller_id 销售id
        6. date_b  开始时间 （ 2012-2-2）
        7. date_e  结束时间
    - data
        ```
        {
            "data": [
                {
                    "order_number": "171-0079064-7925139",   -- 订单号
                    "account_code": "puerifr",      -- 账号简称
                    "site": "FR",           -- 站点
                    "seller": "陈丽珍",             --销售
                    "currency_code": "EUR",         -- 币种
                    "rate": "7.683600",             -- 汇率
                    "refund": "0.00",               -- 退款
                    "refund_cny": "0.00",           -- 退款人民币
                    "refund_date": "2019-03-06"     -- 退款日期
                }
            ],
            "page": 1,
            "pageSize": "1",
            "count": 356
        }
        ```
- ### amazon fba退款详情
    - ##### http://172.18.8.242/amazon-refund/fba
    - ##### get
    - ##### 参数
        1. page
        2. pageSize
        3. site
        4. account_id  账号id
        5. seller_id 销售id
        6. date_b  开始时间 （ 2012-2-2）
        7. date_e  结束时间
    - data
        ```
        {
            "data": [
                {
                    "order_number": "171-0079064-7925139",
                    "account_code": "puerifr",
                    "site": "FR",
                    "seller": "陈丽珍",
                    "currency_code": "EUR",
                    "rate": "7.683600",
                    "refund": "0.00",
                    "refund_cny": "0.00",
                    "refund_date": "2019-03-06"
                }
            ],
            "page": 1,
            "pageSize": "1",
            "count": 127
        }
        ```
- ### 导出
    - #####  http://172.18.8.242/amazon-refund/export
    - ##### post
    - 参数 
        1. 搜索参数 
        2. shipping_type  1 自发货 2 fba
    - data
        ```
        {"message":"申请成功","join_queue":1}
        (2018-12-1) : Amazon 未抓取订单的账号数量 4265。

        ```