---
layout: post
title:  "Bob the Builder Project"
categories: blog assignment
permalink: posts/blog-post-bobthebuilder
author: Daniel Huang, Emily Jenks, Pei Xi Kwok, Vida Rusli
---

## About
This is a webapp based project that helps to automate a resume based on information that you provide. 
The webapp also provides job recommendations based on Indeed.

Link to [git repository](https://github.com/EGZJ17/pic16b-mnist-demo)

## Overview 

OVERVIEW OF RESUME BUILDER An online resume builder. It is a webapp developed to simplify the task of creating a resume for individuals, providing effective means of designing a professional looking resume. The webapp is especially designed for individuals who have a hard time creating their resume such as graduate students. This way, they will get a clear idea of the sections and information that should be included in a resume. The system is pretty simple without too much flexibility but can be expanded to include different templates, sections and so on. This project is user-friendly and requires minimum human intervention. Individuals just have to fill up a form that specifies questions from all required fields such as personal questions, educational, experience and skills. The answers provided by the users are stored and the system automatically generates a well structured resume.

OVERVIEW OF RECOMMENDATION SYSTEM The webapp also provides a site to input the preferred job title and location in order to generate the top job postings on [Indeed](https://www.indeed.com/). This way, the user can immediately start applying to job right after building their resume. 

The webapp is built on three main components: Indeed Scraper, Flask Webapp and HTML and CSS Files.

SOFTWARE REQUIREMENTS:
- Programming Language: Python
- User Interface: HTML and CSS

![bruindoe_resume.png]({{ site.baseurl }}/images/bruindoe_resume.png)

### Component 1: Indeed Scraper 
- 2 paragraphs 
- one code snippet
![indeed_scraper.png]({{ site.baseurl }}/images/indeed_scraper.png)

### Component 2: Flask Webapp

In this component, we will be talking about the Flask Webapp aspect of our project. In order for this webapp to work, we created an __init__.py in the directory. Then, we created a templates folder to store all html files for the different pages on our webapp. There is also a style.css and resume_style.css file in a separate static folder. First, we imported all the necessary packages. When the webapp is first launched by the user, it follows the command @app.route("/") and the main( ) function is called. After this, the function render_template (), which has been imported from Flask, is returned so that the main_better.html template is rendered. In other words, this means that when someone looks up the website, it will show the home page of the webapp, which displays instructions on how to use the webapp. Next, the @app.route("/about/") calls the function hello( ), which renders the about.html template. Basically, when the user clicks “About Us” on our website, the url adds “/about/” to the end and redirects the user to the about us page.

Now, let’s talk about how the filling out and generating the resume works. Now if the user selects “Form”, the @app.route("/form/") calls the ask( ) function. This is the page where the user fills out their information. In this function command we considered two methods; get and post. The get method is when the user first arrives to the form page. In the function ask( ), the form.html template is rendered when the user enters the page through the get method. On the other hand, the post method is when the user has already been to the form page and has filled out the information the form requests. In the function ask( ), if the post is the method, then we use a flask import function called redirect( ) in order to redirect the page to the resume command. Once the user fills out the information and is redirected, the @app.route("/resume/") calls the resume( ) function. In this function, we take the information that the user inputted and store it in a python variable in order to pass the parameters. The syntax for this is first_name=request.form[‘first_name’]. Once we store all the inputs, we return the function render_template (), which has been imported from Flask, so that the resume.html template is rendered. Since we are passing the parameters, we also need to pass the parameters through the render_template () function with the syntax “first_name= first_name”. then the resume.html template is rendered and now the user can view their resume on the webapp!

```python
from flask import Flask, g, render_template, request
from flask import redirect, url_for, abort

from bs4 import BeautifulSoup
import pandas as pd
import os
import requests

import io
import base64

app = Flask(__name__)

@app.route('/')
def main():
    """
    Loads template for main page
    """
    return render_template('main_better.html')

@app.route('/form/', methods=['POST', 'GET'])
def ask():
    """
    Loads page for user input
    """
    if request.method == 'GET':
        return render_template('form.html')
    else: 
        try:
            return redirect(url_for('resume'))
        except:
            return render_template('form.html', error=True) 

@app.route('/resume/', methods=['POST'])
def resume():
    """
    Loads information from user input into html template and outputs resume
    """
    first_name=request.form['first_name']
    last_name=request.form['last_name']
    location=request.form['location']
    phone=request.form['phone']
    email=request.form['email']

    school1=request.form['school1']
    school1startdate=request.form['school1startdate']
    school1enddate=request.form['school1enddate']
    school1GPA=request.form['school1GPA']
    school1Relevant_Courses=request.form['school1Relevant_Courses']

    company1=request.form['company1']
    company1position=request.form['company1position']
    company1startdate=request.form['company1startdate']
    company1enddate=request.form['company1enddate']
    company1experience1=request.form['company1experience1']
    company1experience2=request.form['company1experience2']

    company2=request.form['company2']
    company2position=request.form['company2position']
    company2startdate=request.form['company2startdate']
    company2enddate=request.form['company2enddate']
    company2experience1=request.form['company2experience1']
    company2experience2=request.form['company2experience2']

    Achievement1=request.form['Achievement1']
    Achievement1description1=request.form['Achievement1description1']

    languages=request.form['languages']
    technical_skills=request.form['technical_skills']
    interests=request.form['interests']

    return render_template('resume.html', first_name=first_name, last_name=last_name, location=location, phone=phone, email=email, 
    school1=school1, school1startdate=school1startdate, school1enddate=school1enddate, school1GPA=school1GPA, school1Relevant_Courses=school1Relevant_Courses, 
    company1=company1, company1position=company1position, company1startdate=company1startdate, company1enddate=company1enddate, company1experience1=company1experience1, company1experience2=company1experience2,
    company2=company2, company2position=company2position, company2startdate=company2startdate, company2enddate=company2enddate, company2experience1=company2experience1, company2experience2=company2experience2,
    Achievement1=Achievement1, Achievement1description1=Achievement1description1, 
    languages=languages, technical_skills=technical_skills, interests=interests)

@app.route('/indeed_test/', methods=['POST', 'GET'])
def submit():
    if request.method == 'GET':
        return render_template('indeed_test.html')
    else:
        user_job = request.form['job']
        user_location = request.form['location']
        user_job = user_job.replace(" ", "%20")
        user_location = user_location.replace(" ", "%20")
        current_url = f"https://www.indeed.com/jobs?q={user_job}&l={user_location}"

        return render_template('indeed_test.html', user_job=user_job, user_location=user_location, current_url=current_url)

@app.route('/about/')
def hello():
    return render_template('about.html')
```

![resume_builder.png]({{ site.baseurl }}/images/resume_builder.png)

### Component 3: HTML and CSS file
> HTML

HTML was used in creating the formatting for the website including the following subpages:
- about.html: about us page gives a brief introduction of what the webapp is for
- base.html: specifies the base URL and/or target for all relative URLs in a document. The <base> tag must have either an href or a target attribute present, or both. There can only be one single <base> element in a document, and it must be inside the <head> element.
- form.html: contains the code prompting for user input such as personal questions and education. These information will then be stored in different variables to be used in building the resume
- indeed_test.html: prompts for input desired job and location. It will then output the job recommendations generated by the indeed scraper
- main_better.html: represents the dominant content of the <body> of a document. The main content area consists of content that is directly related to or expands upon the central topic of a document, or the central functionality of an application.
- resume.html: provides a skeleton for our resume pdf. (This is assisted by the style1.css file instead of style.css)

```html
{% raw %}{% extends 'base.html' %}
<link href="{{ url_for('static', filename='resume_style.css') }}" rel='stylesheet' type='text/css'>

<div class="container">
  <div class="header">
    <div class="full-name">
      <span class="first-name">{{first_name}}</span>
      <span class="last-name">{{last_name}}</span>
    </div>
  <div class="contact-info">
    <span class="email">Email: </span>
    <span class="email-val">{{email}}</span>
    <span class="separator"></span>
    <span class="phone">Phone: </span>
    <span class="phone-val">{{phone}}</span>
    <span class="separator"></span>
    <span class="location">Location: </span>
    <span class="location">{{location}}</span>
  </div>
</div>

<div class="section">
  <div class="section__title">Education</div> 
    <div class="section__list">
      <div class="section__list-item">
        <div class="name">{{school1}}</div>
        <div class="text">{{school1startdate}}-{{school1enddate}}</div>
        <div class="text">{{school1GPA}}</div>
        <div class="text">{{school1Relevant_Courses}}</div>
      </div>
    </div>
</div>

<div class="section">
  <div class="section__title">Experience</div> 
    <div class="section__list">
      <div class="section__list-item">
        <div class="name">{{company1}}</div>
        <div class="text">{{company1position}}</div>
        <div class="text">{{company1startdate}}-{{company1enddate}}</div>
        <div class="text">{{company1experience1}}</div>
        <div class="text">{{company1experience2}}</div>
      </div>
      
      <div class="section__list-item">
        <div class="name">company2</div>
        <div class="text">{{company2position}}</div>
        <div class="text">{{company2startdate}}-{{company2enddate}}</div>
        <div class="text">{{company2experience1}}</div>
        <div class="text">{{company2experience2}}</div>
        </div>
      </div>
    </div>

<div class="section">
  <div class="section__title">Achievements</div> 
    <div class="section__list">
      <div class="section__list-item">
        <div class="name">{{Achievement1}}</div>
        <div class="text">{{Achievement1description1}}</div>
      </div>
    </div>
</div>

<div class="section">
  <div class="section__title">Skills</div>
  <div class="skills">
    <div class="skills__item">
      <div class="left"><div class="name">
      {{languages}}
        </div></div>
    </div> 
</div>
       <div class="skills__item">
           <div class="left"><div class="name">
            {{technical_skills}}</div></div>
         </div>
         
       </div>
     <div class="section">
     <div class="section__title">
       Interests
       </div>
       <div class="section__list">
         <div class="section__list-item">
            {{interests}}
          </div>
       </div>
     </div>
     </div>
  </div>
</div>
</div>
{% endblock %}{% endraw %}
```  
> CSS
- style.css: creates the style formatting for about.html, base.html, form.html, indeed_test.html, main_better.html
- resume_style.css: creates the style formatting for resume.html

![resume_form.png]({{ site.baseurl }}/images/resume_form.png)

## Concluding Remarks

Bob the Builder Project is designed a developed by a team of four UCLA undergraduates. The project objectives was to integrate web scraping and flask to design a "quick-and-easy" resume builder deployed through heroku. This resume would be able to help fellow undergraduates especially freshman and sophomores who are starting from scratch. 

The project was set to also include job and keyword recommendations through web scraping but the team decided to only implement job recommendations which was done through scraping Indeed as mentioned before. However, this program can be further developed to include it along with other creative aspects.

Some ideas to further develop the webapp is to allow users to choose different templates for the resume, check for punctuation, spelling and grammar mistakes or provide selections for user input. 

This project served its purpose in allowing the team to understand more about building a webapp from scratch! It was fun, frustrating at times but definitely fulfilling. That is it for our project. 

`print("Goodbye, World")`
