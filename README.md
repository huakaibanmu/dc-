# 登录DC竞赛下载数据
http://www.dcjingsai.com/common/cmpt/%E2%80%9C%E8%BE%BE%E8%A7%82%E6%9D%AF%E2%80%9D%E6%96%87%E6%9C%AC%E6%99%BA%E8%83%BD%E5%A4%84%E7%90%86%E6%8C%91%E6%88%98%E8%B5%9B_%E6%88%91%E7%9A%84%E9%98%9F%E4%BC%8D.html

# 数据下载地址
链接：https://pan.baidu.com/s/13IMDPMz0rf8kM1JAea53uQ 
密码：y6m4
大小：488.5M

# 导入要用到的pandas库、sklearn的train_test_split模块
import pandas as pd
from sklearn.model_selection import train_test_split

# 读数据（先读前1000行测试一下）
filedata = pd.read_csv('data/train_set.csv', nrows=1000)
print(filedata)

数据说明：数据有4列：id, article, word_seg, class. id 为数据索引, article和word_seg分别是脱敏后用数字对文章“字”、“词”的表示，class就是文章类型的标注，也就是模型输出要拟合的值。

# 训练集和验证集拆分,取20%的数据作为验证集
x_train, x_val, y_train, y_val = train_test_split(filedata[['article', 'word_seg']], filedata['class'], test_size=0.2)

之后还会涉及到对训练集和测试集进一步处理，先给自己找一台服务器是正事。

