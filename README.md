
In [1]:

from nltk.corpus import stopwords
from nltk.stem import PorterStemmer
from nltk.tokenize import word_tokenize, sent_tokenize

In [8]:

def create_freq_table(text) -> dict:
    stop_words = set(stopwords.words("english"))
    words = word_tokenize(text)
    ps = PorterStemmer()
    
    freq_table = {}
    for w in words:
        word = ps.stem(w)
        if word in stop_words:
            continue
        if word in freq_table:
            freq_table[word] += 1
        else:
            freq_table[word] = 1
    
    return freq_table

In [18]:

def scoring_sentences(sentences, freq_table) -> dict:
    sent_value = {}
    
    for s in sentences:
        word_count = len(word_tokenize(s))
        for val in freq_table:
            if val in s.lower():
                if s[:10] in sent_value:
                    sent_value[s[:10]] += freq_table[val]
                else:
                    sent_value[s[:10]] = freq_table[val]
        sent_value[s[:10]] = sent_value[s[:10]]
    
    return sent_value

In [20]:

def avg_score(sent_val) -> int:
    sum_val = 0
    for val in sent_val:
        sum_val += sent_val[val]
    
    
    avg_val = sum_val // len(sent_val)
    
    return avg_val

In [5]:

def summary(sent, sent_val, thres):
    sent_count = 0
    summary = ''
    
    for s in sent:
        if s[:10] in sent_val and sent_val[s[:10]] > (thres):
            summary += ' ' + s
            sent_count += 1
    
    return summary

In [21]:

# Freq table
text = ''

with open("untitled.txt", encoding="utf8") as f:
    text = f.read()

freq_table = create_freq_table(text)

sents = sent_tokenize(text)

sent_scores = scoring_sentences(sents, freq_table)

threshold = avg_score(sent_scores)

summary = summary(sents, sent_scores, 1.5 * threshold)

print(summary)

 “This was a pioneering experiment that allowed one to infer the simultaneous position of a particle in two places,” says Elitzur’s colleague Eliahu Cohen of the University of Ottawa in Ontario. The experiment is designed so the probe photon can only show interference if it interacted with the shutter photon in a particular sequence of places and times: namely, if the shutter photon was in both boxes A and C at some time (t1), then at a later time (t2) only in C, and at a still later time (t3) in both B and C. So interference in the probe photon would be a definitive sign the shutter photon made this bizarre, logic-defying sequence of disjointed appearances among the boxes at different times—an idea Elitzur, Cohen and Aharonov proposed as a possibility in 2017 for a single particle spread across three boxes. Through the lens of the TSVF, Elitzur says, this flickering, ever changing existence can be understood as a series of events in which a particle’s presence in one place is “canceled” by its own “counterparticle” in the same location. “The experiment is bound to work,” Wharton says—but he adds it “won’t convince anyone of anything, since the results are predicted by standard quantum mechanics.” In other words, there would be no compelling reason to interpret the outcome in terms of the TSVF rather than one of the many other ways that researchers interpret quantum behavior. And if someone thinks they can formulate a different picture of “what is really going on” in this experiment using standard quantum mechanics, he adds, “Well, let them go ahead!”

He is confident that the work heralds “nothing short of a revolution within quantum mechanics.” Now that measurement methods have become precise enough, he says, “you can be sure that notions like retrocausation are going to become part and parcel of quantum reality.”

In [ ]:


