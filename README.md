# Live Project
Here is were you can find more information about me and what I have accomplished as a developer.
## Introduction
For the past two weeks, I have had the privilege to work in an enviroment that was designed to be based off of a real development team in a company, developing a full scale MVC Web Application in C# using ASP.NET, and the Entity Framework, using Visual Studio. Me and my peers were assigned tasks (called stories) usually to add more functionality to the application, and to be kept track of and implemented in using version control. This project was organized and ran using Azure Devops to assign stories, and to have a workflow with the code we were making. This web application is for a theatre company that rents out their building for acting companies to use for a certian time, with their information being stored in a database that can be accessed from the website, that includes CRUD functionalities built in. Most of my stories revolved around the renting section of the web application, where you could see past, and present renting requests made by fictional companies, but there is also many other sections of the application that had other uses and different functionality. My assigned stories were mostly back-end work, but also had a good amount of front-end, all of varying degrees of difficulty. Over the two weeks sprint, I had the opportunity to work on other project management and team programming skills that I'm confident I will use again and again on future projects.

Below are descriptions of some of the stories i worked on, along with some code snippets of code I implemented. 
# Stories
* Character Limit Helper Method
* Create Accordian To Display All Rental Requests
* Sort Rental Requests and Hide Expired Rental Requests
* Rental Survey Notification
* Create Request Manager
* Seed Request Manager
* Easy Login Button

## Character Limit Helper Method
With this story, I was tasked with creating and implementing a method that could be used to limit the number of characters that are displayed in a speficied string, and display ellipses at the end of the string where the character limit hits. For example, "Software Development" would turn into "Softwar..." if the character limit was set to 7. This method had two parameters, the first was a string that was the content that was to be truncated, and an integer to represent how many characters are allowed before cutting off the string, and add the ellipses (...).


## Create Accordian To Display All Rental Requests
This story, I was tasked with changing a current web page that showed all rental requests in a table, to display the requests in a accordian instead, where clicking on the horizontal bars would reveal additional details about the rental request. This required some front-end work, and the use of Bootstrap to implement an accordian, while inserting the details into the required spots in the accordian.   


## Sort Rental Requests and Hide Expired Rental Requests
In this story, I was tasked to hav+e the web page sort and display the rental requests by start date in ascending order. As well as have expired rental requests be hidden after a week has passed since the end time of the request when the page is loaded, and make a button that toggle between showing expired and current rentals.


## Rental Survey Notification
I was then assigned to make a button in the rental request that would appear on the last day of the rental request, that would invite the user to fill in a rental survey, as well as have the option to click a link that said "Ignore Survey". This required adding a boolean property to the RentalRequest model named "IgnoreSurveyPrompt" that would be set to false by default. This new property should be set to true if the user declines to fill in the survey (if they click "Ignore Survey"), and if a week has passed from the end date of the rental request and the user has not taken any action (neither declined nor filled in the survey).


## Create Request Manager
After that I was assigned to create an admin for the Rental area called RequestManager that would have more access than a normal user would have. This required making a new model in the Rental area that extended from the User model, so it would inherit its properties, as well as adding two more unique properties to the RequestManager called "RejectedRequests", and "AcceptedRequests".


## Seed Request Manager
For this next story, I was asked to make it so everytime the webpage is loaded, an instance of RequestManager was seeded in the database for testing purposes. This required to create a seed method for RequestManager, and calling the method in the configuration file so that it loads everytime the web application is ran.


## Easy Login Button
This final story, I was tasked with making an easily accessible login button in the rental area, that logs the user in as a RequestManager when clicked if development/testing purposes are needed. A partial view was used to store the button for code reuseability, then rendered on the main layout page. Additionally, the button should only be displayed when the current user is not logged in. 
