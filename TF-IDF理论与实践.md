
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

  (0, 677125)   0.25191372784801147
  (0, 12690)    0.03284846297775902
  (0, 616921)   0.040651423405947164
  (0, 674148)   0.7135910842275884
  (0, 465336)   0.011897095845137168
  (0, 360142)   0.017637060053488276
  (0, 22487)    0.12531092159647053
  (0, 740583)   0.015209752680132731
  (0, 320365)   0.010741068946503824
  (0, 604051)   0.008679870400650444
  (0, 96589)    0.018207483739320393
  (0, 451343)   0.1734177114880802
  (0, 516)      0.023404048783309032
  (0, 5596)     0.020498800024591354
  (0, 430925)   0.010850118658001173
  (0, 411199)   0.032740521721721684
  (0, 294745)   0.009092793961648946
  (0, 502521)   0.010252109832213887
  (0, 127841)   0.033902030539070475
  (0, 422014)   0.01570790898398023
  (0, 693832)   0.008577130665063857
  (0, 201864)   0.009763086844980954
  (0, 758924)   0.022186082536757783
  (0, 139081)   0.019190592703078393
  (0, 678511)   0.022760198674761718
  :     :
  (81820, 476506)       0.030541869428446194
  (81820, 430519)       0.056718418982837256
  (81820, 288457)       0.03431933738901778
  (81820, 43909)        0.03321138734758029
  (81820, 17472)        0.03517873020699229
  (81820, 283650)       0.07004302489747975
  (81820, 440363)       0.038183355065253964
  (81820, 56753)        0.038183355065253964
  (81820, 326562)       0.09402465290618824
  (81820, 516821)       0.038183355065253964
  (81820, 389038)       0.03383729654357864
  (81820, 592614)       0.038183355065253964
  (81820, 710405)       0.0334089332257708
  (81820, 299399)       0.03895619816756387
  (81820, 237200)       0.0385504231858485
  (81820, 4107) 0.0694502247414663
  (81820, 714264)       0.03992408549142323
  (81820, 194400)       0.03753997962497213
  (81820, 442311)       0.03895619816756387
  (81820, 632568)       0.04207933392295712
  (81820, 675879)       0.0412199411049826
  (81820, 646457)       0.0431872839643946
  (81820, 584586)       0.08949770368418243
  (81820, 744778)       0.044748851842091215
  (81820, 592304)       0.044748851842091215



