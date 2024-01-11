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

The directory is changed to the home directory when no argument is given. **Not an error.**

### With Directory
Command:
```
[user@sahara ~]$ cd lecture1
```

Output:
```
[user@sahara ~/lecture1]$  
```

Since a directory "lecture1" was given as an argument, the command changes the working directory to the inputted argument. **Not an error.**

### With File
Command:
```
[user@sahara ~/lecture1]$ cd Hello.java
```

Output:
```
bash: cd: Hello.java: Not a directory
```

It doesn't change directories because the argument given is a file. The argument only accepts directories. **Error.**

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

Since no argument is given, it automatically shows the files and directories in the "./" directory, or the working directory. **Not an error.**

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

It shows the file given, which is "Hello.java". Instead of showing multiple files and directories, it only displays one file, because the argument given was a single file. **Not an error.**

## cat
### No Arguments
Command:
```
[user@sahara ~]$ cat
```

Output:
```

```

Since no argument was given, the command prints nothing as a result. **Not an error.**

### With Directory
Command:
```
[user@sahara ~]$ cat lecture1
```

Output:
```
cat: lecture1/: Is a directory
```

It doesn't show the file contents because the argument given was a directory, rather than a file. **Error.**

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
