## SCS 3253 020 - Machine Learning Term Project
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

### Data Preparation & Exploration
*insert ipynb code link*

### Model
The data set was trained with...
*insert ipynb code link*

### Results




