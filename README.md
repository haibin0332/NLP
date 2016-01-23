# NLP

reading and practicing

http://blog.csdn.net/yangliuy/article/details/8330640

pos_tag with stanford tagger

java -mx300m -cp stanford-postagger.jar edu.stanford.nlp.tagger.maxent.MaxentTagger -model models/chinese-distsim.tagger -textFile del.txt -outputFile out.txt

http://www.elias.cn/Python/JPype

jieba 词性标注

http://www.hankcs.com/nlp/corpus/several-revenue-segmentation-system-used-set-of-source-tagging.html

stanford 词性标注

ROOT：要处理文本的语句
IP：简单从句
NP：名词短语
VP：动词短语
PU：断句符，通常是句号、问号、感叹号等标点符号
LCP：方位词短语
PP：介词短语
CP：由‘的’构成的表示修饰性关系的短语
DNP：由‘的’构成的表示所属关系的短语
ADVP：副词短语
ADJP：形容词短语
DP：限定词短语
QP：量词短语
NN：常用名词
NR：固有名词
NT：时间名词
PN：代词
VV：动词
VC：是
CC：表示连词
VE：有
VA：表语形容词
AS：内容标记（如：了）
VRD：动补复合词
CD: 表示基数词
DT: determiner 表示限定词
EX: existential there 存在句
FW: foreign word 外来词
IN: preposition or conjunction, subordinating 介词或从属连词
JJ: adjective or numeral, ordinal 形容词或序数词
JJR: adjective, comparative 形容词比较级
JJS: adjective, superlative 形容词最高级
LS: list item marker 列表标识
MD: modal auxiliary 情态助动词
PDT: pre-determiner 前位限定词
POS: genitive marker 所有格标记
PRP: pronoun, personal 人称代词
RB: adverb 副词
RBR: adverb, comparative 副词比较级
RBS: adverb, superlative 副词最高级
RP: particle 小品词 
SYM: symbol 符号
TO:”to” as preposition or infinitive marker 作为介词或不定式标记 
WDT: WH-determiner WH限定词
WP: WH-pronoun WH代词
WP$: WH-pronoun, possessive WH所有格代词
WRB:Wh-adverb WH副词

#NLTK 用法

http://blog.csdn.net/liushulinle/article/details/18816965

http://blog.csdn.net/liushulinle/article/details/18817019

#Tools

http://m.blog.csdn.net/blog/huyoo/12188573


#important python code

1)re.sub("[\s+\.\!\/_,$%^*(+\"\']+|[+——！，。？、~@#￥%……&*（）=。]+|[“”]+".decode("utf8"), "".decode("utf8"), genrefield) 

2)sorted(word_dict.items(), key=lambda d: d[1]) 根据value值排序

3)#!/usr/bin/env python # -*- coding: utf-8 -*-

4)if dict.get(keyset, 0)!=0: #hash method  get(keyset, default) 不存在则返回0，如果不为零，exist


#output word2vec


import gensim
import codecs


if __name__=='__main__':
    
    print 'wait loading model...'    
    
    model_path = r'../data/worddata/vectors.bin'   
    f = codecs.open(r'../data/worddata/simwords_result.txt', 'wb', 'utf-8')  
    model = gensim.models.Word2Vec.load_word2vec_format(model_path, binary=True)  # C binary format
    print 'waiting loading dictionary...'
    
    wordsdict = [unicode(line.strip(), 'utf8') for line in open(r'../data/worddata/fullworddict.txt')]
    wordsdict=set(wordsdict)
    
    #time.sleep(100)
    print 'finish loading'
    
    while True:
        
        input_options=raw_input('Enter a raw word: '.encode('utf-8'))
      
        if input_options.decode('utf8') in wordsdict:
            # Open the key file and read the key
            sim_words=model.most_similar(input_options.decode('utf8'), topn=200)
            for sim_word in sim_words:
                #print sim_word[0], sim_word[1]
                f.write('%s %0.8f\n' %(sim_word[0], sim_word[1]))
            sim_words=model.most_similar(input_options.decode('utf8'), topn=20)
            for sim_word in sim_words:
                print sim_word[0], sim_word[1]   
            print 'Finish...'       
        else:
            print 'Input word not in dictionary, please reenter.'

    
