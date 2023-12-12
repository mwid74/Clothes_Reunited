# Clothes_Reunited
#### Video Demo:  <https://youtu.be/Mh8TYxp0T9o>
#### Description:A web application for finding lost clothes.

I noticed, walking around our neighbourhood (I live in London, UK) that people often drop things, mainly items of clothing, but also children’s toys and other stuff. I thought it might be interesting to create an app that allowed local people, when they found an item, to take a picture of it, and upload it to the webapp, with a brief description of the object and where it was found. Other local people could log onto the website, scroll through the results, and with some luck, perhaps find that item they dropped in the streets a few days before. The website would have two pages therefore – a home page for displaying the items, and a register page for uploading items and photos. It would be difficult to identify an item with no photo, so I could not let someone upload a form without a photo. 

Creating this app used many of the skills I learned in the CS50 course (I had no previous computing experience to speak of). I mainly drew on the week 9 Flask, html and SQL stuff we had learnt. 

The first thing I did was draw out on paper exactly what I expected my app to do. I divided the task into different stages: 

1.	Design a basic html home page. 
2.	Create the SQL database for storing data about clothes.
3.	Write the flask application for loading the pages (a home page and a page for registering found items)
4.	Write the code for accessing the SQL and displaying it on the page.
5.	Write the code for uploading and displaying images.
6.	Finalise the design for the webapp.

This is more or less the plan I followed, and these are the difficulties I encountered. 

### Index.html
I used Bootstrap for this, and found the documentation reasonably straightforward. After looking at various options, I found an existing webpage layout that I thought would work and then I just copied that html, and then gradually stripped out most elements I didn’t want. Index.html now contains jinja script which extends the layout from the templates page, but actually I tidied all that up later. Initially all the code was in the index page. I took a navbar from the Bootstrap page and adapted it.  Then comes the main part of the code, which is adapted again from Week 9 class, creating the form for getting the sql. In earlier versions of the page,  I had a couple of columns and a grid pattern, and the SQL results appeared in a table. I looked up how to show my results without the table and it was quite simple. The claimed function was the most difficult part and I went through several versions which simply didn’t work. I wanted ‘claim’ to dynamically update the page when an object is claimed with a ‘claimed’ stamp on top of the item and the ‘claim’ button to disappear. After a lot of frustration, I decided to simplify the function, and I just had the claim function update the database and reload the page. The claimed status was then just in the html section and the forced reload meant the updated table values were always there.

### Clothes.db

This is the sql database with the table (items) where I store all the data about the items which are found. The table originally had a few different fields, such as ‘colour’ etc. but I simplified it. Initially, I ran the webpages with just text, thinking that the images part would be very difficult to implement. I later added the image column, and had most trouble with getting the right path to the images (partly due to a simple typo on my part). 

### App.py
Most of the code on this page originated with week 9 so it was simple enough. I actually cannibalised the code from the Finance Problem Set to write my app.py. Eventually, I looked in the flask documentation and found another way of initiating databases, which I tried out and it eventually worked. That is why my database setup does not use CS50 functions. 

### Layout.html
After I had my index.html page working okay, I took out a  lot of html from that and put it in the layout page, because I wanted to use the header and navbar for the register page. The comments at the top of layout.html are really notes to myself because I was getting confused with what all the lines were doing. As I eventually put a logo and had trouble positioning it, I divided the header into columns (30%, 40%, 30 %) to get it to work. Some other code was left over from the html template I stole in the footer, and I don’t really know what that is.

### Register. Html
This page extends the layout from template. Then it uses forms (similar to week 9 class finance problem). I did experiment with using other code to submit the forms, but it didn’t work, so I went back to basics. The big difference with the week 9 of course is the addition of the image upload, and all the modal stuff for checking that an image has been uploaded before submitting. Early tests of my upload function saw that it was easy to fill my database with null values, missing photos etc. So that is why there is code there to check if the photo was uploaded before submitting, and ensuring that fields are filled in. 

### Static and Images and custom-styles.css
Images is inside the static file. This includes the test images for the website that are already on the page. 

I didn’t use much in my custom-styles css page. I use it for my repeating tile theme on the register page, and I also for the custom navbar, but in the end I reverted back to the code which is in line on the html files for this. It was really just for me to experiment with how css worked. 


### Problems

I decided to try to use the vs code on my computer to develop the project, and this little side project caused me a lot of problems. I didn’t really understand what I was doing and spent a long time trying to open folders on the WSL server which kept kicking me out and going back to local files. I found microsofts chat function (copilot) useful for asking questions about stuff I didn’t know. Once I had done that and installed everything, making the database was relatively simple, but then more problems. I couldn’t save the database in a database folder (as somewhere it was written I should). Eventually, however, it worked. Then my database table kept disappearing. Various problems like this. Originally, I was going to have a database with fields like ‘Colour’ and ‘Brand’ etc. But in the end, I just went for ‘description’. I figured that people don’t really want to identify the brand of a piece of dropped clothing, and also that the accompanying picture would explain everything. The location was important, however. I left the images to a later stage, as I wanted to first work on getting the website working without anything too complex. 

I had a lot of trouble with the ‘claimed’ function. I wanted to have a button you could press so that an item was ‘claimed’ so that people would not go looking for it. At first I tried a complicated javascript function which did not work, which was supposed to update the database if pressed with success (1) or otherwise, and this would trigger some css to stamp claimed above the item. It also had to remove the claim button. I fiddled with this for a long time, and then decided a simpler route: why not simply have claimed or unclaimed in a column in the sql and get the function to change that and print out that value at all times, rather than fetching some css. I still had a lot of problems but it was easier to figure out.  
