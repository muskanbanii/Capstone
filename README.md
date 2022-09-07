
# Anonymous Chat application 

Designing and implementing a web application of your own with Python and JavaScript.

Hey everyone this is Muskan Bani and for this CS50 web project, I desgined an anonymous chat application which allows the users to enter a **"ROOM NAME"** and a **"USERNAME"** and they are taken to the chat room. Later the user can share the **"ROOM NAME"** to someone and they can enter this room! They both will be able to chat in real time! 

#Why I chose this app?

I chose this application because I wanted to create a web application with rather simple UI and people can chat in real time! It was a fine project and I really enjoyed making it. Since most of us are introverts and we the introverts really wanted something that would preserve our idendity and at the same time we would be able to express ourselves more freely.

It would be an understatement to say that CS50's projects were challenging. Compared to the challenges presented by the instructors of this course, my previous web development experiences were nothing. Instead of spoon-feeding, I truly appreciate the spirit of pushing students to solve problems. Due to this course's thrown in the deep end approach, I have gained a deeper understanding of programming. I decided to work with technologies outside my comfort zone as part of my capstone project because the project should embody that same spirit. When I began the course, I knew nothing about Python or Django. As a result, I had to learn a new language, a new framework, how databases work, how websockets work, authentication, and so on. To remain in a state of discomfort and growth, this project was selected.

#Project distinctiveness and complexities:

There are many aspects of the project that make it unique. Among them is real-time chat using websockets, an upgraded web protocol. To make this possible, Django Channels was used. By using Django Channels, the server and client can maintain a constant connection without HTTP requests. Channel Layers is an optional feature in Django Channels that manages messaging and events through the database. As a result, the client does not have to refresh the page to receive and display the latest messages. In my opinion, the chat feature alone should satisfy the requirements for distinctiveness and complexity.

The project's frontend is built using Django's html templates. Bootstrap CSS library was also integrated to assist with styling, along with JavaScript.

## How to run application:


1. Install the requirememts 
```
pip install -r requirements.txt
```

2. Initialize the database with makemigrations, migrate, then create superuser.
```
py manage.py makemigrations
py manage.py migrate
py manage.py createsuperuser

```
3. Launch the Django server. If set up correctly, server will launch on http://127.0.0.1:8000/.
```
py manange.py runserver

```

## Files

1). In the folder called templates` we have:
```home.html``` 
which contains the code for the entering the username and room name. This has integrated css file in <style file>

```css
body {
  margin: 0 auto;
  max-width: 800px;
  padding: 0 20px;
}

.container {
  border: 2px solid #dedede;
  background-color: #d8d8d8 ;
  border-radius: 5px;
  padding: 10px;
  margin: 10px 0;
}

.darker {
  border-color: #ccc;
  background-color: #ddd;
}

.container::after {
  content: "";
  clear: both;
  display: table;
}

.container img {
  float: left;
  max-width: 60px;
  width: 100%;
  margin-right: 20px;
  border-radius: 50%;
}

.container img.right {
  float: right;
  margin-left: 20px;
  margin-right:0;
}

.time-right {
  float: right;
  color: #aaa;
}

.time-left {
  float: left;
  color: #999;
}
</style>
</head>
<body>

<div align="center">
    <h2>Anonymous Chat</h2>
</div>


<div class="container">
    <style>
    input[type=text], select {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    }

    input[type=submit] {
    width: 100%;
    background-color: #4CAF50;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    }

    input[type=submit]:hover {
    background-color: #45a049;
    }

    div {
    border-radius: 5px;
    background-color: #f2f2f2;
    padding: 20px;
    }

```

2). In the file ```room.html``` We have the code for the chat room which helps the user chat
it has integrated css and javascript.

```javascript
$(document).ready(function(){

setInterval(function(){
    $.ajax({
        type: 'GET',
        url : "/getMessages/{{room}}/",
        success: function(response){
            console.log(response);
            $("#display").empty();
            for (var key in response.messages)
            {
                var temp="<div class='container darker'><b>"+response.messages[key].user+"</b><p>"+response.messages[key].value+"</p><span class='time-left'>"+response.messages[key].date+"</span></div>";
                $("#display").append(temp);
            }
        },
        error: function(response){
            alert('An error occured')
        }
    });
},1000);

})


<script type="text/javascript">
  $(document).on('submit','#post-form',function(e){
    e.preventDefault();

    $.ajax({
      type:'POST',
      url:'/send',
      data:{
          username:$('#username').val(),
          room_id:$('#room_id').val(),
          message:$('#message').val(),
        csrfmiddlewaretoken:$('input[name=csrfmiddlewaretoken]').val(),
      },
      success: function(data){
         //alert(data)
      }
    });
    document.getElementById('message').value = ''
  });
```

youtube demo
https://youtu.be/OOFDu7zoBiY
