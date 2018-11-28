<a name="top"></a>
# Exercise 8 - Tweet Comments Backend

## Navigation

| Previous | | Next
|---|---|---|
| [Exercise 7 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) | [Overview](../README.md) | [Exercise 9 - Debugging](../Exercise-09-Debugging)



## Table of Contents

* [Overview](#user-content-intro)
* [Clone Exercise Content and Code Walkthrough](#user-content-step1)
* [Setup RabbitMQ Producer in `ratings_backend` Module](#user-content-step2)
* [Setup RabbitMQ Consumer in `tweet_comments` Module](#user-content-step3)
* [Setup the API Key For Posting Comments on Twitter](#user-content-step4)
* [Deploying the Application and Testing](#user-content-step5)



<a name="Intro"></a>
## Overview

Till now we have seen that Furniture Shop/Franck has published a 'Wishlist' of products that it/he wishes to carry. We also saw that loyal customers like Mary have access to the customer portal to provide ratings and comments on the wishlist to influence the shop's decision. If we now provide a mechanism to spread the word about these wishlist reviews to a broader audience, more customers would be able to provide their inputs via the portal. And based on this feedback, Franck can order for the highly rated items into his furniture store inventory.

To achieve this reach, we can send out a **tweet** on the Furniture Store's twitter account whenever a customer posts a review of any particular product. We will build `tweet_comments`- a _headless_ micro-service, i.e. a micro-service without any UI & directly consumable in other micro-services, to realise this functionality.

As the communication between our application and Twitter needs to be asynchronous, we will use a message-broker like RabbitMQ to provide the queueing capability. Once a customer posts a review, the comments are published to a RabbitMQ queue. We will then pick the same message from the queue and publish it to Twitter.


## Important - Before we Begin

In the upcoming sections, you will be required to clone the exercise content from a given git repository. In general, NodeJS modules need to be built based on the requirement and cannot be easily templated. To explain relevant sections of the code, you will notice that certain parts/modules are commented. The exercises will guide you to uncomment individual pieces of code, while explaining the relevance of each piece and what it tries to achieve. Please take note that commenting/uncommenting will differ based on the type of file you are working with. Javascript files will consist of line comments "//". Please follow the instructions closely to have a smooth exercise experience.

[Top](#Top)


<a name="Step1"></a>
# 1. Clone Exercise Content and Code Walkthrough

As a part of the previous exercise, we have cloned the content required for this exercise too.

If you have not done so, please follow the steps 1 to 4 mentioned [here](../Exercise-06-Comments-and-Ratings-Backend#1-clone-exercise-content-and-code-walkthrough)

We know that the cloned application consists of 3 modules - `ratings_backend`, `ratings_frontend` and `tweets_comments`. In this exercise, we will focus on the `ratings_frontend` module.

![Step Image](images/Exercise8_1-6_clone_project.png)

To start working on *Exercise 8*, the `tweet_comments` module, we will switch to `exercise-8` branch in git.

1. Select the folder `cloud-cf-furnitureshop-product-ratings` in your Web IDE Files explorer and then using your Git Pane, click on `Discard All` (Discard all unstaged changes in the list) as shown in the picture below.

    ![Step Image](images/Exercise8_1-1_Git_discard_all.png)

2. In the confirmation dialog that appears, click on `Discard`.

    ![Step Image](images/Exercise8_1-2_Git_discard_confirmation.png)

3. Using your Git Pane, click on `+` (Create Local Branch) as shown in the picture below.

    ![Step Image](images/Exercise8_1-3_Git_pane.png)

4. In the popup that appears, select the source branch as `origin/exercise-8` and enter the branch name as `exercise-8` and click on **Create**.

    ![Step Image](images/Exercise8_1-4_create_local_branch.png)

5. Refer to the image below and ensure that you have successfully checked out branch `exercise-8`

    ![Step Image](images/Exercise8_1-5_branch_exercise.png)

Open the `tweets_comments` module and navigate to the `package.json` file which lists all the packages that your module depends on.

![Step Image](images/Exercise8_1-7_tweet_comments.png)

Note that the file contains dependencies on the following node/npm modules:

![Step Image](images/Exercise8_1-8_package_json.png)

 * `cfenv` - used to parse Cloud Foundry-provided environment variables
 * `amqplib` - used to make amqp clients for NodeJS
 * `twit` - Twitter API Client for Node.j

[Top](#Top)



<a name="Step2"></a>
# 2. Setup RabbitMQ Producer in `ratings_backend` Module

1. Go to the `ratings_backend` module built in Exercise 6 and open the `route.js` file under `route` folder.

    ![Step Image](images/Exercise8_2-1_route_js.png)

1. Uncomment the rabbitmq libraries highlighted in the image.

    ![Step Image](images/Exercise8_2-3_rmq_libs.png)

    Note: To uncomment this code, delete only the first two `//` slash characters at the start of the line

1. Uncomment the `addToRabbitMQ` method - the producer which creates a channel and sends the review data from the ratings service to the RabbitMQ queue.

    ![Step Image](images/Exercise8_2-3_rmq_producer.png)

1. Uncomment the `addToRabbitMQ` method call.

    ![Step Image](images/Exercise8_2-4_rmq_method_call.png)

[Top](#Top)



<a name="Step3"></a>
# 3. Setup RabbitMQ Consumer in `tweet_comments` Module

1. The entry point to `tweets_comments` module is the `app.js`. Open this file.

    ![Step Image](images/Exercise8_3-1_tweets_comments.png)

1. Uncomment the consumer code in `app.js`. This piece creates a channel and reads message from the RabbitMQ queue. We then push this message i.e. in our case 'Reviews' to Twitter.

    ![Step Image](images/Exercise8_3-2_rmq_consumer.png)

[Top](#Top)



<a name="Step4"></a>
# 4. Setup the API Key For Posting Comments on Twitter

In this section we will go over the configuration steps required to post the review comments on twitter. A Twitter account activated for development provides a set of access keys that can be used by an application to securely connect to twitter. As a part of this exercise, we will be using the API Keys to this [twitter handle](https://twitter.com/sapfurnishop). Since these keys are sensitive, we must gain access to them in a secure manner.

1. Export (download) the `twitterkey.zip` file as shown in the picture below.

    ![Step Image](images/Exercise8_4-1_twitter_zip.png)

1. Extract the archive as shown in the picture below.  The ZIP file password is *Welcome18*.

    ![Step Image](images/Exercise8_4-2_twitter_zip_extract.png)

1. While extracting, you will be prompted to enter a password. Please ask the presenters for the archive's password and continue extracting `twitterkey.zip`

    ![Step Image](images/Exercise8_4-3_twitter_zip_pass.png)

    Once you've successfully extracted the archive, you should see the `config.json` file.

1. Right click on the extracted file - `config.json`, click on the *Edit* option and copy the entire content of the file.

    ![Step Image](images/Exercise8_4-4_twitter_config.png)

1. In you Web IDE, open *tweet_comments -> config ->* `config.js` and paste the content copied in the previous step.

    ![Step Image](images/Exercise8_4-5_twitter_config.png)

[Top](#Top)




<a name="Step5"></a>
# 5. Deploying the Application and Testing

We will now build and deploy the application that has been built above. Please note that the build and deploy may take few minutes. Please use this deployment time to login to the Cloud cockpit and check the creation of backing service instances, service bindings and applications. The order mentioned in your `mta.yaml` file will be followed during the deployment. You can also keep an eye on the flow of the deployment by watching the console logs from Web IDE or using the CF CLI command - **`cf logs <app name> --recent`**.

1.  To ensure that you do not deploy an incorrect MTAR it is advisable to delete the `product_ratings` folder under *mta_archives* folder as shown in the picture below.

    ![Step Image](images/Exercise8_5-1_pr_folder_delete.png)

1. Right click on the **`cloud-cf-furnitureshop-product-ratings`** folder, go to `Build` and click **Build** as shown in the picture below.

    ![Step Image](images/Exercise8_5-2_app_build.png)

   Once the build is completed successfully, you will see a new folder created in your Web IDE's File Explorer with the name **`mta_archives`**.

1. Right-click on the generated .mtar file **`product_ratings_1.0.0`**, and go to Deploy &rarr; and click on **Deploy to SAP Cloud Platform** as shown in the picture below.

    ![Step Image](images/Exercise8_5-3_app_deploy.png)

1. In the popup that appears, please enter the following details and click _Deploy_.

    ![Step Image](images/Exercise8_5-4_cf_endpoints.png)

    ```
      Cloud Foundry API Endpoint: https://api.cf.eu10.hana.ondemand.com
      Organization: TechEd2018_OPP363
      Space: <select your space from the drop down list>
    ```

1. Once your application is deployed launch the url for ratings_frontend app.  `tweet_comments` is a headless service (I.E. it has no user interface) is and is consumed by the `ratings` service.

1. Select a product from the list and navigate to the `Rate Item` tab. Give the product a rating and a comment and click on submit.

    ![Step Image](images/Exercise8_5-6_provide_rating.png)

   You can also check the review feeds for a particular product.

    ![Step Image](images/Exercise8_5-6_check_comments.png)

1. In your browser, go to this [twitter handle](https://twitter.com/sapfurnishop) to see your comment posted as a tweet.

    ![Step Image](images/Exercise8_5-7_review_tweet.png)

    Twitter handle URL: https://twitter.com/sapfurnishop

[Top](#Top)


<hr>
© 2018 SAP SE
<hr>


# Navigation

| Previous | | Next
|---|---|---|
| [Exercise 7 - Comments and Ratings Frontend](../Exercise-07-Comments-and-Ratings-Frontend) | [Overview](../README.md) | [Exercise 9 - Debugging](../Exercise-09-Debugging)

