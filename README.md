# weatherforecast
weather forecast project 

Automation framework  explained:

In  Acceptance test folder 

create src – main , test ( subfolders)

In  Test -  Java, resources folder


In  Java folder -  all the java code will be placed 

Driver : WeatherforecastDriver.class  which contains project (weatherforecast) ) specific resuable methods like closedriver,opencustomerview,refreshpage,changeurl,login,takescreenshot,sleep,waittoappear
waitforloading,focusanelement,mousehoverpanel, getvalue, gettext,settext, setvalue, cleartext, etc can be placed
WebDriverFactory .class (final) : generic methods related to the driver  examples: getWebDriver, getChromeDriver, getPhantomDriver,  

hook :  hook has setup final class which contains generic methods that has to be executed for each scenario , 
 public final class Setup{
   static {
      
      // If the suite is stoped abruptly (JUNIT mode or a fail in jenkins) this will close the browsers)
      Runtime.getRuntime().addShutdownHook(new Thread(){
         
         @Override
         public void run(){
            tearDown();
         }
         
      });
   }
@Before – method to be executed for each scenario example 

public void before(Scenario scenario) throws IOException, InterruptedException {
   Weatherforecast = new WeatherforecastDriver(WebDriverFactory.getWebDriver(getBrowserTarget()));
     
   Setup.scenario = scenario;
}
  and @after with tearDown methods after execution of the scenario.
static public void tearDown(){
   WeatherforecastDriver.takeScreenshot(Setup.scenario);
   WeatherforecastDriver.closeDriver();
}

steps ( a folder for step definition specific to project  :  contains the class with the  stepdefinitions of the steps in cucumber feature file.


Util folder : “utilities” folder is constituted of various generics, constants, Readers and classes for implementing user defined exceptions. Each of the folders under utilities has got its own significance.

Dbconnector class : generic methods in the class, 
Class contains methods Dbconnector, closeconnector

  DataSetters – The folder incorporates the classes that implement the getters and setters of the test data fetched from the Excels. To lode multiple sets of Test data, we create ArrayLists.

DbTestingUtils :
Examples :  gettingDbvalue, GettingDbvalueInt, UpdateDb, GetDbArray, getDbContactHistory

LoginUtils: getPassword  i.e using filesystem 
Queries :  class with methods to assign query as per the required.

FunctionLibrary – The folder is constituted of the classes which contain functions and methods that can be shared and used amongst the multiple classes. Very often, we are suppose to perform certain procedures prior and aftermath to the actual test execution like login to the application, setting up environments, activities related to rolls, data manipulations, writing results, methods those generate pre/post-conditions to other methods. Since we tend to perform these activities for all or most of the test script. Thus it is always recommended to create a separate class for such activities instead of coding them repeatedly in each of the test script. 

TestingUtils.java – contians methods that can be shared between multiple classes.

UserRoles – The folder accommodates the classes that take care of the Role based access criteria if any for instinct users.
UserMapperUtils.java 
TestRunner java file :  which runs the feature files.

 In Resource folder :   chromedriver, featurefiles, environment properties


how to build the project :  


to build and start the jetty 
for build go to project folder weatherforecast  
1. mvn clean install 

To start jetty , go to test folder weatherforecastacceptance test  
2. mvn -p jetty install 


To run the project :

1.dbconnector.java :  change the environment in "src/test/resources/web/d01/environment.properties" to the environment we wanted to run

2.go to the selected environment properities (example d01) d01 environment properties file 

for deployed versions in specific environments like d01 : 

weatherforecast url=https://weatherforeastd01.com 
#cuw.http.url=http://localhost:10091

For testing locally : 
#cuw.http.url=https://weatherforecastd01.com
cuw.http.url=http://localhost:10091

make sure that localhost should be commented out.

3.go to acceptance test pom file example: weatherforecast acceptance-test
<properties>
        <runQATests>false</runQATests>
        <env>d01</env>
        <browser>PHANTOM</browser>
        <cucumber.version>1.1.5</cucumber.version>        
    </properties>

to run the specific feature file, select the webforecastcucumbertest file and click on run.


If the time is given , we can update the code with the reusable methods, coding standards will be maintained, automation framework will be completed, accessability can be done, cross browser testing, web services provided by api can also be automated .
