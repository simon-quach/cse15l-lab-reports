# Week 1 Lab Report

## cd
### No Arguments
Command:
```
[user@sahara ~]$ cd
```

Output:
```
[user@sahara ~]$  
```

It changes to the root directory. **Not an error.**

### With Directory
Command:
```
[user@sahara ~]$ cd lecture1
```

Output:
```
[user@sahara ~/lecture1]$  
```

It changes the directory to /lecture1. **Not an error.**

### With File
Command:
```
[user@sahara ~/lecture1]$ cd Hello.java
```

Output:
```
bash: cd: Hello.java: Not a directory
```

It doesn't change directories because the argument given is a file. **Error.**

## ls
### No Arguments
Command:
```
[user@sahara ~]$ ls
```

Output:
```
lecture1
```

It shows the files and directories in the "/" directory. **Not an error.**

### With Directory
Command:
```
[user@sahara ~]$ ls lecture1
```

Output:
```
Hello.class  Hello.java  messages  README
```

It shows the files and directories in the "/lecture1" directory. **Not an error.**

### With File
Command:
```
[user@sahara ~/lecture1]$ ls Hello.java
```

Output:
```
Hello.java
```

It shows the file given, which is "Hello.java". **Not an error.**

## cat
### No Arguments
Command:
```
[user@sahara ~]$ cat
```

Output:
```

```

It doesn't print anything because no argument was given. **Not an error.**

### With Directory
Command:
```
[user@sahara ~]$ cat lecture1
```

Output:
```
cat: lecture1/: Is a directory
```

It doesn't show the file contents because the argument given was a directory. **Error.**

### With File
Command:
```
[user@sahara ~/lecture1]$ cat Hello.java
```

Output:
```
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOExcept
ion {
    String content = Files.readString(Path.of(args[0]), 
StandardCharsets.UTF_8);    
    System.out.println(content);
  }
```

It prints the file contents because a file was given for the argument. **Not an error.**
