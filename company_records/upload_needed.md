~~lazada 海外仓导出~~

~~ALTER TABLE `erp-admin`.`lazada_order`~~ 

~~ADD COLUMN `involve_oversea` tinyint(1) NOT NULL DEFAULT 0 COMMENT '是否包含海外仓订单（0默认,1，部分海外仓，2全部海外仓，3，全部本地仓）' AFTER `address_updated_at`;~~

~~trunk/application/order/controller/Lazada.php~~

~~trunk/application/order/service/LazadaService.php~~

~~trunk/application/order/queue/LazadaOverSeaExportQueue.php~~


~~<http://erp.com/guanyi/test?test&action=fixLazadaInvolveOversea&page=4&pageSize=10000>~~


~~获取amazon结算内容~~

~~trunk/application/order/service/AmazonSettlementReportSummary.php~~


~~trunk/application/common/model/amazon/AmazonSettlementReportSummaryDetail.php~~
~~trunk/application/order/service/OrderService.php~~

~~trunk/application/common/cache/driver/AmazonReport.php~~

~~trunk/application/order/service/AmazonReportCallback.php~~



~~ALTER TABLE `erp-admin`.`amazon_settlement_report`~~ 

~~MODIFY COLUMN `wait_summary` tinyint(1) NOT NULL DEFAULT 0 COMMENT '待汇总,0:否,1:是' AFTER `type`;~~



~~ALTER TABLE `erp-admin`.`amazon_settlement_report_summary`~~ 

~~ADD COLUMN `fba_inventory_amount` decimal(12, 4) NOT NULL DEFAULT 0.0000 COMMENT 'FBA Inventory Reimbursement(调整费用)' AFTER `reserve_amount`,~~

~~ADD COLUMN `shop_fee` decimal(12, 4) NOT NULL DEFAULT 0.0000 COMMENT '店铺费用' AFTER `fba_inventory_amount`,~~

~~ADD COLUMN `advertising_fee` decimal(12, 4) NOT NULL DEFAULT 0.0000 COMMENT '广告费用' AFTER `shop_fee`;~~


~~trunk/application/index/service/DepartmentUserMapService.php~~

~~ALTER TABLE `erp-admin`.`amazon_settlement_report`~~ 

~~ADD COLUMN `report_type` tinyint(1) NOT NULL DEFAULT 0 COMMENT '报告版本，（0：默认，1：v1, 2：v2）' AFTER `wait_summary`;~~

~~ALTER TABLE `erp-admin`.`amazon_settlement_report_detail`~~ 

~~ADD COLUMN `posted_date` int(10) UNSIGNED NOT NULL DEFAULT 0 COMMENT '交易时间' AFTER `amount_usd`;~~


~~ALTER TABLE `erp-admin`.`amazon_settlement_report_detail`~~ 

~~DROP INDEX `idx_amazon_transaction_type_id`,~~

~~ADD INDEX `idx_amazon_posted_date`(`posted_date`) USING BTREE,~~

~~ADD INDEX `idx_amazon_order_number`(`order_number`) USING BTREE;~~



jumia订单分站点

ALTER TABLE `erp-admin`.`jumia_order` 

ADD COLUMN `site` varchar(10) NOT NULL DEFAULT '' COMMENT '站点' AFTER `order_id`,

CHARACTER SET = utf8mb4, COLLATE = utf8mb4_general_ci;

ALTER TABLE `erp-admin`.`jumia_order_detail` CHARACTER SET = utf8mb4, COLLATE = utf8mb4_general_ci;



trunk/application/order/service/JumiaOrderService.php

trunk/extend/jumia/JumiaOrderApi.php

trunk/application/order/task/JumiaToLocalOrder.php

trunk/extend/jumia/JumiaBaseApi.php



wish

ALTER TABLE `erp-admin`.`wish_ticket_reply` 

MODIFY COLUMN `message` text CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL COMMENT '回复消息' AFTER `date`,

MODIFY COLUMN `image_urls` varchar(1000) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL DEFAULT '' COMMENT '图片地址' AFTER `sender`;



ALTER TABLE `erp-admin`.`wish_ticket` 

ADD COLUMN `seller_id` smallint(5) NOT NULL DEFAULT 0 COMMENT '销售id' AFTER `ticket_id`;





trunk/extend/service/wish/operation/Ticket.php

trunk/extend/service/wish/operation/Common.php

trunk/application/customerservice/task/WishTicket.php

trunk/application/customerservice/task/WishOneTicket.php

trunk/application/customerservice/queue/WishTicketQueue.php

trunk/application/customerservice/queue/WishOneTicketQueue.php

trunk/application/common/model/wish/WishTicket.php

trunk/application/common/model/wish/WishTicketInfo.php

trunk/application/common/model/wish/WishTicketReply.php

trunk/application/common/model/wish/WishTicketReplyLevel.php

trunk/application/common/cache/driver/WishTicket.php

trunk/application/customerservice/controller/WishTicket.php

trunk/application/customerservice/service/WishTictetService.php

trunk/application/extra/controller.php

trunk/application/customerservice/service/MsgTemplateHelp.php





~~/application/order/service/AmazonSettlementReportSummary.php~~

~~/application/order/service/AmazonReportCallbackVtwo.php~~

~~/application/order/service/AmazonReportCallback.php~~

~~/application/order/service/AmazonSettlementReport.php~~



~~wish二次同步发货~~

~~trunk/application/order/service/SynchronizeService.php~~

~~trunk/application/common/cache/driver/Synchronous.php~~

~~trunk/application/order/queue/WishSynchronousSecQueue.php~~

~~trunk/extend/service/wish/operation/Order.php~~

~~trunk/application/order/interfaces/WishSynchronous.php~~



~~退款明细~~

~~application/extra/controller.php~~
~~application/report/controller/AmazonRefundDetail.php~~
~~application/report/service/AmazonRefundDetailService.php~~
~~application/order/service/AmazonSettlementReport.php~~
~~application/order/service/AmazonSettlementReportSummary.php~~
~~application/report/queue/AmazonRefundDetailExportQueue.php~~



**~~增加查询条件：买家选择物流，下拉列表，单选，下拉列表选项显示买家下单时选择的物流。（后）**~~
~~trunk/application/order/controller/Aliexpress.php~~
~~trunk/application/order/service/AliOrderServer.php~~





~~wish检测未抓单账号，要重启swoole~~ 
~~application/order/task/CheckOrderGrabTime.php~~
~~application/order/task/WishDownload.php~~
~~application/order/service/WishService.php~~
~~application/common/cache/driver/WishAccount.php~~



~~shopee**查看详情框，提供维护平台sku的功能**~~

~~trunk/application/order/controller/Shopee.php~~

~~trunk/application/order/task/ShopeeToLocal.php~~

~~trunk/application/order/service/ShopeeService.php~~





amazon根据时间自动回复

ALTER TABLE `erp-admin`.`msg_rule_set` 
ADD COLUMN `rule_start` int(10) NOT NULL DEFAULT 0 COMMENT '规则开始时间' AFTER `delay_time_send`,
ADD COLUMN `rule_end` int(10) NOT NULL DEFAULT 0 COMMENT '规则结束时间' AFTER `rule_start`;



trunk/application/customerservice/service/MsgRuleHelp.php

trunk/application/common/model/MsgRuleSet.php

trunk/application/customerservice/service/AmazonEmail.php

trunk/application/customerservice/controller/MsgRule.php

模板权限设置

trunk/application/common/cache/driver/MsgTemplate.php

trunk/application/customerservice/service/MsgTemplateHelp.php

trunk/application/customerservice/controller/MsgTemplate.php