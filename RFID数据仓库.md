# RFID数据仓库设计

### 1 设计数据仓库

RFID数据格式为（RFID，at_location，time）

标签数据格式为（RFID，product_name，product_category，producer，date_produced，price）

### 2 冗余信息剔除

将相同RFID、at_location、time的数据进行剔除

将相同产品的数据剔除

### 3 数据处理

数据一般是不完整的、有噪声的和不一致的。数据清理例程试图填充缺失的值、光滑噪声并识别离群点、纠正数据中的不一致

对于缺失值使用邻近值进行填补

对于id误读使用删除方法

### 4 联机分析过程

1. 按月：直接搜集time，product_category标签，获取当月所有的数据，之后固定location==A和location==B的数据，两者数据相减
2. 按品牌：直接搜集producer，product_category标签，获取当月所有的数据，之后固定location==A和location==B的数据，两者数据相减
3. 按价格区间：直接搜集price属于【区间】，product_category标签，获取当月所有的数据，之后固定location==A和location==B的数据，两者数据相减

### 5 找问题

确定data_produced时间和和time，相减看是否大于保质期，如果大于保质期就确定at_location的值，值如果在运输就是运输问题，如果是存储就是存储问题
