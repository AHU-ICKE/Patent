# HTW模型

## 环境要求

本模型在Python 3.6环境下测试成功

所需包：

beautifulsoup4\==4.10.0
gensim\==3.8.3
gevent\==21.12.0
jieba\==0.42.1
matplotlib\==3.3.4
nltk\==3.4.5
numpy\==1.18.2
pandas\==1.1.5
scikit_learn\==1.0.2
scipy\==1.4.1
tqdm\==4.48.2

requierments.txt文件列出本模型所需的第三方库

## 项目结构

- Document为数据集文件夹，包含A61和USPTO数据集，w2v文件夹用以存储word2vec模型运行结果

- ExpResult为推荐结果文件夹，用以存储每个数据集中测试集的推荐结果

- FenciInf为停用词词表和AI领域词表

- Model_A61和Model_USPTO，分别对应Document文件夹下的A61和USPTO数据集的模型代码

- SaveOldResult为模型训练参数及结果存储文件夹

  

## 运行方式

以Model_A61中的代码为例，以下命令可直接运行模型训练及测试：

`python Experiment.py`

由于训练时间较长，建议放在服务器后台训练：

`nohup python -u Experiment.py &`

用`tail -f nohup.out`命令查看模型打印输出内容

Experiment.py为模型训练及测试入口

训练主要代码为163-172行：

```python
run_fenci(pat_corpus.inf, Parm)
length_all, length_single, patent, word2id, inventor2id, company2id, id2doc = Parm.GetWordResult(pat_ids, pat_corpus.inf)
sentences = []
for key, value in patent.items():
   sentences.append(value['fenci'])
train_word2vec(sentences, corpus='a61', train=True)
run_ict(topicnum, 100, Parm, train_ids, target_ids, pat_corpus.inf)
```

余下为测试代码，如果训练结束后想多次测试，可以将上述代码注释

