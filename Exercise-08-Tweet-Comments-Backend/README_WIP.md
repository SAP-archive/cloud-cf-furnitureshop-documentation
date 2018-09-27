- - - -
Previous Exercise: [Exercise 07 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) Next Exercise: [Exercise 09 - Autoscaling of Comments and Ratings](../Exercise-09-Autoscaling-of-Comments-and-Ratings)

[Back to the Overview](../README.md)
- - - -

# Exercise 08 - Tweet Comments Backend

Till now we have seen that Furniture Shop/Franck have published a 'Wishlist' of products that they wish to carry. We also saw that loyal customers like Mary have access to the customer portal to provide ratings and comments on the wishlist to influence the shop's decision. If we now provide a mechanism to spread the word about these wishlist reviews to a broader audience, more customers would be able to provide their inputs via the portal. And based on this feedback, Franck can order for the highly rated items into his furniture store inventory.

To achieve this reach, we can send out a **tweet** on the Furniture Store's twitter account whenever a customer posts a review of any particular product. We will build `tweet_comments`- a _headless_ microservice, i.e. a microservice without any UI & directly consumable in other microservices, to realise this functionality.

As the communication between our application and Twitter needs to be aysnchronous, we will use a message-broker like RabbitMQ to providing the queueing capability. Once customer posts a review, the comments are published to a RabbitMQ queue. We will then pick the same message from the queue and publish it to Twitter.

## Important - before we begin

In the upcoming sections, you will be required to clone the exercise content from a given git repository. In general, Node.js modules need to be built based on the requirement and cannot be easily templated. To explain relevant sections of the code, you will notice that certain parts/modules are commented. The exercises will guide you to uncomment individual pieces of code, while explaining the relevance of each piece and what it tries to achieve. Please take note that commenting/uncommenting will differ based on the type of file you are working with. Javascript files will consist of line comments "//" where as UI5/xml files might use block comments with "/*.. */" format. Please follow the instructions closely to have a smooth exercise experience.

### 1. Clone exercise content and code walkthrough

As a part of the previous exercise, we have cloned the content required for this exercise too.

If you have not done so, please follow the steps 1 to 4 mentioned [here](../Exercise4_Comments_and_Ratings_Backend/README.md#1-clone-exercise-content-and-code-walkthrough)

The cloned application consists of 3 modules - `ratings_backend`, `ratings_frontend` and `tweets_comments`. In this exercise, we will focus on the `tweets_comments` module.

![Step Image](images_1/Exercise8_1_clone_project.png)

Open the `tweets_comments` module and navigate to the `package.json` file which lists all the packages that your module depends on.

![Step Image](images_1/Exercise8_2_tweet_comments.png)

Note that the file contains dependencies on the following node/npm modules:

![Step Image](images_1/Exercise8_2_package_json.png)

 * `cfenv` - used to parse Cloud Foundry-provided environment variables

 * `amqplib` - used to make amqp clients for Node.js

 * `twit` - Twitter API Client for Node.j


### 2. Setup RabbitMQ producer in 'ratings_backend' module

1. Go to the `ratings_backend` module built in Exercise 6 and open the `route.js` file under `route` folder.

   ![Step Image](image_1/Exercise8_2-1_route_js.png)

2. Uncomment the `addToRabbitMQ' method - the producer which creates a channel and sends the review data from the ratings service to the RabbitMQ queue.

   Note: To uncomment, follow these steps:

   * Select the commented code
   * Right click mouse on the editor
   * Select the 'Toggle Line Comment' option

   ![Step Image](image_1/Exercise8_2-2_rmq_producer.png)


### 3. Setup RabbitMQ consumer in 'tweet_comments' module

1. The entry point to `tweets_comments` module is the `app.js`. Open this file.

   ![Step Image](images_1/Exercise8_3-1_tweets_comments.png)

   Uncomment the consumer code in `app.js`. This piece creates a channel and reads message from the RabbitMQ queue. We then push this message i.e. in our case 'Reviews' to Twitter.

   Note: To uncomment, follow these steps:

     * Select the commented code
     * Right click mouse on the editor
     * Select the 'Toggle Line Comment' option

   ![Step Image](images_1/Exercise8_3-2_rmq_consumer.png)


2. The keys to configure Twitter account are saved in `config.js` file under the `config` folder.

   ![Step Image](images_1/Exercise8_3-3_twitter_config.png)


### 4. Deploying the application and Test

In this section we will build and deploy the application that has been built in the above steps.

1. Using your File Explorer in Web IDE, rename the **`mta.yaml`** file to **`mta_exercise_5.yaml`** as shown in the picture below.

   ![Step Image](images/iExercise8_4-1_mta5_rename.png)

2. Rename the **`mta_exercise_6.yaml`** file to **`mta.yaml`** as shown in the picture below.

   ![Step Image](images_1/Exercise8_4-2_mta6_rename.png)

3. Right click on the **`product_ratings`** folder, go to `Build` and click **Build** as shown in the picture below.

   ![Step Image](images/Exercise8_4-3_app_build.png)

   Once the build is completed successfully, you will see a new folder created in your Web IDE's File Explorer with the name **`mta_archives`**.

4. Right-click on the generated .mtar file **`product_ratings`**, and go to Deploy &rarr; and click on **Deploy to SAP Cloud Platform** as shown in the picture below.

   ![Step Image](images_1/Exercise8_4-4_app_deploy.png)

5. In the popup that appears, please enter the following details and click _Deploy_.

   ![Step Image](images/Exercise8_4-5_cf_endpoints.png)

    ```
      Cloud Foundry API Endpoint: https://api.cf.eu10.hana.ondemand.com
      Organization: TechEd2018_OPP363
      Space: <select your space from the drop down list>
    ```

6. Once your application is deployed launch the url for ratings_frontend app. As `tweet_comments` is a headless service and is consumed by the `ratings` service.

7. Select a product from the list and navigate to the `Rate Item` tab. Give the product a rating and a comment and click on submit.

   ![Step Image](images_1/Exercise8_4-7_provide_rating.png)

   You can also check the review feeds for a particular product.

   ![Step Image](images)1/Exercise8_4-8_check_comments.png)

8. In your browser, go to this [twitter handle](https://twitter.com/sapfurnishop) to see your comment posted as a tweet.

   ![Step Image](images_1ß/Exercise8_4-9_review_tweet.png)


    Twitter handle URL: https://twitter.com/sapfurnishop

- - - -
© 2018 SAP SE
- - - -

Previous Exercise: [Exercise 07 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) Next Exercise: [Exercise 09 - Autoscaling of Comments and Ratings](../Exercise-09-Autoscaling-of-Comments-and-Ratings)

[Back to the Overview](../README.md)
