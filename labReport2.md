# Lab Report 2: Servers and Bugs :desktop_computer::bug:

## Part 1: Creating the server.
### The code for our StringServer looks like this:
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String str = "";
    String newStr;
    int size = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(str);
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    if (size == 0) {
                        str += parameters[1];
                        size++;
                        return String.format("Success! '" + str + 
                          "' has just been printed in a new line!");
                    }
                    else {
                        newStr = parameters[1];
                        str += "\n" + newStr;
                        size++;
                        return String.format("Success! '" + newStr + 
                          "' has just been printed in a new line!");
                    }
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
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

### Additionally, we'll need another file named Server like this one:

```
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
        System.out.println("Server Started! Visit http://localhost:" + port + " to visit.");
    }
}
```

### To launch our server, we open a new terminal in VS Code and type the following inside the directory with our server files:
![serverLaunch](https://user-images.githubusercontent.com/122497486/215660983-293cc874-8bc3-44af-aec3-cc2ac4505d93.png)

Our server should now be up and running! Let's go ahead and test it...

### Here we can see a couple of tests checking to see that the requests are handled correctly:

#### 1. Testing "add-message?s=CSE 15L TA's rock!".
![test1](https://user-images.githubusercontent.com/122497486/215658283-303c6877-3e87-4bd1-ba1e-2116b7597a5c.png)

#### Result:
![test1result](https://user-images.githubusercontent.com/122497486/215658321-bcb3dfb0-9536-4b5d-8aab-bbff68de2d37.png)

Lets review some of the methods that were called in this first test:
* `handleRequest()` This method takes an url as an argument, in this case: *"localhost:3333/add-message?s=CSE 15L TA's rock!"*
* `getPath()` This method returns the path component of this URI that got passed in the `HandleRequest()` method, which is "/add-message".
* `contains()` The argument for this method was *"/add-message"*, so it checks to see that the path contains "/add-message".
* `getQuery()` This method returns the query component of this URI that got passed in the `HandleRequest()` method, which is "s=CSE 15L TA's rock!".
* `split()` The argument for this method was *"="*, so it splits the query into the LHS("s") and RHS("CSE 15L TA's rock!") of the equal sign.
* `equals()` The argument for this method was *"s"*, so it checks that the LHS of the equal sign was equal to "s".

The fields of this class that changed as a result of handling the request are `String str` and `int size`.
The field `str` was changed to "CSE 15L TA's rock!", while `size` is now 1.



#### 2. Testing another string.
![test2](https://user-images.githubusercontent.com/122497486/215658368-5c7d4879-7100-46f8-838f-1876857cdbda.png)

#### Result:
![test2result](https://user-images.githubusercontent.com/122497486/215658399-59a450f8-823a-4aae-a1f7-e4b21476959e.png)

Finally, let's go over the methods that were called in the second test:
* `handleRequest()` This method takes an url as an argument, in this case: *"localhost:3333/add-message?s=Anything you type here will be concatenated to the previous string and printed in a new line!"*
* `getPath()` This method returns the path component of this URI that got passed in the `HandleRequest()` method, which is "/add-message".
* `contains()` The argument for this method was *"/add-message"*, so it checks to see that the path contains "/add-message".
* `getQuery()` This method returns the query component of this URI that got passed in the `HandleRequest()` method, which is "s=Anything you type here will be concatenated to the previous string and printed in a new line!".
* `split()` The argument for this method was *"="*, so it splits the query into the LHS("s") and RHS("Anything you type here will be concatenated to the previous string and printed in a new line!!") of the equal sign.
* `equals()` The argument for this method was *"s"*, so it checks that the LHS of the equal sign was equal to "s".

The fields of this class that changed as a result of handling the request are `String str`, `String newStr`, and `int size`.
The field `str` was changed to "CSE 15L TA's rock!\nAnything you type here will be concatenated to the previous string and printed in a new line!", `newStr` to "Anything you type here will be concatenated to the previous string and printed in a new line!", and `size` is now 2.

## Part 2: Analyzing a :bug:

### There is a bug lying somewhere in this method, see if you can find it...
```
// Returns a *new* array with all the elements of the 
// input array in reversed order.
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

Here's a failure-inducing input for our buggy program in the form of a JUnit test:

```
@Test
  public void testReversed() {
    int[] input1 = {5, 4, 3};
    assertArrayEquals(new int[]{3, 4, 5}, ArrayExamples.reversed(input1));
  }
```

However, if we try the following input...

```
@Test
  public void testReversed() {
    int[] input1 = {0, 0, 0};
    assertArrayEquals(new int[]{0, 0, 0}, ArrayExamples.reversed(input1));
  }
```

...the test runs just fine and passes. What a sneaky little :bug:!

Let's look at the symptom of our program:

![symptom](https://user-images.githubusercontent.com/122497486/215676633-5f298500-21de-4bfc-87f4-6782a12d4e53.png)

Now that we know what our program's symptom is, let's get rid of the bug that's causing our program to run incorrectly:

### Before:

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```

### After:

```
static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

This gets rid of our bug since now we are correctly assigning the indexes from the old array to the new array (as well as returning the newArray and not the old one).


## Part 3:

I learned many new things these past two weeks!
1. How to launch a web server.
2. How to run a server in a remote computer.
3. How URL handlers work.
4. The difference between symptoms and bugs.
5. And much, much more...
