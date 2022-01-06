# Solution
## The two services are running and registered

I have executed this commands to run and register the services

```
./gradlew :registratior:bootRun
./gradlew :accouts:bootRun
./gradlew :web:bootRun
```

Note: the registration service must be run before the others

The logs produced can be viewed as follows:

* Accounts:

![Accounts_log_p1](img/1-accounts_log_1.png)
![Accounts_log_p2](img/1-accounts_log_2.png)
	
* Web:
 ![Web_log](img/1-web_log.png)

Screenshots show they are initialized and resolving eureka endpoints via configuration.
Also each service is getting registered in Eureka.
## The service registration service has the two services registered

Now that the services are properly running, we can connect to localhost:1111 and check that the services are registered in Eureka
![Eureka dashboard](img/1-servicios_registrados.png)

It produces the following log (doesn't log anything about registered services):
![Eureka_log](img/1-eureka_log.png)

Now both services are registered in Eureka and appear correctly in the dashboard.
## A second account service is running in the port 4444 and it is registered
In `accounts/src/resources/application.yml`, change `port:2222` to `port:4444` in order to boot
a second account service there.

It successfully registers in Eureka:
![Second_account_registered](img/3-accounts_second_registered.png)
![Eureka_second_account_registered](img/3-eureka_2_accounts.png)

As it is shown, there are 2 `ACCOUNTS-SERVICE` available.

## What happens when you kill the service with port 2222. Can the web service provide information about the accounts? Why?

After killing the account service in 2222, the corresponding service disappears from Eureka:
![Eureka_dashboard_2222_killed](img/4-eureka_dashboard_kill.png)

It takes some time to reconfigure. After that, you can ask information to the web service about
the accounts without producing any `500: Internal Server Error` (it is caused while Eureka still redirects to the dead
service until it realises it is down).

This is what happens when asking for an account:
![Web_service_asked_account](img/4-web_account_asked.png)
