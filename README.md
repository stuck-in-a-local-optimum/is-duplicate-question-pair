# qoura-question-pair
 This is a NLP project to solve kaggle competition 'Duplicate question pair' by qoura
 
 
- [Approach1](https://github.com/stuck-in-local-optimum/qoura-questn-pairs/blob/main/src/bow-with-basic-features.ipynb) : BOW WITH BASIC FEATURES
 
- used 6007 features
- 3000 bow features for q1 + 3000 bow features of q2
 
 7 additional features inspired from different kaggle notebooks:
 1) q1_len   -> char of length of q1
 2) q2_len   -> char of length of q2
 3) q1_words -> no. of words in q1
 4) q2_words -> no. of words in q2
 5) words_common -> no. of common unique words
 6) words_total  -> total no. of words in q1 + total no. of words in q2
 7) words_share  -> words  common/words_total

- After some analysis on above 7 features, 3 of them seems to be useful features





word_common                       |  word_total                      |                  word_share
:--------------------------------:|:--------------------------------:|:--------------------------------: 
<img width="389" alt="Screenshot 2022-05-22 at 01 03 57" src="https://user-images.githubusercontent.com/55681180/169666624-8597945b-9add-44f6-abb1-cab5f4c8c0a7.png">  | <img width="390" alt="Screenshot 2022-05-22 at 01 20 06" src="https://user-images.githubusercontent.com/55681180/169667007-98243566-be21-4ede-8da3-92b7738fe3a2.png"> | <img width="389" alt="Screenshot 2022-05-22 at 01 18 05" src="https://user-images.githubusercontent.com/55681180/169666948-5207561b-d074-4ce4-86a7-6a92a097bd1f.png">

- Above we can see, if the value of word_common for a sample is <=4 then there is high probability for the pair to be non_duplicate pair
- if the value of word_total for a sample <=20 then there is high probability for the pair to be duplicate pair
- if the value fo word_share is <=0.2 then probability of non_duplicate pair is higher


- ## [Final Approach](https://github.com/stuck-in-local-optimum/qoura-questn-pairs/blob/main/src/bow-with-preprocessing-and-advanced-features.ipynb): preprocessing and advanced features
- so far we haven't done any preprocessing, preprocessing would definitely improve our model's performance
- following preprocessing had been done on text of question1 and question2
  - replaced al special characters with their string equivalents, e.g., % --> percent
  - the pattern '[math]' appeared 900 times in the data, replaced them with ""
  - expanded the contracting words, e.g., "ain't" --> "am not"
  - removed html tags
  - removed punctuations

- After reading different blogs and kaggle notebooks I got to know to solve this problem we need to create some advanced features
- After collecting from different kaggle notebooks and blogs I had used following advanced features
  - TOKEN FEATURES
   -  cwc_min      : this is the ratio of no. of common words to the length of the smaller question
   -  cwc_max      : this is the ratio of no. of common words to the length of the larger question
   -  csc_min      : this is the ratio of no. of common stop words to the smaller stop word count among the two questions
   -  csc_max      : this is the ratio of no. of common words to the length of the larger question
   -  ctc_min      : this is the ratio of the number of common tokens to the smalller token count among the two questions
   -  ctc_max      : this is the ratio of the number of common tokens to the larger token count among the two questions
   -  last_word_eq : 1 if the last word in the two questions is same, 0 otherwise  
   -  first_word_eq: 1 if the first word in the two questions is same, 0 otherwise  
 - LENGTH BASED FEATURES
   - mean_len             : mean of the length of two questions (no. of words)
   - abs_len_diff         : Absolute difference between the length of the two questions (no. of words)
   - longest_substr_ratio : ratio of the length of the longest substring among the two questions to the length of smaller question
  
 - FUZZY FEATURES: Following 4 features are taken from fuzzywuzzy library, [this](https://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/) short blog easily explained the same.
   - fuzz_ratio         : fuzz_ratio score from fuzzywuzzy library
   - fuzz_partial_ratio : fuzz_partial_ratio from fuzzywuzzy library
   - token_sort_ratio   : token_sort_ratio from fuzzywuzzy library
   - token_set_ratio    : token_set_ratio from fuzzywuzzy library
  
  
  min features                       |  max features                      |                  last and first word equal
:--------------------------------:|:--------------------------------:|:--------------------------------: 
<img width="612" alt="Screenshot 2022-05-22 at 17 25 08" src="https://user-images.githubusercontent.com/55681180/169694837-cef2d5ac-ea1c-4bc9-bbd1-68c368c398e8.png"> | <img width="612" alt="Screenshot 2022-05-22 at 17 52 24" src="https://user-images.githubusercontent.com/55681180/169694910-6c979e2b-e849-49c0-8f42-4f0500ae57f5.png">  |  <img width="414" alt="Screenshot 2022-05-22 at 17 54 15" src="https://user-images.githubusercontent.com/55681180/169694979-81c4243f-541e-43ed-ad09-429a89f76ebe.png">



  
  - EDA ON THESE ADVANCED FEATURES
  <img width="612" alt="Screenshot 2022-05-22 at 17 25 08" src="https://user-images.githubusercontent.com/55681180/169694625-b6f1e6bb-55bd-4eee-911d-9195c7e89691.png">
    - In the above figure, from diagonal plots we can argue that ctc_min, cwc_min, and csc_min are useful features since they are able to classifiy the duplicate and non-duplicate question pairs to some extent though they are overlapping points as well


