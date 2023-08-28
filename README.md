# Sentiment-Analysis-API

The goal of this project was to build an API that allows users to browse, search, rate, and review products. I used MongoDB for the noSQL database, and PyTorch for the sentiment analysis model.

The database design consisted of two data models: Product and Review. The Product model stored information such as the name, description, price, category, and image of each product. The Review model stored information such as the text, rating, date, and sentiment of each review. The sentiment was a numerical value between 1 and 5, indicating how positive or negative the review was. The reviews were embedded within the products, meaning that each product document contained an array of review subdocuments.


## Benefits of This Design:
Scalability: By separating reviews from product details, you can handle a large number of reviews without hitting any document size limits.
Flexibility: Allows for querying and updating reviews independently of products.
Efficiency: Can reduce duplication of data (e.g., product details in every review).

## How to Implement Queries:
To get a product with its reviews: You can perform a query on the products collection and then either use the embedded review references to look up detailed review information or perform a join with the reviews collection (using MongoDB's $lookup operator) based on the review IDs.

To get a review with its associated product: You can query the reviews collection by review ID and then look up the associated product by the product ID.


## Schema

### Products Collection:

    {
        "product": {
            "id": "AVqkIhwDv8e3D1O-lebb",
            "name": "All-New Fire HD 8 Tablet...",
            "asins": "B01AHB9CN2",
            "brand": "Amazon",
            "categories": ["Electronics", "Tablets"],
            "keys": "...",
            "manufacturer": "Amazon",
            "average_sentiment_score": 0.5
            "numReviews": 2
        },
        "reviews": [
          {
            "date": "2021-01-01",
            "id": "r000012",
            "sentiment_score": 0.7
          },
          {
            "date": "2021-02-01",
            "id": "r001342",
            "sentiment_score": 0.3
          }
        ]
    }

Product Document: Contains information about a product, including an array of references to reviews (with minimal information such as date and sentiment score). This could be placed in a products collection.



### Reviews Collection:

    {
          "id": "r000012",
          "productId": "AVqkIhwDv8e3D1O-lebb", // Reference to the product
          "date": "2017-01-13T00:00:00.000Z",
          "dateAdded": "2017-07-03T23:33:15Z",
          "dateSeen": ["2017-06-07T09:04:00.000Z", "2017-04-30T00:45:00.000Z"],
          "didPurchase": null,
          "doRecommend": true,
          "numHelpful": 0,
          "rating": 5,
          "sourceURLs": ["http://...", "http://..."],
          "text": "This product so far has not disappointed. My children love to use it and I like the ability to monitor control what content they see with ease.",
          "title": "Kindle",
          "userCity": null,
          "userProvince": null,
          "username": "Adapter",
          "sentimentScore": 4.7
    }


Review Document: Contains detailed information about a review, including a reference to the product ID it's associated with. This could be placed in a reviews collection.


## Conclusion:
This design makes sense for a system where you expect to have many reviews for each product and want to keep the system scalable and normalized. It aligns well with typical NoSQL design patterns and takes advantage of MongoDB's flexibility in handling complex data structures. Carefully designed indexes are still to be implemnted.
