<a name="top"></a># Navigation

| Exercise | Link |
|---|---|
| Previous | [Exercise 6 - Comments and Ratings Backend](../Exercise-06-Comments-and-Ratings-Backend)
| Next | [Exercise 8 - Tweet Comments Backend](../Exercise-08-Tweet-Comments-Backend)
| Start | [Overview](../README.md)



## Table of Contents
1. [Overview](#Intro)
1. [Clone Exercise Content](#Step1)
1. [Setup the Products List View](#Step2)
1. [Setup the Product Details View](#Step3)
1. [Deploy Application](#Step4)
1. [Appendix](#Appendix)



# Exercise 7 - Comments and Ratings Frontend

Now that we have the backend application of the `Comments and Ratings` backend service in place, in this exercise we will build the front-end application i.e. furniture shop's customer portal. The portal will allow customers like Mary to browse the store's product catalogue and view the wishlist items that the store is planning to stock.

Architecturally, we can either choose to consume micro-services in a single UI via APIs or have every micro-service develop it's own UI and use composition patterns to bring the UIs together. We have chosen to develop independent UIs for each micro-service. Like we have done in previous UI modules, we will continue to use SAPUI5 as the technology of choice for front-end applications. We will now build the UI screens that will enable Mary to add ratings and comments on any product that Franck has uploaded to the wishlist.



<a name="Intro"></a>
## Overview
The customer portal will have two views.

1. Products List View - contains the Wish list items uploaded by the furniture shop(Franck) for its customers.

   ![Step Image](images/Exercise7_Overview_1.png)

1. Product Details View - contains the details of a selected product

    The Product Details View will have two tabs.

    * Tab 1: Details - showing the details and image of the selected product

      ![Step Image](images/Exercise7_Overview_2.png)

    * Tab 2: Rate Item - The logged in user/customer can provide ratings & comments, for a selected item from this tab.

      ![Step Image](images/Exercise7_Overview_3.png)

   There is also a review feed which shows all the comments for the selected product.

   ![Step Image](images/Exercise7_Overview_4.png)


## Important - Before We Begin

In the upcoming sections, you will be required to clone the exercise content from a given git repository. In general, Javascript modules need to be built based on the requirement and cannot be easily templated. To explain relevant sections of the code, you will notice that certain parts/modules are commented. The exercises will guide you to uncomment individual pieces of code, while explaining the relevance of each piece and what it tries to achieve. Please take note that commenting/uncommenting will differ based on the type of file you are working with. Javascript files will consist of line comments "//". Please follow the instructions closely to have a smooth exercise experience.



<a name="Step1"></a>
# 1. Clone Exercise Content

As a part of the previous exercise, we have cloned the content required for this exercise too.

If you have not done so, please follow the steps 1 to 4 mentioned [here](../Exercise-06-Comments-and-Ratings-Backend#1-clone-exercise-content-and-code-walkthrough)

We know that the cloned application consists of 3 modules - `ratings_backend`, `ratings_frontend` and `tweets_comments`. In this exercise, we will focus on the `ratings_frontend` module.

To start working on *Exercise 7*, the `ratings_frontend` module, we will switch to `exercise-7` branch in git.

1. Select the folder `cloud-cf-furnitureshop-product-ratings` in your Web IDE Files explorer and then using your Git Pane, click on `Discard All` (Discard all unstaged changes in the list) as shown in the picture below.

    ![Step Image](images/Exercise7_1-1_Git_discard_all.png)

1. In the confirmation dialog that appears, click on `Discard`.

    ![Step Image](images/Exercise7_1-2_Git_discard_confirmation.png)

1. Using your Git Pane, click on `+` (Create Local Branch) as shown in the picture below.

    ![Step Image](images/Exercise7_1-3_Git_pane.png)

1. In the popup that appears, select the source branch as `origin/exercise-7` and enter the branch name as `exercise-7` and click on **OK**.

    ![Step Image](images/Exercise7_1-4_create_local_branch.png)

1. Refer to the image below and ensure that you have successfully checked out branch `exercise-7`

    ![Step Image](images/Exercise7_1-5_branch_exercise.png)



<a name="Step2"></a>
# 2. Setup the Products List View

In this section, we will setup the view and controller for products list view - a view that shows the wishlist of products.


1. Using your Files explorer in Web IDE, open the `ratings_frontend` module and navigate to the **`products_list.view.xml`** file under the **view** folder as shown in the picture below.

    ![Step Image](images/Exercise7_2-1_prod_list_view.png)

1. Check the code under the **`<pages>`** tag. We see that a table `idProductsListTable` with three columns Product Id, Product Name and Average Rating is created.

    ![Step Image](images/Exercise7_2-2_prod_list_columns.png)

1. We also see that selecting a product from the list will call the event handler `onProductSelection`.

    ![Step Image](images/Exercise7_2-3_prod_list_select.png)

1. Let us check the corresponding controller for Product List. Open the **`products_list.controller`** file as shown in the picture below.

    ![Step Image](images/Exercise7_2-4_prod_list_controller.png)

1. Uncomment the following methods
    * **`getProductsList`** - Fetches the products list from ratings_backend app

    ![Step Image](images/Exercise7_2-5_get_prod_list.png)

    * **`onProductSelection`** - Event handler for table row selection

    ![Step Image](images/Exercise7_2-5_prod_list_select.png)

    Note: To uncomment, follow these steps:

    1. Select the commented code
    1. Use the mouse Right click
    1. Select the '*Toggle Line Comment*' option



<a name="Step3"></a>
# 3. Setup the Product Details View

In this section, we will setup the view and controller for product details view - a view that shows the details of a product and allows the logged in user to rate the product and add a review.

1. Open the **`product_details.view.xml`** file under the **view** folder as shown in the picture below.

    ![Step Image](images/Exercise7_3-1_prod_details.png)

1. Check the code under the **`<pages>`** tag.

    * We see that we create two tabs.

        * Details Tab - where the details of the selected product are displayed
        * Rating Tab - where the user can review the product and submit ratings

     ![Step Image](images/Exercise7_3-2_prod_details_tab.png)

    * Underneath the tabs, all the review comments for the selected product are shown.

     ![Step Image](images/Exercise7_3-2_prod_reviews.png)

1. Let us check the corresponding controller for Product Details. Open the **`products_details.controller`** file as shown in the picture below.

    ![Step Image](images/Exercise7_3-3_prod_details_controller.png)

1. Uncomment the following methods
   * **`setReviewFeed`** - fetches all the reviews for the selected product

    ![Step Image](images/Exercise7_3-4_set_prod_review.png)

   * **`onSubmitRatingButtonPress`** - saves the ratings/comments into the Postgres database. Triggers the calculation of average rating and send the same to HANA.

    ![Step Image](images/Exercise7_3-4_submit_review.png)

        Note: To uncomment, follow these steps:
        1. Select the commented code
        2. Use the mouse Right click
        3. Select the 'Toggle Line Comment' option



<a name="Step4"></a>
# 4. Deploying the Application

We will now build and deploy the application that has been built above. Please note that the build and deploy may take few minutes. Please use this deployment time to login to the Cloud cockpit and check the creation of backing service instances, service bindings and applications. The order mentioned in your `mta.yaml` file will be followed during the deployment. You can also keep an eye on the flow of the deployment by watching the console logs from Web IDE or using the CF CLI command - **`cf logs <app_name> --recent`**.

1. To ensure that you do not deploy an incorrect MTAR it is advisable to delete the `product_ratings` folder under *mta_archives* folder as shown in the picture below.

    ![Step Image](images/Exercise7_4-1_pr_folder_delete.png)

1. Using your Files explorer in Web IDE, right click on the **`cloud-cf-furnitureshop-product-ratings`** folder, go to Build &rarr; and click on **Build** as shown in the picture below.

    ![Step Image](images/Exercise7_4-2_app_build.png)

   Once the build is completed, you will see a new folder created in Files explorer with the name **`mta_archives`**.

1. Right click on the generated .mtar file **`product_ratings_1.0.0`**, and go to Deploy &rarr; and click on **Deploy to SAP Cloud Platform** as shown in the picture below.

    ![Step Image](images/Exercise7_4-3_app_deploy.png)

1. In the popup that appears, enter the following details and click on Deploy

    ![Step Image](images/Exercise7_4-4_app_endpoint.png)

    ```
    Cloud Foundry API Endpoint: https://api.cf.eu10.hana.ondemand.com
    Organization: TechEd2018_OPP363
    Space: <select your space from the drop down list>
    ```

1. Once your application is deployed launch the url for `ratings_frontend` app. Your app should look like shown in the [overview section](#overview).

1. Select a product and go to the `Rate Item` tab in the Product Details view.

1. Give the product a rating and comment and click on submit, as shown in the picture below.

    ![Step Image](images/Exercise7_4-7-1_rating_view.png)

    This will add a review to the product as show below.

    ![Step Image](images/Exercise7_4-7-2_comments_feed_view.png)



<a name="Appendix"></a>
# Appendix - Understanding the HTML5 application code
*Please note that this step is intended only to explain the SAPUI5 HTML application code.  You are not required to performed any changes to your code as a part of this step.*

When you create a SAP UI5 application using the SAP Web IDE, a file structure with all the relevant files are created such as *`style.css`*, *`i18n.properties`*, *`model.js`* etc.

![Step Image](images/Exercise7_Appendix.png)

Let us look at two files *`manifest.json`* and *`xs-app.json`* where you specify some crucial settings for the front end application.

## `manifest.json`

* ***Global Model***

    You have created models such as **`products`** in *`products_list.controller`*; and **`productDetails`** and **`userRatingModel`** in *`product_details.controller`*. These models are view specific, i.e. such models can only be accessed from the corresponding view and controller. To access models from any view, you can setup global models in the *`manifest.json`* file under the **`models`** section.

    You have used two global models in this app *`selectedProductModel`* and *`userInfo`*.

* ***UI App routing***

    You use a router mechanism to navigate between different UI screens. You define the routes for your views in the *`manifest.json`* file under the **`routing` &rarr; `routes`** section


## `xs-app.json`

* ***Backend routing***

    To forward our request sent from ratings_frontend app to the backend app, we define routes under the **`routes`** section inside *`xs-app.json`*


## Further Reading
* [Starting point for SAPUI5 and Fiori](https://sapui5.hana.ondemand.com/)
* [SAP UI5 Icon explorer](https://sapui5.hana.ondemand.com/test-resources/sap/m/demokit/iconExplorer/webapp/index.html#)
* [Github code repository](https://github.com/SAP/cloud-cf-furnitureshop-product-ratings)


<hr>
© 2018 SAP SE
<hr>


# Navigation

| Exercise | Link |
|---|---|
| Previous | [Exercise 6 - Comments and Ratings Backend](../Exercise-06-Comments-and-Ratings-Backend)
| Next | [Exercise 8 - Tweet Comments Backend](../Exercise-08-Tweet-Comments-Backend)
| Start | [Overview](../README.md)
