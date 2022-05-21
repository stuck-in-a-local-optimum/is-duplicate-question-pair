# qoura-question-pair
 This is a NLP project to solve kaggle competition 'Duplicate question pair' by qoura
 
 
- # Approach1 : with Basic Features--------
 
-Initial models were trained on 6007 features
-used 3000 bow features for q1 + 3000 bow features of q2
 
 -used following 7 additional features inspired from different kaggle notebooks:
 1) q1_len   -> char of length of q1
 2) q2_len   -> char of length of q2
 3) q1_words -> no. of words in q1
 4) q2_words -> no. of words in q2
 5) words_common -> no. of common unique words
 6) words_total  -> total no. of words in q1 + total no. of words in q2
 7) words_share  -> words  common/words_total

- After some analysis on above 7 features, some of them seems to be useful features
- ### word_common
- Here we can see, if word_common b/w q1 and q1 is <=4 then there is high probability for the pair to be non_duplicate
<img width="389" alt="Screenshot 2022-05-22 at 01 03 57" src="https://user-images.githubusercontent.com/55681180/169666624-8597945b-9add-44f6-abb1-cab5f4c8c0a7.png">
