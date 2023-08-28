# Sentiment-Analysis-API

The goal of this project was to build an API that allows users to browse, search, rate, and review products. I used MongoDB for the noSQL database, and PyTorch for the sentiment analysis model.

The database design consisted of two data models: Product and Review. The Product model stored information such as the name, description, price, category, and image of each product. The Review model stored information such as the text, rating, date, and sentiment of each review. The sentiment was a numerical value between 1 and 5, indicating how positive or negative the review was. The reviews were embedded within the products, meaning that each product document contained an array of review subdocuments.
