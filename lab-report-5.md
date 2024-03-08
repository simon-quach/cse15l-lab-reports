# Part 1 - Debugging Scenario

## Student Message
Hi! I'm having an issue with the code that I am writing. I'm writing a function called `merge` that merges two sorted lists of strings (`list1` and `list2`) into one sorted list. When I run `grade.sh` to test if my code works, it fails one of the test cases. I am getting this error: `org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds`. I assume my code is not optimized well enough, but I can't seem to figure out what's wrong. Here is a screenshot of my error code and my tester code:

<img width="622" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/44469dbb-6815-452b-8436-fd2375aeebfd">
<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/f9eb961b-b9a7-47a9-95e3-ecdf08667b0e">

## TA Message
Hi! Thanks for reaching out. It seems that there is most likely something wrong with the function that you wrote. Can you send a screenshot of your code? Also, is that your output from running `bash grade.sh`?

## Student Message
Yes, that is my output from running `bash grade.sh`. Here is a screenshot of my `merge` function:

<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/1eb32b87-2215-42f7-a95d-c136ccf3bc42">

## TA Message
The bug is located in the very last `index1 += 1` line, inside of the `while (index2 < list2.size())` loop. Instead of `index1`, it should be `index2`, because in this while loop, you're supposed to increment the second index to loop through the second list, or else it will be stuck in an infinite loop. Here is the corrected code:

<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/96e0c793-ce54-4196-92c8-8269a386c5ec">

## Student Message
After running `bash grade.sh` again to test my code, everything works!

<img width="191" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/9157fc3d-e1fd-40e9-8a26-29f628857dea">

## All Files
### `grade.sh`
```
CPATH=".:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar"

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

if [[ $# -eq 0 ]]
then
    echo "No arguments provided."
    exit 1
fi

git clone $1 student-submission 2> git-output.txt
if [[ $? -ne 0 ]]
then
    echo "Error cloning repo, Please check link"
    exit 1
fi


if [[ -f student-submission/TestListExamples.java ]]
then 
    echo "Missing Necessary Files"
    exit 1
fi

cp TestListExamples.java student-submission/ListExamples.java grading-area
cp -r lib grading-area

cd grading-area
pwd
javac -cp $CPATH  *.java 2> error.txt
if [[ $? -ne 0 ]]
then
    echo "Compilation Error(s), Please Fix and Resubmit"
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt
```

### Wrong `ListExamples.java`
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker {
  boolean checkString(String s);
}

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while (index1 < list1.size() && index2 < list2.size()) {
      if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      } else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while (index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while (index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }

}
```

### Corrected `ListExamples.java`
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker {
  boolean checkString(String s);
}

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for (String s : list) {
      if (sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }

  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while (index1 < list1.size() && index2 < list2.size()) {
      if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      } else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while (index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while (index2 < list2.size()) {
      result.add(list2.get(index2));
      index2 += 1;
    }
    return result;
  }

}
```

# Part 2 – Reflection

During the second half of this quarter, I really enjoyed doing all of the in person labs because I am a firm believer that hands-on experience is the best way to learn new things, especially when it comes to programming. Something new that I learned was how to use bash to automate command line commands, and also how to use arguments with the command line. Using vim has also been really cool, because it's another way to edit documents and files when you only have the command line available. It makes you appreciate the many different tools that developers have made throughout the years to make the process of programming even easier.
