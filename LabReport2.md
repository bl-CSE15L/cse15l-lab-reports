# **Lab Report 2 - Servers and SSH Keys**   
In this lab report, I reflect on my learning about connecting to a remote system, programming and hosting my own web server, and creating my own SSH key.   

---

## Chat Server:   
ChatServer.java - My personal implementation using a String variable to store messages   
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String chatLogs = "";
    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return chatLogs;
        } else if (url.getPath().equals("/add-message")) {
            String[] separateQueries = url.getQuery().split("&");
            String[] messageString = separateQueries[0].split("=");
            String[] userString = separateQueries[1].split("=");
            if (messageString[0].equals("s") && userString[0].equals("user")) {
                chatLogs += (userString[1] + ": " + messageString[1]) + "\n";
            }
            return chatLogs;
        } else
        return "404 Not Found or Incorrect Args";
    }
}

class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

### /add-message - Example 1   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/34421475-bfa2-4fd7-b461-54803c002da6)   
In this screenshot, the ```handleRequest``` method was called. The ```handleRequest``` method also calls on ```equals()```, ```getQuery()```, and ```.split()``` to parse all the needed ```String```s from the URL. The main method is called when the server is started and uses ```parseInt()``` for the port and ```start()``` to start the server.   
The argument passed into ```handleRequest``` is the URL of the web server with the ```/add-message``` path stored as a ```URI``` parameter. This ```URI``` is then broken down through the subsequent methods to get the Strings ```messageString``` and ```userString``` which then get displayed through their concatenation in the field ```chatLogs``` which is an initially empty ```String```.
The field that gets changed is ```chatLogs``` as it is the ```String``` variable that records all the messages and is the variable that is displayed and returned. This variable gets updated every time a new message is added and starts empty when the server starts.   

### /add-message - Example 2   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/1fd3cd1d-d197-4534-8aec-969f9b385aa1)   
In this screenshot, the ```handleRequest``` method is also called. The ```handleRequest``` method calls on ```equals()```, ```getQuery()```, and ```.split()``` like last time to parse all the needed ```String```s from the URL.  
The argument passed into ```handleRequest``` is the URL of the web server with the ```/add-message``` path. This URL is again broken down through the subsequent methods to get new ```messageString``` and ```userString``` ```String```s which get concatenated in ```chatLogs``` with all the previous messages and displayed.
The field that gets changed is ```chatLogs``` as it concatenates all the messages since the server started. In this screenshot, it concatenates the previous message from jpolitz and yash.

---
## SSH Key:   

### Private Key   
My private key for ``ieng6``` is in ```/c/Users/jedix/.ssh/id_rsa```   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/af5adf62-b61d-4aee-b727-18657a07f5c9)

### Public Key   
My Public key for ``ieng6``` is in ```/home/linux/ieng6/oce/7g/blappay/.ssh/authorized_keys```   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/0512beb1-ee1b-414f-a4c9-0c8c92d9cc5e)

### Logging In
Here I don't need to use a password to login to ```ieng6```   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/3d392c13-98f6-416a-bc71-8e4a1b18be69)

---

## What I Learned
Throughout these past 2 weeks, I found it really exciting to learn how to program my own web server and host it remotely. I learned that changes saved locally are not saved remotely and vice versa and I also learned how to navigate across both systems within my terminal. Additionally, this experience has helped me visualize how directories and files interact with one another when trying to access them.   

---
