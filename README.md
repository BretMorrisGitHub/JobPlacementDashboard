# Live Project

## Introduction
For the past two weeks, I have had the privilege to work in an enviroment that was designed to be based off of a real development team in a company, developing a full scale MVC Web Application in C# using ASP.NET, and the Entity Framework, using Visual Studio. Me and my peers were assigned tasks (called stories) usually to add more functionality to the application, and to be kept track of and implemented in using version control. This project was organized and ran using Azure Devops to assign stories, and to have a workflow with the code we were making. This web application is for a theatre company that rents out their building for acting companies to use for a certian time, with their information being stored in a database that can be accessed from the website, that includes CRUD functionalities built in. Most of my stories revolved around the renting section of the web application, where you could see past, and present renting requests made by fictional companies, but there is also many other sections of the application that had other uses and different functionality. My assigned stories were mostly back-end work, but also had a good amount of front-end, all of varying degrees of difficulty. Over the two weeks sprint, I had the opportunity to work on other project management and team programming skills that I'm confident I will use again and again on future projects.

Below are descriptions of some of the stories I worked on, along with some code snippets of code I implemented. 
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

```C#
namespace TheatreCMS3.Helpers
{
    public class TextHelpers
    {
        public static string CharacterLimit(string content, int numbOfCharacters)
        {
            var truncated = content.Substring(0, numbOfCharacters) + "...";
            return truncated;
        }
    }
}
```

## Create Accordian To Display All Rental Requests
This story, I was tasked with changing a current web page that showed all rental requests in a table, to display the requests in an accordian instead, where clicking on the horizontal bars would reveal additional details about the rental request. This required some front-end work, and the use of Bootstrap to implement an accordian, while inserting the details into the required spots in the accordian.   

```C#
<div class="accordion" id="accordionExample_@item.RentalRequestID">
    <div class="card">
        <div class="card-header" id="heading_@item.RentalRequestID">
            <h2 class="mb-0">
                <button class="btn btn-link btn-block text-left" type="button" data-toggle="collapse" data-target="#collapse_@item.RentalRequestID" aria-expanded="true" aria-controls="collapse_@item.RentalRequestID">
                    @item.ContactPerson
                </button>
            </h2>
        </div>

        <div id="collapse_@item.RentalRequestID" class="collapse bg-dark" aria-labelledby="heading_@item.RentalRequestID" data-parent="#accordionExample_@item.RentalRequestID">
            <div class="card-body bg-light text-dark border border-danger">
                <p>Company: @item.Company</p><br />
                <p>Contact Person: @item.ContactPerson</p>
                <p>Time Remaining: @item.GetRentalDuration()</p>
            </div>
            <div class="border border-danger p-20 bg-light text-dark">
                <p>Start Time: @item.StartTime</p>
                <p>End Time: @item.EndTime</p>
                <p>Rental Code: @item.RentalCode</p><br />
                <p>Project Info: @item.ProjectInfo</p><br />
                <p>Accepted: @item.Accepted</p><br />
                <p>Contract Signed: @item.ContractSigned</p>
                <p>Ignore Survey Prompt: @item.IgnoreSurveyPrompt</p>

                @Html.ActionLink("Edit", "Edit", new { id = item.RentalRequestID })
                @Html.ActionLink("Details", "Details", new { id = item.RentalRequestID })
                @Html.ActionLink("Delete", "Delete", new { id = item.RentalRequestID })
            </div>
        </div>
    </div>
</div>
```

## Sort Rental Requests and Hide Expired Rental Requests
In this story, I was tasked to have the web page sort and display the rental requests by start date in ascending order. As well as have expired rental requests be hidden after a week has passed since the end time of the request when the page is loaded, and make a button that toggles between showing expired and current rentals.

```C#
<input id="Button1" type="button" value="Expired Rentals" onclick="switchVisible();" />

<br />
<div id="non-expired">
    @foreach (var item in Model.OrderBy(t => t.StartTime))
    {
        // Shows Non expired requests
        if (item.EndTime.AddDays(7) > DateTime.Now)
        {
            <div class="accordion" id="accordionExample_@item.RentalRequestID">
                <div class="card">
                    <div class="card-header" id="heading_@item.RentalRequestID">
                        <h2 class="mb-0">
                            <button class="btn btn-link btn-block text-left" type="button" data-toggle="collapse" data-target="#collapse_@item.RentalRequestID" aria-expanded="true" aria-controls="collapse_@item.RentalRequestID">
                                @item.ContactPerson
                            </button>
                        </h2>
                    </div>

                    <div id="collapse_@item.RentalRequestID" class="collapse bg-dark" aria-labelledby="heading_@item.RentalRequestID" data-parent="#accordionExample_@item.RentalRequestID">
                        <div class="card-body bg-light text-dark border border-danger">
                            <p>Company: @item.Company</p><br />
                            <p>Contact Person: @item.ContactPerson</p>
                            <p>Time Remaining: @item.GetRentalDuration()</p>
                        </div>
                        <div class="border border-danger p-20 bg-light text-dark">
                            <p>Start Time: @item.StartTime</p>
                            <p>End Time: @item.EndTime</p>
                            <p>Rental Code: @item.RentalCode</p><br />
                            <p>Project Info: @item.ProjectInfo</p><br />
                            <p>Accepted: @item.Accepted</p><br />
                            <p>Contract Signed: @item.ContractSigned</p>
                            <p>Ignore Survey Prompt: @item.IgnoreSurveyPrompt</p>

                            @Html.ActionLink("Edit", "Edit", new { id = item.RentalRequestID })
                            @Html.ActionLink("Details", "Details", new { id = item.RentalRequestID })
                            @Html.ActionLink("Delete", "Delete", new { id = item.RentalRequestID })
                        </div>
                    </div>
                </div>
            </div>
        }
    }
</div>

<div id="expired">
    @foreach (var item in Model.OrderBy(t => t.StartTime))
    {
        // Shows expired requests
        if (item.EndTime.AddDays(7) < DateTime.Now)
        {
            <div class="accordion" id="accordionExample_@item.RentalRequestID">
                <div class="card">
                    <div class="card-header" id="heading_@item.RentalRequestID">
                        <h2 class="mb-0">
                            <button class="btn btn-link btn-block text-left" type="button" data-toggle="collapse" data-target="#collapse_@item.RentalRequestID" aria-expanded="true" aria-controls="collapse_@item.RentalRequestID">
                                @item.ContactPerson
                            </button>
                        </h2>
                    </div>

                    <div id="collapse_@item.RentalRequestID" class="collapse bg-dark" aria-labelledby="heading_@item.RentalRequestID" data-parent="#accordionExample_@item.RentalRequestID">
                        <div class="card-body bg-light text-dark border border-danger">
                            <p>Company: @item.Company</p><br />
                            <p>Contact Person: @item.ContactPerson</p>
                            <p>Time Remaining: @item.GetRentalDuration()</p>
                        </div>
                        <div class="border border-danger p-20 bg-light text-dark">
                            <p>Start Time: @item.StartTime</p>
                            <p>End Time: @item.EndTime</p>
                            <p>Rental Code: @item.RentalCode</p><br />
                            <p>Project Info: @item.ProjectInfo</p><br />
                            <p>Accepted: @item.Accepted</p><br />
                            <p>Contract Signed: @item.ContractSigned</p>
                            <p>Ignore Survey Prompt: @item.IgnoreSurveyPrompt</p>

                            @Html.ActionLink("Edit", "Edit", new { id = item.RentalRequestID })
                            @Html.ActionLink("Details", "Details", new { id = item.RentalRequestID })
                            @Html.ActionLink("Delete", "Delete", new { id = item.RentalRequestID })
                        </div>
                    </div>
                </div>
            </div>
        }
    }
</div>

@Html.Partial("_LoginBtnRequestManager")
```

## Rental Survey Notification
I was then assigned to make a button in the rental request that would appear on the last day of the rental request, that would invite the user to fill in a rental survey, as well as have the option to click a link that said "Ignore Survey". This required adding a boolean property to the RentalRequest model named "IgnoreSurveyPrompt" that would be set to false by default. This new property should be set to true if the user declines to fill in the survey (if they click "Ignore Survey"), and if a week has passed from the end date of the rental request and the user has not taken any action (neither declined nor filled in the survey). This code snippet was then added in the 'non-expired' section, under the HTML action links.

```C#
<button class="btn bg-dark text-light">View Survey</button>
@if (item.EndTime.Date <= DateTime.Today && item.EndTime.AddDays(+7) > DateTime.Today && item.IgnoreSurveyPrompt == false)
{
    <button class="btn bg-dark text-light">Fill in Rental Survey</button>
}
@Html.ActionLink("IgnoreSurvey", "IgnoreSurvey", new { id = item.RentalRequestID })
```

## Create Request Manager
After that I was assigned to create an admin for the Rental area called RequestManager that would have more access than a normal user would have. This required making a new model in the Rental area that extended from the User model, so it would inherit its properties, as well as adding two more unique properties to the RequestManager called "RejectedRequests", and "AcceptedRequests".

```C#
namespace TheatreCMS3.Areas.Rent.Models
{
    public class RequestManager : ApplicationUser
    {
        public int RejectedRequests { get; set; }
        public int AcceptedRequests { get; set; }
    }
}
```

## Seed Request Manager
For this next story, I was asked to make it so everytime the webpage is loaded, an instance of RequestManager was seeded in the database for testing purposes. This required to create a seed method for RequestManager, and calling the method in the configuration file so that it loads everytime the web application is ran.

```C#
public class RequestManager : ApplicationUser
    {
        public int RejectedRequests { get; set; }
        public int AcceptedRequests { get; set; }

        public static void SeedRequestManager(ApplicationDbContext context)
        {
            var roleManager = new RoleManager<IdentityRole>(new RoleStore<IdentityRole>(context));
            var roleUserManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(context));

            if (!roleManager.RoleExists("RentalManager"))
            {
                var requestRole = new IdentityRole();
                requestRole.Name = "RentalManager";
                roleManager.Create(requestRole);

                var rentalManager = new RequestManager
                {
                    UserName = "RentalManager",
                    Email = "RentalManager@gmail.com",
                };

                string password = "Password123!";
                var requestManagerResult = roleUserManager.Create(rentalManager, password);

                if (requestManagerResult.Succeeded)
                {
                    roleUserManager.AddToRole(rentalManager.Id, "RentalManager");
                }
            }
        }
    }
```

## Easy Login Button
This final story, I was tasked with making an easily accessible login button in the rental area, that logs the user in as a RequestManager when clicked if development/testing purposes are needed. A partial view was used to store the button for code reuseability, then rendered on the main layout page. Additionally, the button should only be displayed when the current user is not logged in. 

```C#
@if (!User.Identity.IsAuthenticated)
{
    {
        ViewBag.Title = "_LoginBtnRequestManager";
    }
    using (Html.BeginForm("RequestManagerLogin", "Account", new { area = "", ReturnUrl = Request.Url.AbsoluteUri }, FormMethod.Post))
    {
        @Html.AntiForgeryToken()
        <button type="submit" class="cms-bg-main cms-text-light bottom-right">Log in as Request Manager</button>
    }
}
```
