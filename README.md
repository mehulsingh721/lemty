# Lemty (a project inspired by [Klenty](https://www.klenty.com/))

It is a bulk emailing software which I created to help me in my business and to test my skills as a developer. Since I am a software developer not a UI Designer, its UI looks exactly Klenty but the code from back to front is purely mine.

## Project Description
### Features
Just like most bulk emailing softwares lemty's goal is to improve email deliveribility and convert prospects into clients. I have put a lot of hard work into this to include features like:

* Open Tracking
* Link Click Tracking
* Upload prospects from CSV.
* Add multiple Emails.
* Follow up emails.
* Campaign Reporting.
* Custom Email Intervals
* Preview and edit prospects before starting campaign.
* Set custom hours for sending emails.

### Tech Stack
To accommodate the this many features and still build as solid application I chose:
* Spring Boot (Java framework for building REST APIs)
* ReactJS (Frontend)
* Postgresql (Database)
* Quartz (Job Scheduling)
* Gmail API
* Heroku (Backend Server)
* Netlify (Frontend Server)

## How it works
### Sending Emails
When the campaign is started, the first thing it will do is loop through all the prospects in campaign and create jobs for each prospect in quartz database. __This job includes email data to be sent__

And after that first email job will be triggered. And when that job fires it will trigger next job __with a interval specified in settings__.
Just before a job is finished running data like, sent time step completed etc. will be updated and if there is a follow up email then that will be scheduled too.

### Tracking
At first, when I thought of tracking feaures, I was clueless about everything but as I progressed in the project, it was the easiest part.
1. #### Open Tracking
    You just simply attach a 1 x 1px image url to every email and when an email is opened there will be a __GET__ request to our server for the image with URL parameter of __Sent Email Id__ in our database and from that we can simply update our data.

2. #### Click Tracking
    When a user adds a link to email body, our server replaces that link with our tracking link and add url parameter named __URL__ with value of link in email body.(same for every link in the body). So when the link is clicked it will first go to our link and as soon as request is made, our server will redirect prospect to the user's link and our servver will update the data.

## Upcoming Features
* __Campaign Playbook__ : Automate the journey of prospects.
* __Reply Tracking__: Track replies for all emails sent from our softwares.
* __Google Sheets Integration__: Directly import prospects from google sheets.
* __CMS Integration__
* __Few UI Tewaks__

## Known Issues
* adding step to existing campaign does not create new jobs.
* campaign preview buggy.
* Server shut down after 30 min