- ### 收件箱
    - #### http://172.18.8.242/wish-ticket?test 
    - #### get
    - #### 参数
        1. account_id
        2. status erp处理状态(0 待处理，2 等待用户回应， 3 已关闭, 4： 48小时)
        3. seller_id 销售id
        4. buyer 客户 string
        5. order_id 订单号 string
        6. ticket_id 站内信编号
        7. reply_level 回复级别 1， 2，3
        8. page 
        9. pageSize
    - #### data
        ```
        {
            "data": [
                {
                    "order": [
                        {
                            "order_id": "5cb4cf794aa2126f5c32a4cd",    --订单号
                            "country": "NL",                           -- 国家
                            "price": "15.0",                           -- 价格
                            "state": "SHIPPED",                        -- 状态
                            "order_time": "2019-04-15 10:37:45",       -- 下单时间
                            "shipped_date": "2019-04-16",              -- 发货时间
                            "tracking_number": "US478717302CN",        -- 追踪号
                            "shipping_provider": "WishPost",           -- 物流提供商
                            "sku": "DB0055902|1695522423",             -- sku
                            "quantity": "1"                            -- 数量
                        }
                    ],
                    "buyer": "F Kilic",         --客户
                    "subject": "Hoe werkt mijn product?",   --主题
                    "account_code": "261wishsen",       --店铺
                    "open_date": "2019-05-08 08:14:33",         --开启日期
                    "order_id": "5cb4cf794aa2126f5c32a4cd",         --订单号
                    "label": "How Does my Product Work?",           --标签
                    "ticket_id": "5cd338a92f975148a2fe79a4",        --站内信编号
                    "reply_level": 2,                               --回复级别
                    "free_time": "23小时13分",                      --剩余时间
                    "reply": [
                        {
                            "sender": "wish support",               --发送人
                            "message": "Een transcript van de chat tussen F Kilic en Wish assistent:\n\n(F Kilic)\n&gt;&gt;&gt; https://contestimg.wish.com/api/webimage/5aeaadf68a743b51d4a5b7df-2-medium?cozy=1\n\n(Wish assistent)\n&gt;&gt;&gt; Hallo F, ik ben de support-assistent van Wish!\n&gt;&gt;&gt; Hier is de meest recente tracking-info die ik heb:\n&gt;&gt;&gt; Komt aan op 24 mei 2019\n&gt;&gt;&gt; Heb je dit item al ontvangen?\n\n(F Kilic)\n&gt;&gt;&gt; Ja\n\n(Wish assistent)\n&gt;&gt;&gt; Is er een probleem met je bestelling?\n\n(F Kilic)\n&gt;&gt;&gt; Hoe werkt mijn item precies?\n\n(Wish assistent)\n&gt;&gt;&gt; Het spijt ons dat het onduidelijk is hoe je item werkt! Wij willen dit voor je rechtzetten.\n&gt;&gt;&gt; Neem contact op met een helpdesk-medewerker van Wish want we hebben meer informatie nodig over dit probleem. Wil je contact opnemen met een helpdesk-medewerker?\n\n(F Kilic)\n&gt;&gt;&gt; neem contact op met de helpdeskvertegenwoordiger\n\n(Wish assistent)\n&gt;&gt;&gt; Geef een gedetailleerde beschrijving van het probleem, zodat we je het beste kunnen helpen.\n&gt;&gt;&gt; Zorg ervoor dat je geen gevoelige informatie zoals creditcard- en persoonlijke identificatienummers in je bericht opneemt.\n",
                            "date": "2019-05-08 08:14:33",       --发送时间
                            "image_urls": "[]"                  --图片地址
                        },
                        {
                            "sender": "user",
                            "message": "hoi kan ik deze gebruiken zonder SD card? Heeft u een geschikte SD card bij dezelfde leverancier?",
                            "date": "2019-05-08 08:14:34",
                            "image_urls": "[]"
                        },
                        {
                            "sender": "wish support",
                            "message": "Hallo F,\n\nBedankt voor je bericht. Ik begrijp dat je niet helemaal weet hoe jouw product precies werkt.\n\nIk heb daarom voor jou een bericht gestuurd naar de verkoper om te vragen voor meer informatie. De verkoper zou binnen de 48 uur moeten antwoorden.\n\nMocht je nog vragen hebben, aarzel dan niet om ons te contacteren. Bedankt voor het shoppen bij Wish, en ik wens je nog een prettige dag verder!\n\nJohannes\nWish Team",
                            "date": "2019-05-09 10:35:12",
                            "image_urls": "[]"
                        },
                        {
                            "sender": "wish support",
                            "message": "Hello Merchant,\n\nOur customer has a question about how to use their product.\n\nCould you please provide us with a .PNG / .JPEG / .GIF of instructions on how to use the product or a product manual?\n\nAlso, the customer wants to know if he can use this item without sd card. Can you provide us with more information about this?\n\nJohannes\nWish Customer Support",
                            "date": "2019-05-09 10:35:12",
                            "image_urls": "[]"
                        }
                    ]
                }
            ],
            "page": "1",
            "pageSize": "1",
            "count": 16
        }
        ```

- ### 发件箱 
    - ##### http://172.18.8.242/wish-ticket/outbox?test&page=1&pageSize=1
    - ##### get
    - ##### 参数
        1. send_state 0：默认，-1: 发送失败， 1：接收消息，
        2. seller_id 　　销售id
        3. buyer   　　　买家
        4. order_id 　　订单id
        5. page
        6. pageSize
    - ##### data
        ```
        {
            "data": [
                {
                    "buyer": "F Kilic",                     -- 买家
                    "id": 82,                               -- id
                    "ticket_id": "5cd338a92f975148a2fe79a4",        --ticket 编号
                    "account_code": "261wishsen",               --店铺名
                    "subject": "Hoe werkt mijn product?",       -- 主题
                    "date": "2019-05-08 08:14:33",              -- 发送日期
                    "message": "Een transcript van de chat tussen F Kilic en Wish assistent:\n\n(F Kilic)\n&gt;&gt;&gt; https://contestimg.wish.com/api/webimage/5aeaadf68a743b51d4a5b7df-2-medium?cozy=1\n\n(Wish assistent)\n&gt;&gt;&gt; Hallo F, ik ben de support-assistent van Wish!\n&gt;&gt;&gt; Hier is de meest recente tracking-info die ik heb:\n&gt;&gt;&gt; Komt aan op 24 mei 2019\n&gt;&gt;&gt; Heb je dit item al ontvangen?\n\n(F Kilic)\n&gt;&gt;&gt; Ja\n\n(Wish assistent)\n&gt;&gt;&gt; Is er een probleem met je bestelling?\n\n(F Kilic)\n&gt;&gt;&gt; Hoe werkt mijn item precies?\n\n(Wish assistent)\n&gt;&gt;&gt; Het spijt ons dat het onduidelijk is hoe je item werkt! Wij willen dit voor je rechtzetten.\n&gt;&gt;&gt; Neem contact op met een helpdesk-medewerker van Wish want we hebben meer informatie nodig over dit probleem. Wil je contact opnemen met een helpdesk-medewerker?\n\n(F Kilic)\n&gt;&gt;&gt; neem contact op met de helpdeskvertegenwoordiger\n\n(Wish assistent)\n&gt;&gt;&gt; Geef een gedetailleerde beschrijving van het probleem, zodat we je het beste kunnen helpen.\n&gt;&gt;&gt; Zorg ervoor dat je geen gevoelige informatie zoals creditcard- en persoonlijke identificatienummers in je bericht opneemt.\n",
                    "order_id": "5cb4cf794aa2126f5c32a4cd",     -- 订单号
                    "country": "NL",                            -- 国家
                    "price": "15.0",                            -- 价格
                    "state": "SHIPPED"                          --订单状态
                    "send_state": 1                             -- 发送状态0：默认，-1: 发送失败， 1：接收消息，
                }
            ],
            "page": "1",
            "pageSize": "1",
            "count": 2
        }
        ```

- ### 回复消息
    - ##### http://172.18.8.242/wish-ticket/reply
    - ##### post
    - ##### 参数
        1. ticket_id  站内信编号
        2. message 回复消息
        3. account_id 账号id
    - ##### {message: success}

- ### 重新发送失败消息
    - ##### http://172.18.8.242/wish-ticket/resend
    - ##### post
    - ##### 参数
        1. ticket_id  站内信编号
        2. message 回复消息
        3. account_id 账号id
    - ##### {message: success}

- ### 删除回复失败的消息
    - ##### http://172.18.8.242/wish-ticket/delete-failure
    - ##### put
    - ##### 参数
        1. id  消息id
    - ##### {message : 删除成功}

- ### 关闭ticket
    - ##### http://172.18.8.242/wish-ticket/close
    - ##### post
    - ##### 参数
        1. ticket_id
        2. account_id
    - ##### {message: success}
- ### 申请wish support
    - ##### http://172.18.8.242/wish-ticket/appeal
    - ##### post
    - ##### 参数
        1. ticket_id
        2. account_id
    - ##### {message: success}

- ### 设置ticket level
    - ##### http://172.18.8.242/wish-ticket/set-reply-level
    - ##### post
    - ##### 参数
        1. reply_level 回复级别
        2. max_time 时间 （小时）
    - ##### {修改成功}