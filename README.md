Mangopay SDK
=================================================
MangopaySDK is a Java client library to work with
[Mangopay REST API](http://docs.mangopay.com/api-references/).


Compatibility Note
-------------------------------------------------
Since v1.0.6 of this SDK, you must be using at least v2.01 of the API ([more information about the changes required](https://docs.mangopay.com/api-v2-01-overview/))


Installation
-------------------------------------------------
SDK has been written in Java 7. It depends only on a single external package:
[gson](http://code.google.com/p/google-gson/) 2.2.4.

The installation is as easy as downloading the two jar files and storing them
under any classpath/location that will be available for imports in your project:

- [mangopaysdk](https://github.com/MangoPay/mangopay2-java-sdk/raw/master/dist/mangopaysdk.jar)
- [gson](https://github.com/MangoPay/mangopay2-java-sdk/raw/master/lib/google-gson-2.2.4/gson-2.2.4.jar)


License
-------------------------------------------------
MangopaySDK is distributed under MIT license, see LICENSE file.


Unit Tests
-------------------------------------------------
JUnit tests are placed under
[tests directory](https://github.com/MangoPay/mangopay2-java-sdk/tree/master/test/com/mangopay).


Contacts
-------------------------------------------------
Report bugs or suggest features using
[issue tracker at GitHub](https://github.com/MangoPay/mangopay2-java-sdk).


Account creation
-------------------------------------------------
You can get yourself a [free sandbox account](https://www.mangopay.com/get-started/create-sandbox/) or sign up for a [production account](https://www.mangopay.com/get-started/submit-your-app/create-credentials/) (note that validation of your production account can take a few days, so think about doing it in advance of when you actually want to go live).


Configuration
-------------------------------------------------
Using the credential info from the signup process above, you should then set `api.Config.ClientId` to your Mangopay Client ID and `api.Config.ClientPassword` to your passphrase.

`api.Config.BaseUrl` is set to sandbox environment by default. To enable production
environment, set it to `https://api.mangopay.com`.

    import com.mangopay.MangoPayApi;

    // ...

    MangoPayApi api = new MangoPayApi();

    // configuration
    api.Config.ClientId = "your-client-id";
    api.Config.ClientPassword = "your-client-password";
    //api.Config.BaseUrl = "https://api.mangopay.com";

    // call some API methods...
    List<User> users = api.Users.getAll();


Sample usage
-------------------------------------------------

    import com.mangopay.MangoPayApi;
    import com.mangopay.entities.User;
    import com.mangopay.entities.BankAccount;
    import com.mangopay.core.Pagination;
    import java.util.List;

    // ...

    MangoPayApi api = new MangoPayApi();

    // get some user by id
    User john = api.Users.get(someId);

    // change and update some of his data
    john.Tag += " - CHANGED";
    api.Users.update(john);

    // get all users (with pagination)
    Pagination pagination = new Pagination(1, 8); // get 1st page, 8 items per page
    List<User> users = api.Users.getAll(pagination);

    // get his bank accounts
    pagination = new Pagination(2, 10); // get 2nd page, 10 items per page
    List<BankAccount> accounts = api.Users.getBankAccounts(john.Id, pagination);
