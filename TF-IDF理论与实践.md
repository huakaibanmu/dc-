
# TF-IDF是什么？
  TF-IDF是Term Frequency-Inverse Documentory Frequency的缩写，翻译出来是“词频-逆文本频率”，用来评估一个词对于一个文件集或者语料库中的其中一份文件的重要程度，用在文本分词、向量化之后，用来描述文本中的词特征，属于机器学习前的预处理部分。
 
# TF-IDF是如何描述词特征的？
TF指的是词频，也就是文本分词后各词出现的频率，但是在文本中会经常出现的‘I’ 'to'之类的词，其频率虽然高，但对于文本的重要性低于‘travel’ ‘tea’之类的词，因此IDF是对TF的进一步修正，避免仅仅用词频来表示词特征。
在定性的角度上，IDF反映了一个词在所有文本中出现的频率，如果一个词在很多文本中都有出现，如 'to'，IDF应该低；一个词如果在较少的文本中出现，IDF应该是高的。
在定量的角度上，这里给出得出一个词的IDF的计算公式：

<img src="http://chart.googleapis.com/chart?cht=tx&chl=IDF(x) = log\frac{N}{N(x)}" style="border:none;">

N代表语料库中所有文本的总数，N(x)代表语料库中含有x词的文本总数。因此在极端的例子中，一个词在所有的文本中都出现，这个词的IDF就是0。

**平滑后的IDF：**
如果一个生僻词语料库中没有，这时分母N(x)为0，IDF没有意义。因此要对上面的公式进一步平滑处理：

<a href="https://www.codecogs.com/eqnedit.php?latex=IDF(x)&space;=&space;log\frac{N&plus;1}{N(x)&plus;1}&space;&plus;&space;1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?IDF(x)&space;=&space;log\frac{N&plus;1}{N(x)&plus;1}&space;&plus;&space;1" title="IDF(x) = log\frac{N+1}{N(x)+1} + 1" /></a>

**TF-IDF计算**
TF-IDF = <a href="https://www.codecogs.com/eqnedit.php?latex=TF(x)&space;*&space;IDF(x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?TF(x)&space;*&space;IDF(x)" title="TF(x) * IDF(x)" /></a>
其中TF就是词x在文本中出现的频率。

# 用scikit-learn实现TF-IDF
```
from sklearn.feature_extraction.text import TfidfVectorizer
tfidfs = TfidfVectorizer()
re = tfidfs.fit_transform(corpus)
print re
```
# 处理达观杯数据（结合作业一）：
```
import pandas as pd
from sklearn.model_selection import train_test_split
from sklearn.feature_extraction.text import TfidfVectorizer

filedata = pd.read_csv('new_data/train_set.csv')
x_train, x_val, y_train, y_val = train_test_split(filedata[['article', 'word_seg']], filedata['class'], test_size=0.2)
tfidf = TfidfVectorizer()
vectorizer = tfidf.fit(x_train['word_seg'])
X_train = vectorizer.fit_transform(x_train['word_seg'])
X_valid = vectorizer.fit_transform(x_val['word_seg'])
print(X_train)
```

输出数据




