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
real-time collaboration between users. We aim to build upon current implementations of real-time collaboration and extend 
those implementations to provide additional features.

## Background
Real-time collaboration has been implemented as a feature in word processing software, such as Microsoft Word, Google Docs, and 
Pages. These applications provide a more professional and formal environment for document writing. Our project aims to provide
a similar environment geared towards social interaction. The mini-map feature is currently implemented in VS Code as a way to
show the user which part of the document they are currently viewing. Our goal is to implement this feature to show where the
other users are in the conversation as well as the user's relative position in the conversation. Current messaging 
applications follow a more rigid messaging format. Messages in a conversation are often presented in chronological order and 
are uneditable. Our application will strive to break from these conventions to provide a fully editable conversation where the
user can type wherever they choose.

## Tasks
This messaging application will allow users to create accounts to communicate
with each other. The accounts can be created using an email account or with
Google or Facebook authentication. When signed in, users can view and modify their
"conversations" with other users.

The base functionality of a conversation should mimic a real-time collaboration
word processor. Any changes being made to the conversation will be reflected in
real-time to all other users participating in the conversation. Text, images,
and gifs will be accepted as valid conversation inputs. The application will
support text styling options, such as bold, italics, underlines, etc. Conversation
content can also be locked by users so that a specific group of content cannot
be modified.

In addition to the word processing capabilities, there will be features to
supplement the messaging platform.  Users will be notified immediately when
other users modify a conversation in the same vein as text message
notifications. Upon re-entering a conversation, the user will be presented with
the changes made since the last time they were active. Users can manually view
the history of any excerpt to determine which user contributed each change to
the excerpt. An overview of the conversation that displays the positions of
other active users in the conversation will be placed in the corner of every
conversation.

Search functionality will also be provided in the application. Users will be
able to search through conversations for specific keywords and filter certain
parameters.

## Methods
We will research and use many different software development methodologies, tools, and technologies
in the process of building this system. Software development is an inherently volatile branch of
engineering, so we will need a workflow that is flexible enough to accomodate for any sudden shifts
in design. The Agile methodology would allow us to quickly write code, test it, and have it running
in our "production" environment. In addition to our weekly meetings with our supervisor, we will
have team meetings once a week to update each other on individual progress and share any
discoveries. Also, we will consider pair programming, where two programmers write code together at
one computer, as a potential technique for working collaboratively. When not working together in
person, we will communicate over Slack.

We plan to use an online Kanban board on GitHub to help organize our Agile workflow. The board will
be a space for us to put tasks and organize them into columns according to each task's progress.
GitHub will also be where we host our remote repositories for all of our source code and
documentation. GitHub features like organizations, pull requests, and issue tracking will help keep
our project organized.

Once code for a feature or bug fix is written by one team member (or two in the case of pair
programming), it will need to go through code review by at least one other team member. Testing will
also be an important step for validating new changes to any code base we have. Continuous
Integration/Continuous Deployment (CI/CD) pipelines will help in automating this process. Before any
pull request can get merged to our master branch in Git, it must be approved by at least one
reviewer and a pipeline must be run that will run a suite of tests to validate that there are no
breaking changes.

Since we are developing a complex software system, we will need to research technologies for each
component of the system. We need a scalable platform to run the server-side code, so cloud vendors
like Amazon Web Services or Google Cloud could be useful options for us. The concurrency and memory
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
