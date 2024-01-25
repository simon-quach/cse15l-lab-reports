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
        return "Message added!";
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

<img width="544" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/eca55923-b080-48f8-8677-c0767f7f1e64">
<img width="580" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/61479e7e-0615-4ff4-8dc7-3f590c92c031">
