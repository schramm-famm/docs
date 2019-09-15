# Real-Time Collaboration Messaging Application
**Students**
* Thao-Tran Le-Phuong 100997443
* Honor Lopes 101008909
* Riley MacKinnon 100996542
* Igor Veselinovic 101011081

**Supervisor**

Cheryl Schramm

### Table of Contents
* [Objectives](#objectives)
* [Background](#background)
* [Tasks](#tasks)
* [Methods](#methods)
* [Timetable](#timetable)
* [Facilities](#facilities)
* [Degree Relevance](#degree-relevance)
	* [Thao-Tran Le-Phuong](#thao-tran-le-phuong)
	* [Honor Lopes](#honor-lopes)
	* [Riley MacKinnon](#riley-mackinnon)
	* [Igor Veselinovic](#igor-veselinovic)

## Objectives
The objective of this project is to develop a messaging platform that is formatted as a blank document that allows for 
real-time collaboration between users.

## Background
Real-time collaboration has been implemented as a feature in word processing software, such as Microsoft Word, Google Docs, and 
Pages. These applications provide a more professional and formal environment for document writing. Our project aims to provide
a similar environment geared towards social interaction.

## Tasks
* The application shall require users to have accounts.
  * Email, Display Name, Password
  * Multi-Factor Authentication
  * Google/Facebook authentication
* The application shall allow user input to be displayed to other authorized users in real-time.
* Users have "conversations" with each other where the conversation is updated in real-time with other's input
* Notifications will be when a user is typing/has typed within the conversation
* When a user re-enters a conversation, they'll be shown the changes made to the conversation since the last time they were 
there
* A mini-map can be displayed in the corner of the screen that shows an overview of the conversation and where other users are 
in it 
* Lock content
  * Essentially pinning an excerpt so that it can't be edited
  * Possibly lock position and content
* Formatting will be stored as XML
* Input images and animated gifs
* Highlight excerpt and get history of it
  * Which user typed what
* Search through conversations and users

## Methods
We will research and use many different software development methodologies, tools, and technologies
in the process of building this system. Software development is an inherently volatile branch of
engineering, so we will need a workflow that is flexible enough to accomodate for any sudden shifts
in design. Certain elements of the Agile approach to software development could benefit our
productivity. Collaborating with customers and end users won't be a concern for us, but since we
will be working with new technologies throughout the development process, we will constantly be
coming up with new ideas for how we want to implement any given feature.

An Agile workflow should allow us to quickly write code, test it, and have it running in our
"production" environment. In addition to our weekly meetings with our Supervisor, we will have
additional formal team meetings once a week to update each other on individual progress and share
any discoveries. Also, we will experiment with pair programming, where two programmers write code
together at one computer, as a potential technique for working collaboratively. When not working
together in person, we will use Slack for communication.

We plan to use an online Kanban board on GitHub to help organize our Agile workflow. The board will
be a space for us to put tasks and organize them into columns according to each task's progress.
GitHub will also be where we host our remote repositories for all of our source code and
documentation. GitHub features like organizations, pull requests, and issue tracking will help keep
our project organized.

Once code for a feature or bug fix is written by one team member, it will need to go through code
review by at least one other team member. In the case of pair programming, there will be constant
review from the paired programmer who isn't directly writing code, so this might affect that
workflow. Testing will be an important step for validating new changes to any code base we have.
Continuous Integration/Continuous Deployment (CI/CD) pipelines will greatly help in automated this
process. Before any pull request can get merged to our master branch in Git, a pipeline must be run
that will run a suite of tests to validate that there are no breaking changes.

Since we are developing a complex software system, we will need to research technologies for each
component of the system. We need a scalable platform to run the server-side code, so cloud vendors
like Amazon Web Services or Google Cloud could be useful options to us. The concurrency and memory
management features of Go make it suitable for our server-side needs, along with a relational
database management system using SQL. There are many framework options for the front-end of our web
application, including React, Angular, and Vue. WebAssembly is another front-end technology that we
are interested in incorporating into our web application.

## Timetable

## Facilities

## Degree Relevance

### Thao-Tran Le-Phuong

### Honor Lopes

### Riley MacKinnon

### Igor Veselinovic
