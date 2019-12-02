## SCS 3253 020 - Machine Learning Term Project - December 2019
## Apple App Store Games
### Team 7: 
Leona Yiu & Xiaoxu Zhang

### Overview
The objective of this project is to predict the success of a game from the Apple App Store based on the appearance of the game's icon, in particular the 512x512 pixels in the icon jpg. For this project, we are hoping to determine how the pixel features involved in the game's icon can determine the game's success, which would be measured by the Average User Rating as well as the User Rating Count. 

### Data Set
The data source was obtained from Kaggle via the following [link](https://www.kaggle.com/tristan581/17k-apple-app-store-strategy-games) .
The data set comprises 17,007 strategy games available on the Apple App Store and was collected on August 3rd, 2019 using the iTunes API and the App Store sitemap. The following are the attributes contained in this data set:

1. URL: URL of the game in the Apple App Store
2. ID: The assigned ID
3. Name: Name of the game
4. Subtitle: Secondary text under the name
5. Icon URL: 512px x 512px jpg
6. Average User Rating: Rounded to nearest .5, requires at least 5 ratings
7. User Rating Count: Number of ratings internationally, null means it is below 5
8. Price: Price in USD
9. In-app Purchases: Prices of available in-app purchases
10. Description: App description
11. Developer: App developer
12. Age Rating: Either 4+, 9+, 12+ or 17+
13. Languages: ISO2A language codes
14. Size: Size of the app in bytes
15. Primary Genre: The main genre
16. Genres: Genres of the app
17. Original Release Date: When game was released
18. Current Version Release Date: When game was last updated

### Data Preparation
The main field of interest is the Icon URL for each of the games listed in the Apple App Store data set. From each Icon URL, the 512x512 pixels in the game's icon jpg is converted into 512x512 strings of 3 color code (RGB format). Based on the color codes involved in the icon, a function is defined in order to determine a) the count of colors taking more than 10% of the full image (hpercent_c_cnt), b) count of colors taking less than 0.1% of the full image (lpercent_c_cnt), and c) count of pixels of the color that appears the most in the icon (max_c_cnt). A final csv is exported after processing each of the game's icons with these 3 new features added to the original data set for further analysis and modeling. 

[Link to Data Preparation Code](https://github.com/leonayiu/Apple-App-Store-Games/blob/master/Data_Exploration.ipynb)

[Link to Output File after processing Game Icons](https://github.com/leonayiu/Apple-App-Store-Games/blob/master/AppStore_Games_Icon_Pixel.xlsx) 

### Data Exploration & Modeling 
After dropping any records where the Icon URL and Average User Rating fields were null, there remained 3,027 records which have a game rating of >= 4 and User Rating Count >= 50. Majority of these high rated games (2,317 / 3,027 = 77%) have icon images with 0 color that takes up more than 10% of the full image (hpercent_c_cnt) and <27,000 pixels of the color that appears the most in the icon (max_c_cnt). 
Based on these observations of the high rated games, these two parameters were used as the feature variables for establishing our model.
The data set was trained using the Random Forest Classifier, where engineered feature variables hpercent_is_0 and max_cnt_is_less_27000 were used to predict the target variable 'Great_App' (having a rating 4 or more).

[Link to Data Exploration & Modeling Code](https://github.com/leonayiu/Apple-App-Store-Games/blob/master/Data_Exploration_Modeling.ipynb)

### Results
Confusion Matrix Results: 
Model accurately predicted 1664 / 2269 (73%) cases that the game is a Great App (high rating of 4 or higher). However, there are 605 cases (25%) cases where the model incorrectly predicted that the game is a Great App, when based on the actual average user ratings from the data set, the games had low ratings.

lassification Report Results: 
73% precision classifying that a game is a Great App based on feature variables hpercent_is_0 and max_c_cnt_is_less_27000 (0 color taking >10% of game icon, <27,000 pixels of the most frequent color present in icon).
100% recall indicating 100% of all the game icons with high rating were correctly labled by the Random Forest classifier. 
F1 score of 85%, measuring test's accuracy as weighted harmonic mean of precision and recall. Overall, the Random Forest Classifier is good at recognizing game with high rating.

Mean AUC Score:
Mean AUC score value of 0.48 indicates a mediocre classifier, being able to distinguish between highly rated games versus low rated games. 
