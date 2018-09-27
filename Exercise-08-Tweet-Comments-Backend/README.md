- - - -
Previous Exercise: [Exercise 07 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) Next Exercise: [Exercise 09 - Autoscaling of Comments and Ratings](../Exercise-09-Autoscaling-of-Comments-and-Ratings)

[Back to the Overview](../README.md)
- - - -

# Exercise 08 - Tweet Comments Backend

Till now we have seen that Furniture Shop/Franck have published a 'Wishlist' of products that it/he wishes to carry. We also saw that loyal customers like Mary have access to the customer portal to provide ratings and comments on the wishlist to influence the shop's decision. If we now provide a mechanism to spread the word about these wishlist reviews to a broader audience, more customers would be able to provide their inputs via the portal. And based on this feedback, Franck can order for the highly rated items into his furniture store inventory.

To achieve this reach, we can send out a **tweet** on the Furniture Store's twitter account whenever a customer posts a review of any particular product. We will build `tweet_comments`- a _headless_ microservice, i.e. a microservice without any UI & directly consumable in other microservices, to realise this functionality.

As the communication between our application and Twitter needs to be aysnchronous, we will use a message-broker like RabbitMQ to provide the queueing capability. Once a customer posts a review, the comments are published to a RabbitMQ queue. We will then pick the same message from the queue and publish it to Twitter.

## Important - before we begin

In the upcoming sections, you will be required to clone the exercise content from a given git repository. In general, Node.js modules need to be built based on the requirement and cannot be easily templated. To explain relevant sections of the code, you will notice that certain parts/modules are commented. The exercises will guide you to uncomment individual pieces of code, while explaining the relevance of each piece and what it tries to achieve. Please take note that commenting/uncommenting will differ based on the type of file you are working with. Javascript files will consist of line comments "//" where as UI5/xml files might use block comments with "/*.. */" format. Please follow the instructions closely to have a smooth exercise experience.

### 1. Clone exercise content and code walkthrough

As a part of the previous exercise, we have cloned the content required for this exercise too.

If you have not done so, please follow the steps 1 to 4 mentioned [here](../Exercise-06-Comments-and-Ratings-Backend#1-clone-exercise-content-and-code-walkthrough)

We know that the cloned application consists of 3 modules - `ratings_backend`, `ratings_frontend` and `tweets_comments`. In this exercise, we will focus on the `ratings_frontend` module.

![Step Image](images/Exercise8_1-6_clone_project.png)

To start working on *Exercise 8*, the `tweet_comments` module, we will switch to `exercise-8` branch in git.

1. Using your Git Pane, click on `Discard All` (Discard all unstaged changes in the list) as shown in the picture below.
    ![Step Image](images/Exercise8_1-1_Git_discard_all.png)

2. In the confirmation dialog that appears, click on `Discard`.
    ![Step Image](images/Exercise8_1-2_Git_discard_confirmation.png)

3. Using your Git Pane, click on `+` (Create Local Branch) as shown in the picture below.

    ![Step Image](images/Exercise8_1-3_Git_pane.png)

4. In the popup that appears, select the source branch as `origin/exercise-8` and enter the branch name as `exercise-8` and click on **OK**.

    ![Step Image](images/Exercise8_1-4_create_local_branch.png)

5. Refer to the image below and ensure that you have successfully checked out branch `exercise-8`

    ![Step Image](images/Exercise8_1-5_branch_exercise.png)

Open the `tweets_comments` module and navigate to the `package.json` file which lists all the packages that your module depends on.

![Step Image](images/Exercise8_1-7_tweet_comments.png)

Note that the file contains dependencies on the following node/npm modules:

![Step Image](images/Exercise8_1-8_package_json.png)

 * `cfenv` - used to parse Cloud Foundry-provided environment variables

 * `amqplib` - used to make amqp clients for Node.js

 * `twit` - Twitter API Client for Node.j


### 2. Setup RabbitMQ producer in 'ratings_backend' module

1. Go to the `ratings_backend` module built in Exercise 6 and open the `route.js` file under `route` folder.

   ![Step Image](images/Exercise8_2-1_route_js.png)

2. Uncomment the `addToRabbitMQ' method - the producer which creates a channel and sends the review data from the ratings service to the RabbitMQ queue.

   Note: To uncomment, follow these steps:

   1. Select the commented code
   2. Right click mouse on the editor
   3. Select the 'Toggle Line Comment' option

   ![Step Image](images/Exercise8_2-2_rmq_producer.png)


### 3. Setup RabbitMQ consumer in 'tweet_comments' module

1. The entry point to `tweets_comments` module is the `app.js`. Open this file.

   ![Step Image](images/Exercise8_3-1_tweets_comments.png)

   Uncomment the consumer code in `app.js`. This piece creates a channel and reads message from the RabbitMQ queue. We then push this message i.e. in our case 'Reviews' to Twitter.

   Note: To uncomment, follow these steps:

     1. Select the commented code
     2. Right click mouse on the editor
     3. Select the 'Toggle Line Comment' option

   ![Step Image](images/Exercise8_3-2_rmq_consumer.png)


2. The keys to configure Twitter account are saved in `config.js` file under the `config` folder.

   ![Step Image](images/Exercise8_3-3_twitter_config.png)


### 4. Deploying the application and Test

In this section we will build and deploy the application that has been built in the above steps.

1. Right click on the **`product_ratings`** folder, go to `Build` and click **Build** as shown in the picture below.

   ![Step Image](images/Exercise8_4-1_app_build.png)

   Once the build is completed successfully, you will see a new folder created in your Web IDE's File Explorer with the name **`mta_archives`**.

2. Right-click on the generated .mtar file **`product_ratings`**, and go to Deploy &rarr; and click on **Deploy to SAP Cloud Platform** as shown in the picture below.

   ![Step Image](images/Exercise8_4-2_app_deploy.png)

3. In the popup that appears, please enter the following details and click _Deploy_.

   ![Step Image](images/Exercise8_4-3_cf_endpoints.png)

    ```
      Cloud Foundry API Endpoint: https://api.cf.eu10.hana.ondemand.com
      Organization: TechEd2018_OPP363
      Space: <select your space from the drop down list>
    ```

4. Once your application is deployed launch the url for ratings_frontend app. As `tweet_comments` is a headless service and is consumed by the `ratings` service.

5. Select a product from the list and navigate to the `Rate Item` tab. Give the product a rating and a comment and click on submit.

   ![Step Image](images/Exercise8_4-5_provide_rating.png)

   You can also check the review feeds for a particular product.

   ![Step Image](images/Exercise8_4-5_check_comments.png)

6. In your browser, go to this [twitter handle](https://twitter.com/sapfurnishop) to see your comment posted as a tweet.

   ![Step Image](images/Exercise8_4-6_review_tweet.png)


    Twitter handle URL: https://twitter.com/sapfurnishop

- - - -
© 2018 SAP SE
- - - -

Previous Exercise: [Exercise 07 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) Next Exercise: [Exercise 09 - Autoscaling of Comments and Ratings](../Exercise-09-Autoscaling-of-Comments-and-Ratings)

[Back to the Overview](../README.md)
