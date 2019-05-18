```mysql
select 
a.account_id,
group_concat(a.id)
from amazon_settlement_report as a 
LEFT JOIN amazon_settlement_report_summary as b on a.id=b.amazon_settlement_report_id
where 
1=1
and settlement_start_time>1551369600
and settlement_start_time<1554957645
GROUP BY a.account_id

SELECT CONVERT(JSON_EXTRACT(org_data ,'$.quantity_purchased'),UNSIGNED INTEGER) FROM amazon_settlement_report_detail WHERE amazon_transaction_type_id in (2103,2203,2124,2287) and JSON_EXTRACT(org_data ,'$.quantity_purchased') >0


UPDATE amazon_settlement_report r
RIGHT JOIN amazon_get_report g ON ( g.generated_report_id = r.report_id ) 
AND g.report_type = '_GET_V2_SETTLEMENT_REPORT_DATA_FLAT_FILE_V2_' 
SET r.report_type = 2;

UPDATE amazon_settlement_report r
RIGHT JOIN amazon_get_report g ON ( g.generated_report_id = r.report_id ) 
AND g.report_type = '_GET_V2_SETTLEMENT_REPORT_DATA_FLAT_FILE_' 
SET r.report_type = 1;

UPDATE amazon_settlement_report_detail d 
SET d.posted_date = unix_timestamp(
	substring_index(
		REPLACE ( REPLACE ( CONVERT ( JSON_EXTRACT( d.org_data, '$.posted_date' ), CHAR ), '"', '' ), 'T', ' ' ),
		'+',
		1 
	) 
);


```

