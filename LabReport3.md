# **Lab Report 3 - Bugs and Commands**   
In this lab report, I reflect on my learning debugging and testing using JUnit and using various commands to get all kinds of information on repositories.   

---   

## Bugs:   
Here I demonstrate my process of debugging a program   

### Failure-Inducing Input:   
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests {
  @Test 
	public void testReverseInPlaceLen3() {
    int[] input = {0, 1, 2};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{2, 1, 0}, input);
	}
}
```
### Non-Failure-Inducing Input:   
```
import static org.junit.Assert.*;
import org.junit.*;

public class ArrayTests { 
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
}
```   
### Symptom:
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/a82566e6-7fb7-4ff4-87be-109bf8c92bbe)   
### Debugging:   
Before:   
```
public class ArrayExamples {
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
}
```
After:   
```
public class ArrayExamples {
  static void reverseInPlace(int[] arr) {
    int[] shallow = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      shallow[i] = arr[i];
    }
    for(int i = 0; i < shallow.length; i += 1) {
      arr[i] = shallow[shallow.length - i - 1];
    }
  }
}
```
### Explanation:   
The original code modifies the array while it is also being accessed, causing it to reverse elements already reversed. The fix I implemented creates a shallow copy of the parameter array which the new returned array can access to reverse its elements.   

---

## Researching Commands:   
