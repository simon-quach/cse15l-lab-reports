# Week 1 Lab Report

## cd
### No Arguments
Command:
```
cd
```

Output:
```
[user@sahara ~]$  
```

### With Directory
Command:
```
cd lecture1
```

Output:
```
[user@sahara ~/lecture1]$  
```

### With File
Command:
```
cd Hello.java
```

Output:
```
bash: cd: Hello.java: Not a directory
```

## ls
### No Arguments
Command:
```
ls
```

Output:
```
lecture1
```

### With Directory
Command:
```
ls lecture1
```

Output:
```
Hello.class  Hello.java  messages  README
```

### With File
Command:
```
ls Hello.java
```

Output:
```
Hello.java
```

## cat
### No Arguments
Command:
```
cat
```

Output:
```

```

### With Directory
Command:
```
cat lecture1
```

Output:
```
cat: lecture1/: Is a directory
```

### With File
Command:
```
cat Hello.java
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
