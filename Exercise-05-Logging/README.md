 - - -
Previous Exercise: [Exercise 4 - Order New Items](../Exercise-04-Order-New-Items) Next Exercise: [Exercise 6 - Comments and Ratings Backend](../Exercise-06-Comments-and-Ratings-Backend)

[Back to the Overview](../README.md)
- - - -
# Exercise 05 - Logging

## Why is logging important?
- No debugging of microservices in production.
- Debug port is closed by default.
- Applications must be SOX-compliant - immutable.
- We may have multiple instances so it may be difficult to target/troubleshoot specific instances.

We want to be able to look back in time, identify corresponding requests, which version of software was running at that time, which methods were being called etc.

The logs we collect are only useful if they can be analysed and visualised easily. It is helpful toto be able to collect logs in a single location and preferably in a common format.

In this exercise, you will learn how you as an application developer or a dev ops engineer can visualize the application logs provided by default via Cloud Foundry ELK stack which provides elastic search, logstadsh (data processor and enrichment of logs) and Kibana. This is a good combination to store, search and visualise log entries.

## 1. Review Logging Configuration and Code

In Exercise 4, we added the backend serivce calls to our wishlist application. As part of this exercise, we included the logging configuration and code to avoid having to build and redeploy the application again just to include the logging. 

1. In your Web IDE Full-stack open mta.yaml.
2. Under the srv module, nocite how we have already got the logging level set to `info` using the property:
```
    properties: 
      SET_LOGGING_LEVEL: '{com.company.furnitureshop: INFO}'    
```
2. Next, open `BackendService.java` under  `srv\src\main\java\com\company\furnitureshop\`. 
3. Notice the info logging entries, for example:
```
logger.info("Class:BackendService - now in @Query getProducts()");
```

![Service Bindings](images/Exercise3_1b_backend_service.JPG)

There is no need to change any code. We will need to bind an instance of the application-logs service in the next step.

## 2. Create and Bind a Service of application-logs
We will need to create and bind an instance of the application logging service to our application.
1. In the SAP Cloud PLatform Cockpit, go to your _Space-your space-applications-your application_ (srv).
2. From the application overview, click _Service Bindings_ on the left menu.
3. Click _Bind Service_.

![New Binding](images/Exercise3_2_service_bindings.JPG)

4. In the _Bind Service_ wizard, for _Choose Service Type_ select `Service from the catalog`.

![Service Type](images/Exercise3_3_service_bindings.JPG)

5. Click _Next_.
6. Search for `Application Logging`, select it.

![application logging](images/Exercise3_4_service_bindings.JPG)

7. Click _Next_.
8. For _Plan_ select `lite`.

![plan lite](images/Exercise3_5_service_bindings.JPG)

9. Click _Next_.
10. For _Parameters_ leave everything blank.
11. Click _Next_.
12. For _Instance Name_, enter `furniture_shop_logging`.

![instance name](images/Exercise3_6_service_bindings.JPG)

13. Click _Finish_.
14. Your Service Bindings should now include `furniture_shop_logging`.

![bindings list](images/Exercise3_7_service_bindings.JPG)

15. From the _Overview_ for your application restart your application.

## 3. Generate, and View Logs in Kibana
In this step, we will explore how easy it is to view and analyze your logs using the Kibana Dashboard. An alternative would be to view the application logs in the cockpit or using the Cloud Foundry command line tools, ie `cf logs application name --recent`. 

1. In order to collect new logs after binding the Application Logging instance to the `srv` application you will need to run the application once to generate the logs. Open the wishlist application in your browser and view a few products and their backend product details.
2. Return to the SAP Cloud Platform Cockpit.
3. Click _Logs_ on the left menu.

![Logs Menu](images/Exercise3_8_logging.JPG)

4. Click the _Open Kibana Dashboard_ button.
5. Log in user your SAP Cloud Platform User and Password.
6. Lets take a look at the different dashboards within Kibana.
   - _Overview_
     This shows the organization(s), space(s) of which you are a member (you        only see those logs). You can filter by organization or space. 
   - _Usage_ 
     To check usage which endpoints are called how often.
   - _Performance and Quality_
     Analyze request timeline further.
   - _Requests and Logs_
     Helps you to view, search and analyze the actual log messages.
     
![Requests and logs](images/Exercise3_15_all_logging.JPG)

7. We will start by changing a few settings. Click the configuration on the top right to set the timeline (last 15 minutes, current day etc) and enable autorefresh.
8. Next, Click _Requests and Logs_.
9. In the requests list, you can filter out unwanted requests using the mignifying glass(-) button when you hover over an item (so you can filter for a specific component or log level).

![Filter out](images/Exercise3_19_filter_out.JPG)

10. You can also add columns to the display. Expand a request in the list and scroll down to view the attributes of that request. Hover your mouse over the attribute of interest and click the _Toggle Colum in Table_ button to add that attribute to the column view.

![Toggle Column](images/Exercise3_11_toggle%20column1.JPG)

11. The column is now added to the view:

![Toggle Column](images/Exercise3_12_toggle%20column2.JPG)

12. You can add filters by correlation id to group together the logs for that correlation id. This will filter the Requests list and Application Log list for the correlation id. 

![Correlation ID](images/Exercise3_18_filter_correlation_id.JPG)

13. To use the same filters across other dashboards you need to first pin them. Hover over the filter and click the _Pin_ icon.

![Pin filter](images/Exercise3_13_pin%20filter.JPG)

14. In the _Application Logs_ pane, select any entry and click the arrow in the table to axpand that entry.

![Expand](images/Exercise3_16_application_logs_expand.JPG)

15. You can switch between the _table_ and _JSON_ view using the tabs. Click the JSON tab to view the expanded application log entry in JSON format. 

![Expand](images/Exercise3_16a_application_logs_JSON.JPG)

This concludes our brief introduction to application logging and how they are processed, enriched and visualised using Kibana. 

- - - -
© 2018 SAP SE
- - - -
Previous Exercise: [Exercise 4 - Order New Items](../Exercise-04-Order-New-Items) Next Exercise: [Exercise 6 - Comments and Ratings Backend](../Exercise-06-Comments-and-Ratings-Backend)

[Back to the Overview](../README.md)
