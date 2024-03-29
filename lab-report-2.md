# Lab Report 2 - Servers and SSH Keys (Week 3)

## Part 1
In this section, I created a webserver called ChatServer that supports the path `/add-message`, which adds messages to the chat log. It should keep track of a single string that gets added to by incoming requests.

Here is the code that I wrote for the implementation:
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
  // The one bit of state on the server: a number that will be manipulated by
  // various requests.
  ArrayList<String[]> mapping = new ArrayList<String[]>();

  public String handleRequest(URI url) {

    if (url.getPath().equals("/")) {
      String res = "";
      for (String[] message : mapping) {
        res += message[0] + ": " + message[1] + "\n";
      }
      if (res.equals("")) {
        return "No new messages";
      }
      return res;
    } else {
      if (url.getPath().contains("/add-message")) {
        String[] parameters = url.getQuery().split("&");
        String user = parameters[1].split("=")[1];
        String text = parameters[0].split("=")[1];
        String[] message = { user, text };
        mapping.add(message);

        String res = "";
        for (String[] m : mapping) {
          res += m[0] + ": " + m[1] + "\n";
        }
        if (res.equals("")) {
          return "No new messages";
        }
        return res;
      }
      return "404 Not Found!";
    }
  }
}

class ChatServer {
  public static void main(String[] args) throws IOException {
    if (args.length == 0) {
      System.out.println("Missing port number! Try any number between 1024 to 49151");
      return;
    }

    int port = Integer.parseInt(args[0]);

    Server.start(port, new Handler());
  }
}
```

To start, I used the path `/add-message?s=Hello!&user=Simon` to mimick a message "Hello!" sent by user named "Simon". The page shows this:

<img width="544" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/eca55923-b080-48f8-8677-c0767f7f1e64">
<br />

This calls the handleRequest method in my code. Since the path is `/add-message`, the code looks at the logic under there if statement `if (url.getPath().contains("/add-message"))`. It stores the two parameters in `String[] parameters` like this:
```
{ "s=Hello!", "user=Simon" }
```
<br />

The "s=" and "user=" are then removed and the two strings are concatenated to the results string that is later returned. Once the res string returns, it should have added an additional message. When a request with the path `/add-message` is received, the parameters are parsed and used to create a new message entry, which is then added to the `mapping` array. Thus, with each request to add a message, the `mapping` field is updated to include the new message. When there is nothing in the message, a blank string will be added.

After I used `/add-message?s=Hey%20there!&user=Simon2` and the page shows this:

<img width="580" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/61479e7e-0615-4ff4-8dc7-3f590c92c031">
<br />

This also calls the handleRequest method in my code. Since the path is `/add-message`, the code looks at the logic under there if statement `if (url.getPath().contains("/add-message"))`. It stores the two parameters in `String[] parameters` like this:
```


{ "s=Hey there!", "user=Simon2" }
```

The "s=" and "user=" are then removed and the two strings are concatenated to the results string that is later returned. Once the res string returns, it should have added an additional message. When a request with the path `/add-message` is received, the parameters are parsed and used to create a new message entry, which is then added to the `mapping` array. Thus, with each request to add a message, the `mapping` field is updated to include the new message. When there is nothing in the message, a blank string will be added.

<br/>

## Part 2
### This is where my private SSH key is located.
<img width="334" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/607074a2-1aad-488c-aea6-10896c34e921">

Path: `/Users/simonquach/.ssh/id_rsa`
<br/>

### This is where my public SSH key is located on ieng6's file system.
<img width="579" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/98d1c50f-4a51-4c17-a25d-afe662ab39b5">

Path: `/home/linux/ieng6/oce/59/siquach/.ssh/authorized_keys`
<br/>

### Here I logged into my ieng6 account without being asked for a password.
<img width="588" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/9c38e04a-3437-4128-b631-d2b9e885ed26">

<br/>

## Part 3
I gained hands-on experience with creating and deploying a basic java web server. It can handle HTTP get requests through the URL. I was also able to use the URL parameters as search queries and data to pass to the backend. Furthermore, I learned about SSH key authentication. By creating a pair of keys, putting one on my computer and the other on the remote computer, I was able to connect to the remote computer without inputting a password every time.
