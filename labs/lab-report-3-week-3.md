# Week 3 – Servers and Bugs

## Part 1 - Search Engine

The following is my code for a simple search engine that takes in words, saves them, and then can search for words containing certain substrings.

```
import java.io.IOException;
import java.net.URI;
import java.util.*;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    List<String> library = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            String StringOut = String.join(", ", library);
            return String.format("Current library: %s", StringOut);
        } 
        else if (url.getPath().equals("/search")) {
            System.out.println("Path: " + url.getPath());
            String[] parameters = url.getQuery().split("=");
            List<String> buffer = new ArrayList<String>();
            if (parameters[0].equals("s")) {
                for (int i = 0; i < library.size(); i += 1)
                    if(library.get(i).contains(parameters[1]))
                        buffer.add(library.get(i));
                String StringOut = String.join(", ", buffer);
                return String.format("Searched library: %s", StringOut);
            }
        } 
        else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    library.add(parameters[1]);
                    return String.format("%s added to library!", parameters[1]);
                }
            }
        }
        return "404 Not Found!";
    }
}

class SearchEngine {
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

Here is an example of a word being added to the library. We made several method calls for println(), getPath(), contains(), getQuery(), split(), equals(), add(), and format(). println() takes a string, in this case the url path, and puts it out onto the terminal so there is a record of what is being done on the website. contains() takes a string, in this case "/add" and lets us confirm that a substring exists within the path found by getPath(). getQuery() specifially returns the query portion of the url and split() splits the query into two portions depending on where the "=" is. equals() takes a string and compares it to another string, just makes sure the URL is formatted correctly. add() takes a string puts the new word into the library. format() takes a string and allows for a sentence to have variable strings formatted in which is then returned and displayed on the website. <br>
![Add Example](/cse15l-lab-reports/labs/images/SearchEngineAddExample.png)

This is an example of the main page of the website after some words have been added to the library. There are some methods being called including getPath(), equals(), join(), and format(). equals() takes a sting, in this case "/", and comapres it to the path found by getpath(). join() takes two strings, a separater and the string list, which formats them all into one comma separated list. format() lets us format a string with our string variable, which is then returned and displayed on the website. <br>

![Main Example](/cse15l-lab-reports/labs/images/SearchEngineMainExample.png)

Here is an example of a word being searched for in the library. To search for a word in the list, we have to make several method calls for println(), getQuery(), split(), equals(), size(), get(), contains(), add(), join(), and format(). println() takes a string, in this case the url path found by getPath(), and prints onto the terminal to record what the website is doing. getQuery() returns the query portion of the url which split(), given the string "=", separated the url into two portions. equals() takes a sring and compares it to another, in this case just confirm the url is formated properly. size() returns the number of indexes in a list, which was used to iterate through the list. get() takes an integer and returns the string from that index and contains() takes a string which is used to check for a substring as it iterates through the list. If we find a string that does contain the substring we use it as an argument in add() which adds the found string to a list. join() then takes a separator string and the list, putting every found word into a comma separated list. format() takes this string and formats it into a short statement before being displayed onto the website. <br>

![Command Example](/cse15l-lab-reports/labs/images/CommandExample.png)

## Part 2 - Debugging

The following is the code for a test for ListExamples.java.
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.ArrayList;
import java.util.List;

public class ListTests {
  @Test
  public void merge5() {
      List<String> input1 = new ArrayList<>();
      List<String> input2 = new ArrayList<>();
      List<String> expected1 = new ArrayList<>();
      input2.add("crab");
      input2.add("power");
      input2.add("sand");
      input1.add("sandwich");
      input2.add("towers");
      expected1.add("crab");
      expected1.add("power");
      expected1.add("sand");
      expected1.add("sandwich");
      expected1.add("towers");
      assertEquals(expected1, ListExamples.merge(input1, input2));
    }
}
```

After running this text, we see this error. There is some kind of infinite loop that causes the test to not even fully run. <br>

![Search Example](/cse15l-lab-reports/labs/images/ListBugExample.png)

The bug is found in the following section of code. In the final while loop, we can see that the index1 is being itterated when index2 is being used. This causes the while loop to never actual finish, causing the code to fail. After changing index1 to index2 in the loop, the code works fine. 

```
static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;
    while(index1 < list1.size() && index2 < list2.size()) {
      if(list1.get(index1).compareTo(list2.get(index2)) < 0) {
        result.add(list1.get(index1));
        index1 += 1;
      }
      else {
        result.add(list2.get(index2));
        index2 += 1;
      }
    }
    while(index1 < list1.size()) {
      result.add(list1.get(index1));
      index1 += 1;
    }
    while(index2 < list2.size()) {
      result.add(list2.get(index2));
      index1 += 1;
    }
    return result;
  }
```

The following is the code for a test for ArrayExamples.java.
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
	@Test 
	public void testReverseInPlace1() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
}
```

After running this code, we get the following error. The code from the ArrayExamples does not properly reverse the array. <br>

![Search Example](/cse15l-lab-reports/labs/images/ArrayBugExample.png)

The bug is found in the following section of code. The function reverseInPlace, the for loop not only iterates through the entire array, it also does not properly buffer the swapping values causing many of the values to be completely erased. Dividing arr.length by 2 and adding a buffer variable inside the loop allows for the code to properly reverse the array.

```
public class ArrayExamples {

  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }

  // Averages the numbers in the array (takes the mean), but leaves out the
  // lowest number when calculating. Returns 0 if there are no elements or just
  // 1 element in the array
  static double averageWithoutLowest(double[] arr) {
    if(arr.length < 2) { return 0.0; }
    double lowest = arr[0];
    for(double num: arr) {
      if(num < lowest) { lowest = num; }
    }
    double sum = 0;
    for(double num: arr) {
      if(num != lowest) { sum += num; }
    }
    return sum / (arr.length - 1);
  }
}
```