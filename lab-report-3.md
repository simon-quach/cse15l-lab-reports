# Lab Report 3 - Bugs and Commands (Week 5)

## Part 1

In week 4's lab, there was a function called `reverseInPlace()` that was supposed to reverse an array in place.

### A failure-inducing input for the buggy program

```
@Test
public void testReverseInPlace1() {
  int[] input1 = { 3, 5, 2, 4, 1 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1, 4, 2, 5, 3}, input1);
}
```

### An input that doesn't induce a failure, as a JUnit test and any associated code (write it as a code block in Markdown)

```
@Test
public void testReverseInPlace2() {
  int[] input1 = { 1 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 1 }, input1);
}
```

### The symptom, as the output of running the tests

![image](https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/d85c0304-5021-48f5-b0db-0428383830ea)

### The bug, as the before-and-after code change required to fix it

#### Before

```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```

#### After

```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = temp;
  }
}
```

The original code replaces the left side of the array with the right side, but once it starts iterating past the middle of the array, we have already lost the values of the left side array, so we can't use those to change the right side. In order to fix this, I created a temporary variable called `temp` to store the left value, and simutaneously changed the left and right values at the same time.

## Part 2

Here I want to take a look at the `find` command.

This command helps you find files and directories with a specific query.

Here is the syntax for using `find`:

```
find [path] [options] [expression]
```

### Options for using `find`

#### `-name`

You can use this option to look up a specific name for a file or directory.

**Using on a directory:**

```
$ find ./technical/ -type d -name "911report"
./technical/911report
```

This command found the directory name "911report" in `./technical`.

**Using on a file:**

```
$ find ./technical/ -type f -name "chapter-1.txt"
./technical/911report/chapter-1.txt
```

This command found the file name "chapter-1.txt" in `./technical`.

#### `-type`

You can use this option to specify the type to look up, so either directory or file.

**Using on a directory:**

```
$ find ./technical/ -type d -name "911report"
./technical/911report
```

This command found all directories in `./technical` under the name "911report" and not files.

**Using on a file:**

```
$ find ./technical/ -type f -name "chapter-1.txt"
./technical/911report/chapter-1.txt
```

This command found all files in `./technical` under the name "chapter-1.txt" and not directories.

#### `-print`

You can use this option to print certain directories or files.

**Using on a directory:**

```
$ find ./technical/ -type d -print
(printed all files in ./technical)
./technical/plos/pmed.0020273.txt
./technical/plos/pmed.0020274.txt
./technical/plos/pmed.0020275.txt
./technical/plos/pmed.0020278.txt
./technical/plos/pmed.0020281.txt
```

This command printed all directories in `./technical`. I didn't include the entire output because it was too long. I only included the last couple of prints.

**Using on a file:**

```
$ find ./technical/ -type f -print
(printed all directories in ./technical)
./technical/government/Env_Prot_Agen
./technical/government/Gen_Account_Office
./technical/government/Media
./technical/government/Post_Rate_Comm
./technical/plos
```

This command printed all files in `./technical`. I didn't include the entire output because it was too long. I only included the last couple of prints.

#### `-empty`

You can use this option to print empty files or directories.

**Using on a directory:**

```
$ find ./technical/ -type d -empty
```

This command printed nothing because there were no empty directories in `./technical`.

**Using on a file:**

```
$ find ./technical/ -type f -empty
```

This command printed nothing because there were no empty files in `./technical`.

Source: https://www.geeksforgeeks.org/find-command-in-linux-with-examples/
