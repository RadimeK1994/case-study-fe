Hello team,

Firstly, I would like to thank you for this interesting task which I encountered with. It took me some time to solve out the issues which were in the code. Mainly, because I have met with some technologies like a Graphql, Next js. or MongoDB for the very first time, so I had to orient myself somehow in the code and get to my head how are all the things connected together. But frankly, it was one of te best javascript experience for me in a long time. I do not want to get back to online courses again :D. Thank you for that!

Nevertheless, I think I have found the most obvious problems and I have figured out how to fix them. I would like to start with setting up the environment and then I will move to bugs themselves. 

# Setting up the environment


I have cloned case studies from Github and installed all dependencies via npm. Then I was able to run the frontend on the port 3002 and backend on the port 3000. After that, I have noticed that there is some problem with the connection to the database - I got the error form Next and from console in the browser, so, then, I realized that the .env part wasn't in **README** just for fun. Honestly, it took me some time :D. Then I created the default variable on the frontend - API_URL. It worked fine! And then I have moved to the backend side and created .env with variables connected with MongoDB. Then I encountered with the first big issue.
Next js. give me an error message that told me - "the DB names cannot contain, in the charset, "." ". A was a little bit lost because I could not find out what I was doing badly. Then, after I had connected to the MongoDB via Compass and googled for this error message, I have noticed that I have used this path - "hostname/dbname. So I realized that it is nonsense. DB name is the only radim_kriz. So, the first problem solved.

# Fixing bugs

## Change the order of the links

I have started with the easiest one's bugs. I noticed that the order of the FilterLinks components is reversed compared to the reference version. So I have changed their order in the index.ts - in the part of the code (return] where is the content rendered. 

## Show up of the text in the active filter

I was able to see that the filter part **active** is not rendering the text *'active'* which should be there. So I started to investigate where is/are the text/texts stored. Then I found the JSON file named *default.json*, where I find the references like - title, h1, and so on. But there was no *active* reference in the footer part. So I have added active reference with the text **"Active"**. It is called by t() function which is, I suppose, part of **i18react**, at least I found something about this on Google. I have to admit that it was the first time I encountered something like that. 

## Newly inserted todo is not shown up

One of the main issues has occured. The new todo is not shown up in the application after the press of the enter. Firstly, I started investigating in the FE - **index**. I was thinking that possibly there is some function missing like an onPress, onKeyUp, or something which is triggering the user activity. But that idea was not confirmed. So I have moved, after some time looking around, to the backend side. I have understood that Graphql is something like a query language, API or Middleware which is used for the queries, over here for the communication with the MongoDB in this APP. And then the modified data by Graphql are processed/rendered by Next. I have noticed that the other two queries for deleting and switching reffer to the collection with the name - "Todo", but the Add mutation was referencing to the "Todi" collection, so it looks like a mistake for me. I have overwritten that and it has fixed the problem. 

## Remove button is not working

After previous experience with newly inserted todos. I have started to investigate the problem with the removing button in the mutation part. Then I have noticed that there is missing asynchronous pattern - async and wait. The program did not wait for the getting database, so it has to cause the problem. I have added the wait in front of the **getDB** function. Again, I got help from other mutations. 

## The counter

**Note:** Was figured before new todo and remove

I have noticed that the counter did not count the number of items (todos). I was able to find quite quickly the problem. When I took a look at the TodoCount component, I was able to get what the problem is. The property count is getting its number from the variable gettodo which has implemented the filter function. At that period of time it was getting the number from the filter named **ALL**, which has been not functioning yet, there was **no todos**. So I have changed that to ACTIVE filter and it started to do the trick. 

## The problem with the not showing up the todos in all filter

I was able to find that the filter is returning the todos by the filter function and conditions in getTodos. Active filter returns back **not checked todos** and Completed return back **checked todos**. But returning value from the ALL filter has boolean false. So I have changed that to **check.todo**. But, unfortunately, it was not a good way how to solve that, because it did not show the other todos/checked from Completed filter. So I have created the returning array with the checked and not checked variables because JavaScript doesn't support functions that return multiple values. However, you can wrap multiple values into an array or an object and return the array or the object.

## My idea of improvement countering

Then, I got the idea, how to improved the counter. I have added the conditions to the rendering of the Todocount component. Now, it shows the number of the items according to the currently active filter. Kindly, look at this.

## The timestamp is not right

I have noticed that the timestamp is created once and then it is provided the same one for all todos. Something was not correct, and because, I have supposed, that timestamp is somehow created by backend side of the application, I have moved to the adding Graphql mutation again. I have noticed that the variable with the function Date is out of the query/promise scope, so I decided to try to move it to the Promise scope and it has started to work. I have to admit that I am not sure, if I am currently able to explain that in more detail. I can say, it started to work. 

## Improvement of the readability 

I was not satisfied with the current format of the rendered timestamp, so I have added the spaces between the localtimestring and the localtimedate. It looks better for me. 

## Adding thank you message

I want to try to create my own component by the way how all components were created, so I made this silly thing, which you can find below that. :)