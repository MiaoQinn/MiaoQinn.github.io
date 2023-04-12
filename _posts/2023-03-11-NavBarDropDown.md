---
title: "Solutions: Bootstrap 5 Navbar toggle/responsive dropdown(collapse) not working "
---

I have been working on my e-commerce website for a while and I recently tried to make it look nice on Iphone/Android by adding responsive toggle bar using bootstrap 5. After I added the Navbar toggler when I clicked the dropdown icon nothing happened. It took me 4 hours to finally figure out a solution and I hope this article can save you some trouble. 

Here is a Sample Code. 
```html
<nav class="navbar navbar-dark bg-dark navbar-expand-md">
    <a href="#" class="navbar-brand">DemoTech</a>
    <button class="navbar-toggler" data-toggle="collapse" data-target="#navbar">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="navbar-collapse collapse" id="navbar">
        <ul class="navbar-nav">
            <li class="nav-item"><a href="#" class="nav-link">Home</a></li>
            <li class="nav-item"><a href="#" class="nav-link">About</a></li>
            <li class="nav-item"><a href="#" class="nav-link">Contact</a></li>
        </ul>
    </div>
</nav>
```

## Solution 1: Bootstrap 5 syntax-- Use data-bs-*

If you are familiar with bootstrap 4  then you should notice that in bootstrap 5 it starts using  **data-bs-** instead of **data-**.  Change the **data-toggle** and **data-target** to **data-bs-toggle** and **data-bs-target** and see if it works. Try the following code: 

```html
<nav class="navbar navbar-dark bg-dark navbar-expand-md">
    <a href="#" class="navbar-brand">DemoTech</a>
    <button class="navbar-toggler" data-bs-toggle="collapse" data-bs-target="#navbar">
        <span class="navbar-toggler-icon"></span>
    </button>
    <div class="navbar-collapse collapse" id="navbar">
        <ul class="navbar-nav">
            <li class="nav-item"><a href="#" class="nav-link">Home</a></li>
            <li class="nav-item"><a href="#" class="nav-link">About</a></li>
            <li class="nav-item"><a href="#" class="nav-link">Contact</a></li>
        </ul>
    </div>
</nav>
```
[Demo](https://www.codeply.com/p/7plDNvBJnB)

## Solution 2: Import the correct CDN link from Bootstrap Homepage

Check your headings and see if you imported the correct CDN link. In order to see if you have imported the correct bootstrap files, right click on your local test page and select **View Page Source**. Click on your import-link and see if the javascript/css raw file appears. In my project the link looks like this:

```html
<!-- CSS only -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
<sciprt type="text/javascript" th:src="@{/webjars/jquery/jquery.min.js}" ></sciprt>
<!-- javascript only incuding popper.js -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-kenU1KFdBIe4zVF0s0G1M5b4hcpxyD9F7jL+jjXkk+Q2h455rYXK/7HAuoJl+0I4" crossorigin="anonymous"></script>
<!-- March 2023 -->
``` 
Just put it at your html's heading. 

Go to [Bootstrap 5 Homepage](https://getbootstrap.com/docs/5.0/getting-started/introduction/) and check for the latest link. 

## Solution 3: Use CDN links instead of Maven dependencies to import bootstrap files

In my case I imported the bootstrap file via Maven dependency using thymeleaf syntax like this:
```html
<link rel="stylesheet" type="text/css" th:href="@{/webjars/bootstrap/css/bootstrap.min.css}" />
<script type="text/javascript" th:src= "@{/webjars/bootstrap/js/bootstrap.min.js}"></script>
```
In my pom.xml file the dependency looks like this: 

```xml
<dependency>
	<groupId>org.webjars</groupId>
	<artifactId>bootstrap</artifactId>
	<version>5.2.3</version>
</dependency>
``` 
I tried clicking on the dropdown menu using the sample code and nothing happened. When I inspected the page source it indicated that I indeed imported the correct files using the correct path. But when I tried  using the CDN links it suddenly worked. I also tried other 5.x version of bootstrap even 4.x and none of them worked. 


Bottom line if you have stable internet access **ALWAYS** use CDN links to import bootstrap files. 

I hope this article helps! 

Happy Coding!
