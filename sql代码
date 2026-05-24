-- =============================================
-- 电商美妆区域销售分析 - 所有SQL脚本
-- =============================================

-- 1. 各省份护肤品销量排行
SELECT 
    s.所在省份,
    SUM(s.订购数量) AS 总销量
FROM sales_orders s
JOIN products p ON s.商品编号 = p.商品编号
WHERE p.商品大类 = '护肤品'
GROUP BY s.所在省份
ORDER BY 总销量 DESC;

-- 2. 各省份彩妆销量排行
SELECT 
    s.所在省份,
    SUM(s.订购数量) AS 总销量
FROM sales_orders s
JOIN products p ON s.商品编号 = p.商品编号
WHERE p.商品大类 = '彩妆'
GROUP BY s.所在省份
ORDER BY 总销量 DESC;

-- 3. 窗口函数：各省份内城市护肤品销量排名（核心）
SELECT 
    s.所在省份,
    s.所在地市,
    SUM(s.订购数量) AS 总销量,
    ROW_NUMBER() OVER (PARTITION BY s.所在省份 ORDER BY SUM(s.订购数量) DESC) AS 省内排名
FROM sales_orders s
JOIN products p ON s.商品编号 = p.商品编号
WHERE p.商品大类 = '护肤品'
GROUP BY s.所在省份, s.所在地市
ORDER BY s.所在省份, 省内排名;

-- 4. 江苏省护肤品小类销量
SELECT 
    p.商品小类,
    SUM(s.订购数量) AS 总销量
FROM sales_orders s
JOIN products p ON s.商品编号 = p.商品编号
WHERE p.商品大类 = '护肤品' AND s.所在省份 = '江苏省'
GROUP BY p.商品小类
ORDER BY 总销量 DESC;

-- 5. 江苏省彩妆小类销量
SELECT 
    p.商品小类,
    SUM(s.订购数量) AS 总销量
FROM sales_orders s
JOIN products p ON s.商品编号 = p.商品编号
WHERE p.商品大类 = '彩妆' AND s.所在省份 = '江苏省'
GROUP BY p.商品小类
ORDER BY 总销量 DESC;
