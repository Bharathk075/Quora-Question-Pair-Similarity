# Quora-Question-Pair-Similarity
Quora is a place to gain and share knowledge—about anything. It’s a platform to ask questions and connect with people who contribute unique insights and quality answers. This empowers people to learn from each other and to better understand the world.
Over 100 million people visit Quora every month, so it's no surprise that many people ask similarly worded questions. Multiple questions with the same intent can cause seekers to spend more time finding the best answer to their question, and make writers feel they need to answer multiple versions of the same question. Quora values canonical questions because they provide a better experience to active seekers and writers, and offer more value to both of these groups in the long term.

# Challenges
* Identify which questions asked on Quora are duplicates of questions that have already been asked. 
* This could be useful to instantly provide answers to questions that have already been answered. 
* We are tasked with predicting whether a pair of questions are duplicates or not. 
# Metrics 
* log-loss

* It is a binary classification problem, for a given pair of questions we need to predict if they are duplicate or not.
* We shall build the features using the techniques of Natural Language Processing and google word vectors
# Featurization
Let us now construct a few features like:
* ____freq_qid1____ = Frequency of qid1's
* ____freq_qid2____ = Frequency of qid2's 
* ____q1len____ = Length of q1
* ____q2len____ = Length of q2
* ____q1_n_words____ = Number of words in Question 1
* ____q2_n_words____ = Number of words in Question 2
* ____word_Common____ = (Number of common unique words in Question 1 and Question 2)
* ____word_Total____ =(Total num of words in Question 1 + Total num of words in Question 2)
* ____word_share____ = (word_common)/(word_Total)
* ____freq_q1+freq_q2____ = sum total of frequency of qid1 and qid2 
* ____freq_q1-freq_q2____ = absolute difference of frequency of qid1 and qid2 
* __cwc_min__ :  Ratio of common_word_count to min lenghth of word count of Q1 and Q2 <br>cwc_min = common_word_count / (min(len(q1_words), len(q2_words))
* __cwc_max__ :  Ratio of common_word_count to max lenghth of word count of Q1 and Q2 <br>cwc_max = common_word_count / (max(len(q1_words), len(q2_words))
* __csc_min__ :  Ratio of common_stop_count to min lenghth of stop count of Q1 and Q2 <br> csc_min = common_stop_count / (min(len(q1_stops), len(q2_stops))
* __csc_max__ :  Ratio of common_stop_count to max lenghth of stop count of Q1 and Q2<br>csc_max = common_stop_count / (max(len(q1_stops), len(q2_stops))
* __ctc_min__ :  Ratio of common_token_count to min lenghth of token count of Q1 and Q2<br>ctc_min = common_token_count / (min(len(q1_tokens), len(q2_tokens))
* __ctc_max__ :  Ratio of common_token_count to max lenghth of token count of Q1 and Q2<br>ctc_max = common_token_count / (max(len(q1_tokens), len(q2_tokens))
* __last_word_eq__ :  Check if First word of both questions is equal or not<br>last_word_eq = int(q1_tokens[-1] == q2_tokens[-1])
* __first_word_eq__ :  Check if First word of both questions is equal or not<br>first_word_eq = int(q1_tokens[0] == q2_tokens[0])
* __abs_len_diff__ :  Abs. length difference<br>abs_len_diff = abs(len(q1_tokens) - len(q2_tokens))
* __mean_len__ :  Average Token Length of both Questions<br>mean_len = (len(q1_tokens) + len(q2_tokens))/2
* __fuzz_ratio__ :  https://github.com/seatgeek/fuzzywuzzy#usage
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
* __fuzz_partial_ratio__ :  https://github.com/seatgeek/fuzzywuzzy#usage
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
* __token_sort_ratio__ : https://github.com/seatgeek/fuzzywuzzy#usage
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
* __token_set_ratio__ : https://github.com/seatgeek/fuzzywuzzy#usage
http://chairnerd.seatgeek.com/fuzzywuzzy-fuzzy-string-matching-in-python/
* __longest_substr_ratio__ :  Ratio of length longest common substring to min lenghth of token count of Q1 and Q2<br>longest_substr_ratio = len(longest common substring) / (min(len(q1_tokens), len(q2_tokens))
* TF-IDF Average WORD-TO-VECTORS

# ML Models Implemented:
* Random Probability Model
* Logistic Regression with Hyperparameter Tuning (Best alpha = 0.01)
* Linear SVM with Hyperparameter Tuning (Best alpha = 1)
* XG-Boost with Default parameters
* XG-Boost with Hyperparameter Tuning (Best parameters:'n_estimators': 100, 'max_depth': 3)

# Results
| Model | Parameters | Log-loss |
| --- | --- | --- |
| Random Probability Model	|  | 0.849 |
| Logistic Regression	| alpha = 0.01 | 0.466 |
| Linear SVM	| alpha = 1 | 0.618 |
| BG-Boost	| Default | 0.358 |
| XG-Boost	| 'n_estimators': 100, 'max_depth': 3 | 0.3521 |
