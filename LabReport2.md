# **Lab Report 2 - Servers and SSH Keys**   
In this lab report, I reflect on my learning about connecting to a remote system, programming and hosting my own web server, and creating my own SSH key.   

---

## Chat Server:   
ChatServer.java - My personal implementation using a String variable to store messages.
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
Server.java - Pulled from the given wavelet code.
```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started!");
    }
}
```
---  
### /add-message - Example 1   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/34421475-bfa2-4fd7-b461-54803c002da6)   
ttt   

### /add-message - Example 2
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/1fd3cd1d-d197-4534-8aec-969f9b385aa1)   
ttt

---
