```mysql



SELECT
	'SMT(速卖通 ）' as '平台',
	a.CODE AS '账号简称',
	'' as '站点',
-- 	a.id AS '账号ID',
	a.account_name AS '账号全称',
	c.shop_name as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.is_invalid = 1,'有效','无效') as '账号状态',
	'' as '收款方式',
	'' as '开户名',
	'' as '账号'
FROM
	aliexpress_account AS a
	LEFT JOIN (
	SELECT
		a.account_id,
		b.realname 
	FROM
		channel_user_account_map AS a
		LEFT JOIN `user` AS b ON a.seller_id = b.id 
		AND a.channel_id = 4 
	WHERE
		a.channel_id = 4 
	) AS b ON a.id = b.account_id
	LEFT JOIN account c on c.account_code = a.`code`
-- 	where c.channel_id = 4
-- WHERE
--   a.`code` = 'MTJQP';


-- -------------------------------------------------------------------------------------



SELECT
	'亚马逊' as '平台',
	a.CODE AS '账号简称',
	a.site as '站点',
-- 	a.id AS '账号ID',
	a.account_name AS '账号全称',
	c.shop_name as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`status` = 1,'有效','无效') as '账号状态',
	'' as '收款方式',
	'' as '开户名',
	'' as '账号'
FROM
	amazon_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 2 
	WHERE
		d.channel_id = 2 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.id = a.`base_account_id`


-- ---------------------------------------------------

SELECT
	'wish' as '平台',
	a.CODE AS '账号简称',
	'' as '站点',
-- 	a.id AS '账号ID',
	a.account_name AS '账号全称',
	a.shop_name as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`is_invalid` = 1,'有效','无效') as '账号状态',
	'' as '收款方式',
	'' as '开户名',
	'' as '账号'
FROM
	wish_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 3 
	WHERE
		d.channel_id = 3 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_code = a.`code`
	
	
	
	-- --------------------------------------------------
	
	SELECT
	'shopee' as '平台',
	a.`code` AS '账号简称',
	a.site as '站点',
-- 	a.id AS '账号ID',
	a.`name` AS '账号全称',
	a.shop_id as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`platform_status` = 1,'有效','无效') as '账号状态',
	'' as '收款方式',
	'' as '开户名',
	'' as '账号'
FROM
	shopee_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 9 
	WHERE
		d.channel_id = 9 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_code = a.`code`
	
	
	-- ---------------------------------------------------
	
	
		SELECT
	'lazada' as '平台',
	a.`code` AS '账号简称',
	a.site as '站点',
-- 	a.id AS '账号ID',
	a.`name` AS '账号全称',
	' ' as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`status` = 1,'有效','无效') as '账号状态',
	' ' as '收款方式',
	' ' as '开户名',
	' ' as '账号'
FROM
	lazada_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 6 
	WHERE
		d.channel_id = 6 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_name = a.`name`
	
	
	
	
	--  -----------------------------------------------------------------
	
	
		SELECT
	'mymall' as '平台',
	a.`code` AS '账号简称',
	'' as '站点',
-- 	a.id AS '账号ID',
	a.`account_name` AS '账号全称',
	' ' as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`is_invalid` = 1,'有效','无效') as '账号状态',
	' ' as '收款方式',
	' ' as '开户名',
	' ' as '账号'
FROM
	pandao_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 8 
	WHERE
		d.channel_id = 8 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_code = a.`code`
	
	
	--  -----------------------------------------------------------------
		
		
		SELECT
	'jumia' as '平台',
	a.`code` AS '账号简称',
	'' as '站点',
-- 	a.id AS '账号ID',
	a.`account_name` AS '账号全称',
	' ' as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`is_invalid` = 1,'有效','无效') as '账号状态',
	' ' as '收款方式',
	' ' as '开户名',
	' ' as '账号'
FROM
	jumia_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 13 
	WHERE
		d.channel_id = 13 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_code = a.`code`


-- -------------------------------------------------------------------------
		SELECT
	'funmart' as '平台',
	a.`code` AS '账号简称',
	'' as '站点',
-- 	a.id AS '账号ID',
	a.`account_name` AS '账号全称',
	' ' as '店铺名称',
	c.email as '邮箱',
	b.realname AS '销售人员',
	IF(a.`is_invalid` = 1,'有效','无效') as '账号状态',
	' ' as '收款方式',
	' ' as '开户名',
	' ' as '账号'
FROM
	fummart_account AS a
	LEFT JOIN (
	SELECT
		d.account_id,
		b.realname 
	FROM
		channel_user_account_map AS d
		LEFT JOIN `user` AS b ON d.seller_id = b.id 
		AND d.channel_id = 22 
	WHERE
		d.channel_id = 22 
	) AS b ON a.id = b.account_id
	left JOIN account c on c.account_code = a.`code`


```

---

有订单的
```mysql

#声明变量
SET @channel_name='aliexpress';
SET @channel_id=4;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  '' as '站点',
  a.account_name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  aliexpress_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    aliexpress_online_order
  WHERE
    gmt_pay_time > @time_start
    AND gmt_pay_time < @time_end
    GROUP BY
    account_id

);

-- ---------------------------------------------------------------------------------------------




#声明变量
SET @channel_name='wish';
SET @channel_id=3;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  '' as '站点',
  a.account_name as '账号全称',
  a.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  wish_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    wish_platform_online_order
  WHERE
    pay_time > @time_start
    AND pay_time < @time_end
    GROUP BY
    account_id

);


-- ---------------------------------------------------------------------------------------




#声明变量
SET @channel_name='amazon';
SET @channel_id=2;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  a.site as '站点',
  a.account_name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  amazon_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    amazon_order
  WHERE
    payment_time > @time_start
    AND payment_time < @time_end
    GROUP BY
    account_id

);

-- ------------------------------------------------------



#声明变量
SET @channel_name='shopee';
SET @channel_id=9;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  a.site as '站点',
  a.name as '账号全称',
  a.shop_id as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  shopee_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    shopee_order
  WHERE
    create_time > @time_start
    AND create_time < @time_end
    GROUP BY
    account_id

);

-- ---------------------------------------------------------

#声明变量
SET @channel_name='lazada';
SET @channel_id=6;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  a.site as '站点',
  a.name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  lazada_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    lazada_order
  WHERE
    created_at > @time_start
    AND created_at < @time_end
    GROUP BY
    account_id

);

--  ----------------------------------------------------------------



#声明变量
SET @channel_name='mymall';
SET @channel_id=8;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  '' as '站点',
  a.account_name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  pandao_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    pandao_order
  WHERE
    order_time > @time_start
    AND order_time < @time_end
    GROUP BY
    account_id

);

-- -------------------------------------------------------------------------------


#声明变量
SET @channel_name='funmart';
SET @channel_id=22;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  '' as '站点',
  a.account_name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  fummart_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    funmart_order
  WHERE
    t_paytime > @time_start
    AND t_paytime < @time_end
    GROUP BY
    account_id

);

-- ---------------------------------------------------------------------------


#声明变量
SET @channel_name='vova';
SET @channel_id=12;
SET @time_start=1552233600;
SET @time_end=1554912000;


SELECT
  @channel_name AS '平台',
  a.`code` AS '简称',
--   REPLACE(REPLACE(REPLACE(a.site_id,'"',''),'[',''),']','') as '站点',
  '' as '站点',
  a.account_name as '账号全称',
  b.shop_name as '店铺名称',
  b.email as '邮箱',
  c.realname AS '销售人员'
FROM
  vova_account AS a
LEFT JOIN account AS b on a.base_account_id=b.id
LEFT JOIN (
  SELECT
    a.account_id,
    b.realname
  FROM
    channel_user_account_map AS a
  LEFT JOIN `user` AS b ON a.seller_id = b.id
  AND a.channel_id = @channel_id
  WHERE
    a.channel_id = @channel_id
  ) as c on c.account_id=a.id
WHERE 
  a.id in (
  SELECT
    account_id
	
	FROM
    vova_order
  WHERE
    confirm_time > @time_start
    AND confirm_time < @time_end
    GROUP BY
    account_id

);
```