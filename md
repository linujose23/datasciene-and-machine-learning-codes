                                        NewsRecommender(Content-based)


* first we imported all the required Functions like Numpy(For numerical Operations),sklearn Cosine,NLTK Functions,Counter function to get unique words only we used it here we pick the keys.
,Pandas For Reading Data (News.csv)
For Vectorizing our Articles after removing all the un-necessary elements like Regular Expression and Tokenizing our Articles For (Vectorizing and to lighten our matrix)
the Cleaning of the Articles is done through Clean_Tokenize Function that has been created for cleaning the data and NLP functions have also been used to further process the data.

* Then we created an empty list  Total_words then we applied a For loop for Tokenizing each word in our cleaned_articles and Appended it to our empty List Total_words to further use it inside the counter Function.

* We used Counter function here only to get Unique words which are our(keys) and stored it in a variable VOcab we store all the keys from counts (Counter gives counts of words but we only need unique words in the form of dictionary).

* After getting unique words from the Counter Function we Remove Stop Words from it.

* Then we enumerate the Stops_removed(words after removing stop words) and define it as a dictionary to give our self Vocabulary in Tfidf Vectorizer else it will use predefined dictionary of Tfidf which contains lots of Unnecssary words Vocab so to avoid that we give our self VOcabulary thus it also gives a lighter matrix after Vectorizing.

* We Vectorize it after Giving our self Vocabulary (Final_vocab) in Tfidf Vectorizor thus we get the Vectors in the form of Matrix shape(4831 docs and some length of words in columns). 

* Now we used LatentDirichletAllocation(Topic-Modelling) in order to get Articles and Topics(which are Pre Trained in Neural Networks thus we only need to use it) here i have given 8 topics so our matrix we get will be (4831,8) 4831 docs and 8 Topics.

* Now we split it word by word to Calculate the average time to be spent by user to read the Article as mentioned down the Formula used here below.

                  
                   # Formula used to Calculate avg time,interest time Value and User_Profile :
                   
                   
                   
          * First we need to calculate the average time for all article,

                  as time = distance / speed

                  so in our case

                  time = length of article / time  (assumption  (5 word/sec))



                  for example:- user read article number 2 and 7, so we will pick the article vector of 2 and 7

                  2nd Article:- [0.1, 0.5, 0.3, 0.1]

                  7th Article:- [0.2, 0.3, 0.1, 0.4]

                  and time spend

                  2nd Article:- 300 sec

                  7th Article:-700 sec 



                  now time value

                  2nd article time / average time we calculated  (300/600)

                  7th article time / average time we calculated  (700/1000)



                  finally 

                  2nd article vector * 2nd article time value + 7th article vector * 7th article time value

                  ([0.1, 0.5, 0.3, 0.1] * (300/600)) + ( [0.2, 0.3, 0.1, 0.4] * (700/1000))

                  that is our user profile 

                  if we choose the vector as LDA(topic modelling) so we can normalize the final matrix that is our user profile



                  but there are some issues in it like

                  if user spend more time then our average time 

                  for that we use sigmoid 



                  for simplifying the calculations or speed up the process:-



                  make a vector of

                  user read article i.e [[0.1, 0.5, 0.3, 0.1], [0.2, 0.3, 0.1, 0.4]] name it user read article matrix



                  time value i.e [(300/600), (700/1000)] name it time value matrix

                  take sigmod of time value matrix



                         now

                        user read article matrix * sigmoid(time value matrix)

                        this is User profile

                        in case of LDA(Topic modelling use normalization)

 
* The above Formula is used to Create the User_Profiler Function from which we will get our User profiles calculated so in this Function im passing
 three user read Articles and Wordtokenized Article (To Calculate Avg time and here i have given words per second assumed by myself we take 5 words per second),
 and we give our an assumed time ourselves that is article_time(the time user actually spent on the particular article).
 
 * from the User_profiler Function we get user profiles which in this case i have passed three user parameters so we get three user_profile we there for put it all together into a single list.
 
 * Then we take Cosine similarity to get User_preffered Articles thus we get user preffered articles to recommend as per user read Articles we get the similiar articles through Cosine similarity.
 
 * now we used Argsort Function which returns the indexes of Maximum Values out of 1 and Reverse the result in order to get the maximum scores so maximum scores means the indexes of Articles the users are most interested in
   we thus pick Top five articles to recommend after reversing it to descending order thus we get max value indexes of Articles at top.
   
   * Finally we Recommend the Titles of articles as per our Top five indexes or user Interested Articles.
   
   
   
   ************************************************************************************************************************************************************************************************************************************************
 
 
 


