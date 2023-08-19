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
