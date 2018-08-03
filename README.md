# Tencent2018_Final_Phrase_Presto

腾讯2018广告大赛的决赛代码（初赛决赛数据格式一样，其实没区别。）。
两个LGB模型融合，最后成绩0.7534

赛题为相似人群拓展（Lookalike），基于广告主提供的一个种子人群（又称为种子包），自动计算出与之相似的人群（称为扩展人群）。
题目具体内容和相关介绍请看官网链接（包含原始数据）：http://algo.qq.com/home/information/info.html

------------------------------------
由于本次比赛数据量巨大，加上本人能力和毕业季精力有限，本开源的成绩并不是很理想，仅供参考。
这是一个纯LGB模型，包括普通统计模型和独热统计模型两部分，分别单独跑出两个模型的结果后，对result进行平均已获得最终结果。

普通统计特征包括：
简单ID计数统计，对kw,topic做词向量训练后聚类，利用交叉窗口统计ID的转化次数等。

独热统计特征包括：
简单ID独热编码，几个交叉ID的独热编码，interest,kw,topic的词袋编码。

比赛打得很间断，特征是一步步生成的，普通统计模型需按顺序运行feature_dig_v1-v8，然后运行LGB模型的训练，onehotModel文件夹下保存的是独热模型，
需要单独训练（由于OneHot内存占用巨大，该模型我只取了部分数据来做独热）
preProcessing.py为对原始数据的预处理（原始数据扔到data/origin目录下，剩下的中间结果会保存到目录的各个文件夹下）。
resultProcessing.py用于对两个模型进行加权平均。

总而言之，很多东西都写的很粗糙，看看就好，本届比赛其实是NN的天下。

*初赛时本人尽力使用笔记本打比赛，发现这届数据量实在撑不住，NN用的也不太熟练就放弃了，最后还是使用了服务器，所以这份代码对内存需求还是很大的。

------------------------------------

有兴趣的可以看看我去年的代码（明示骗点击）：https://github.com/BladeCoda/Tencent2017_Final_Coda_Allegro
