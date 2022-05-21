# qoura-question-pair
 This is a NLP project to solve kaggle competition 'Duplicate question pair' by qoura
 
 
- ##[Approach1] : with Basic Features--------
 
-Initial models were trained on 6007 features
-used 3000 bow features for q1 + 3000 bow features of q1
 
 -used additional 7 features  that many kaggle notebooks had used it:
 1) q1_len   -> char of length of q1
 2) q2_len   -> char of length of q2
 3) q1_words -> no. of words in q1
 4) q2_words -> no. of words in q2
 5) words_common -> no. of common unique words
 6) words_total  -> total no. of words in q1 + total no. of words in q2
 7) words_share  -> words  common/words_total
