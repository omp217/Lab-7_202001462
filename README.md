# Lab7-202001462

**Name: Om Patel**  
**ID: 202001462**  

## Section-A
**Based on the input ranges, we can identify the following equivalence classes:** <br>

**Equivalence Class Partitions** <br/>
Day:
| Partition ID | Range | Status |
|----------------------|-------|--------|
| E1 | Between 1 and 28 | Valid |
| E2 | Less than 1 | Invalid |
| E3 | Greater than 31 | Invalid |
| E4 | Equals 30 | Valid |
| E5 | Equals 29 | Valid for leap year |
| E6 | Equals 31 | Valid |

Month:
| Partition ID | Range | Status |
|----------------------|-------|--------|
| E7 | Between 1 and 12 | Valid |
| E8 | Less than 1 | Invalid |
| E9 | Greater than 12 | Invalid |

Year: 
| Partition ID | Range | Status |
|----------------------|-------|--------|
| E10 | Between 1900 and 2015 | Valid |
| E11 | Less than 1 | Invalid |
| E12 | Greater than 2015 | Invalid |

**Equivalence Partitioning Test Cases:**

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=12, year=2015</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=32, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2001</td>
    <td>An error message</td>
  </tr>
</table>

<br>

**Boundary Value Analysis:**
Using boundary value analysis, we can identify the following boundary test cases:
1) The earliest possible date: (1, 1, 1900)
2) The latest possible date: (31, 12, 2015)
3) The earliest day of each month: (1, 1, 2000), (1, 2, 2000), (1, 3, 2000),..., (1, 12, 2000)
4) The latest day of each month: (31, 1, 2000), (28, 2, 2000), (31, 3, 2000),..., (31, 12, 2000)
5) Leap year day: (29, 2, 2000)
6) Invalid leap year day: (29, 2, 1900)
7) One day before earliest date: (31, 12, 1899)
8) One day after latest date: (1, 1, 2016)<br>

Based on these boundary test cases, we can design the following test cases:<br>

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=12, year=2015</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=32, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Valid input: day=1, month=6, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=5, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=15, month=6, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=31, month=4, year=2000</td>
    <td>An error message</td>
  </tr>
</table>
</br>

### P1. The function linearSearch searches for a value v in an array of integers a. If v appears in the array a, then the function returns the first index i, such that a[i] == v; otherwise, -1 is returned.

    int linearSearch(int v, int a[])
    {
        int i = 0;
        while (i < a.length)
        {
            if (a[i] == v)
            return(i);
            i++;
        }
        return (-1);    
    }
    
    @Test
    public void test() {
        unittesting obj = new unittesting();
        int[] arr1 = {2, 4, 6, 8, 10};
        int[] arr2 = {-3, 0, 3, 7, 11};
        int[] arr3 = {1, 3, 5, 7, 9};
        int[] arr4 = {};
        
        assertEquals(0, obj.linearSearch(2, arr1));
        assertEquals(4, obj.linearSearch(10, arr1));
        assertEquals(-1, obj.linearSearch(3, arr2));
        assertEquals(4, obj.linearSearch(9, arr3));
        assertEquals(-1, obj.linearSearch(2, arr4));
    }
        
 
**Equivalence Partitioning:**
 
| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| v is present in a        | Index of v         | 
| v is not present in a         | -1         | 

**Boundary Value Analysis:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| Empty array a        | -1         | 
| v is present at the first index of a         | 0         | 
| v is present at the last index of a length of a        | a-1         | 
| v is not present in a         | -1         | 

**Test suites:**

| Tester Action and Input Data | Value to be found | Expected Outcome |
|------------------------------|-------------------|------------------|
| **Valid partition:**                                                |
| [1, 2, 3, 4, 5]              | 3                 | 2                |
| [5, 10, 15, 20, 25]          | 5                 | 0                |
| [2, 4, 6, 8]                 | 5                 | -1               |
| [1, 3, 5, 7]                 | 4                 | -1               |
| **Boundary Value Analysis:**        |                   |                  |
| []          | 5                 | -1               |
| [5]          |5                  | 0               |
| [15]          | 5                 | -1               |
| [5, 10, 15, 20, 25]          | 5                 | 0                |
| [5, 10, 15, 20, 25]          | 25                | 4                |
| [2, 4, 6, 8]                 | 2.2               | Invalid input    |
| [2, 4, 6, 8]                 | a                 | Invalid input    |
| [1.1, c, 5, 7]               | 2                 | Invalid input    |
 
 
 
 

### P2. The function countItem returns the number of times a value v appears in an array of integers a.
    int countItem(int v, int a[])
    {
        int count = 0;
        for (int i = 0; i < a.length; i++)
            {
                if (a[i] == v)
                count++;
            }
        return (count);
    }
    
    public void testCountItem() {
        CountItems counter = new CountItems();
        int[] arr1 = {1, 2, 3, 4, 5};
        int[] arr2 = {1, 2, 3, 4, 5, 6, 7, 8, 9};
        int[] arr3 = {1, 2, 3, 4, 4, 4, 5, 6, 7, 8, 9};
        int[] arr4 = {};
        int v1 = 3;
        int v2 = 10;
        assertEquals(1, counter.countItem(v1, arr1));
        assertEquals(0, counter.countItem(v2, arr1));
        assertEquals(9, counter.countItem(v1, arr2));
        assertEquals(0, counter.countItem(v2, arr2));
        assertEquals(1, counter.countItem(v1, arr3));
        assertEquals(0, counter.countItem(v2, arr3));
        assertEquals(0, counter.countItem(v2, arr4));
    }
<br>

**Equivalence Partitioning:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| v is present in a        | Number of times v appears in a         | 
| v is not present in a         | 0         | 

**Boundary Value Analysis:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| Empty array a        | 0         | 
| v is present once in a         | 1         | 
| v is present multiple times in a        | Number of times v appears in a         | 
| v is not present in a         | 0        | 


**Test suites:**

| Tester Action and Input Data | Value to be found | Expected Outcome |
|------------------------------|-------------------|------------------|
| **Equivalence partition:**                                                |
| [1, 2, 3, 4, 5]              | 3                 | 1                |
| [5, 10, 15, 20, 25]          | 11                 | 0                |
| **Boundary Value Analysis:**        |                   |                  |
| []          | 5                 | 0               |
| [5]          |5                  | 1               |
| [15]          | 5                 | 0               |
| [5, 10, 5, 20, 25]          | 5                 | 2                |
| [2, 4, 6, 8]                 | 2.2               | Invalid input    |
| [2, 4, 6, 8]                 | a                 | Invalid input    |
| [1.1, c, 5, 7]               | 2                 | Invalid input    |
 
 

### P3. The function binarySearch searches for a value v in an ordered array of integers a. If v appears in the array a, then the function returns an index i, such that a[i] == v; otherwise, -1 is returned.
Assumption: the elements in the array a are sorted in non-decreasing order.

    int binarySearch(int v, int a[])
    {
        int lo,mid,hi;
        lo = 0;
        hi = a.length-1;
        while (lo <= hi)
        {
            mid = (lo+hi)/2;
            if (v == a[mid])
            return (mid);
            else if (v < a[mid])
            hi = mid-1;
            else
            lo = mid+1;
        }
        return(-1);
    }
    
    import static org.junit.Assert.assertEquals;
    import org.junit.Test;
    
    public class BinarySearchTest {
        @Test
        public void testBinarySearch() {
            BinarySearch bs = new BinarySearch();

            int[] arr1 = {1, 3, 5, 7, 9};
            assertEquals(0, bs.binarySearch(1, arr1)); // search for 1 in {1, 3, 5, 7, 9}
            assertEquals(2, bs.binarySearch(5, arr1)); // search for 5 in {1, 3, 5, 7, 9}
            assertEquals(4, bs.binarySearch(9, arr1)); // search for 9 in {1, 3, 5, 7, 9}
            assertEquals(-1, bs.binarySearch(4, arr1)); // search for 4 in {1, 3, 5, 7, 9}

            int[] arr2 = {2, 4, 6, 8, 10, 12};
            assertEquals(-1, bs.binarySearch(1, arr2)); // search for 1 in {2, 4, 6, 8, 10, 12}
            assertEquals(2, bs.binarySearch(6, arr2)); // search for 6 in {2, 4, 6, 8, 10, 12}
            assertEquals(5, bs.binarySearch(12, arr2)); // search for 12 in {2, 4, 6, 8, 10, 12}
            assertEquals(-1, bs.binarySearch(7, arr2)); // search for 7 in {2, 4, 6, 8, 10, 12}
        }
    }

**Equivalence Partitioning:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| v is present in a        | Index of v         | 
| v is not present in a         | -1         | 

**Boundary Value Analysis:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| Empty array a        | -1         | 
| v is present at the first index of a         | 0         | 
| v is present at the last index of a length of a        | a-1         | 
| v is not present in a         | -1         | 

**Test suites:**

| Tester Action and Input Data | Value to be found | Expected Outcome |
|------------------------------|-------------------|------------------|
| **Valid partition:**                                                |
| [1, 2, 3, 4, 5]              | 3                 | 2                |
| [5, 10, 15, 20, 25]          | 5                 | 0                |
| [2, 4, 6, 8]                 | 5                 | -1               |
| [1, 3, 5, 7]                 | 4                 | -1               |
| **Boundary Value Analysis:**        |                   |                  |
| []          | 5                 | -1               |
| [5]          |5                  | 0               |
| [15]          | 5                 | -1               |
| [1, 1, 1, 1, 1]          | 1                 | 0/1/2/3/4                |
| [5, 10, 15, 20, 25]          | 5                 | 0                |
| [5, 10, 15, 20, 25]          | 25                | 4                |
| [2, 4, 6, 8]                 | 2.2               | Invalid input    |
| [2, 4, 6, 8]                 | a                 | Invalid input    |
| [1.1, c, 5, 7]               | 2                 | Invalid input    |


### P4. The following problem has been adapted from The Art of Software Testing, by G. Myers (1979). The function triangle takes three integer parameters that are interpreted as the lengths of the sides of a triangle. It returns whether the triangle is equilateral (three lengths equal), isosceles (two lengths equal), scalene (no lengths equal), or invalid (impossible lengths).

    final int EQUILATERAL = 0;
    final int ISOSCELES = 1;
    final int SCALENE = 2;
    final int INVALID = 3;
    int triangle(int a, int b, int c)
    {
        if (a >= b+c || b >= a+c || c >= a+b)
        return(INVALID);
        if (a == b && b == c)
        return(EQUILATERAL);
        if (a == b || a == c || b == c)
        return(ISOSCELES);
        return(SCALENE);
    }
    
    @Test
    public void testEquilateral() {
      assertEquals("Equal", unittesting.triangle(3, 3, 3));
    }

    @Test
    public void testIsosceles() {
      assertEquals("Isosceles", unittesting.triangle(5, 5, 6));

    }

    @Test
    public void testScalene() {
      assertEquals("Scalene", unittesting.triangle(3, 4, 5));
    }

    @Test
    public void testIncorrectInput() {
      assertEquals("Incorrect input", unittesting.triangle(1, 2, 3));

    }
    
**Equivalence Partitioning:**

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: a=3, b=3, c=3</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=4, b=4, c=5</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=5, b=4, c=3</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=0, c=0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=-1, b=2, c=3</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Valid input: a=1, b=1, c=1</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=2, b=2, c=1</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=3, b=4, c=5</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=1, c=1</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=0, c=1</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=1, c=0</td>
    <td>INVALID</td>
  </tr>
</table>

**Boundary Value Analysis:**

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Invalid inputs: a = 0, b = 0, c = 0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid inputs: a + b = c or b + c = a or c + a = b (a=3, b=4, c=8)</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 1</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 100</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = b ≠ c = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a ≠ b = c = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = c ≠ b = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Scalene triangles: a = b + c - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: b = a + c - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: c = a + b - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Maximum values: a, b, c = Integer.MAX_VALUE</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Minimum values: a, b, c = Integer.MIN_VALUE</td>
    <td>INVALID</td>
  </tr>
</table>
</br>

### P5. The function prefix (String s1, String s2) returns whether or not the string s1 is a prefix of string s2 (you may assume that neither s1 nor s2 is null).
    public static boolean prefix(String s1, String s2)
    {
        if (s1.length() > s2.length())
        {
            return false;
        }

        for (int i = 0; i < s1.length(); i++)
        {
            if (s1.charAt(i) != s2.charAt(i))
            {
                return false;
            }
        }
        return true;
    }
    
    public void testPrefix() {
        String s1 = "hello";
        String s2 = "hello world";
        assertTrue(unittesting.prefix(s1, s2));

        s1 = "abc";
        s2 = "abcd";
        assertTrue(unittesting.prefix(s1, s2));

        s1 = "";
        s2 = "hello";
        assertTrue(unittesting.prefix(s1, s2));

        s1 = "hello";
        s2 = "hi";
        assertFalse(unittesting.prefix(s1, s2));

        s1 = "abc";
        s2 = "def";
        assertFalse(unittesting.prefix(s1, s2));
    }

**Equivalence Partitioning:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| Empty string s1 and s2        | True         | 
| Empty string s1 and non-empty s2         | True         | 
| Non-empty s1 is a prefix of non-empty s2        | True         | 
| Non-empty s1 is not a prefix of s2         | False         | 
| Non-empty s1 is longer than s2         | False         | 

**Boundary Value Analysis:**

| Tester Action and Input Data     | Expected Outcome      | 
| ------------- | :---: | 
| Empty string s1 and s2        | True         | 
| Empty string s1 and non-empty s2         | True         | 
| Non-empty s1 is not a prefix of s2         | False         | 
| Non-empty s1 is longer than s2         | False         | 

**Test Suites**

| Tester Action and Input Data | Expected Outcome |
|------------------------------|------------------|
| **Equivalence Partitioning**|
| s1= "abcd",s2 = "abcd" | true |
| s1 = "",s2 = "" | true |
| s1 = "ha",s2 = "hasrh" | true |
| s1 = "hcp",s2 = "hc" | false |
| s1 = "abc",s2 = "" | false |
| s1 = "",s2 = "abc" | true |
| s1 = "o",s2 = "ott" | true |
| s1 = "abc",s2 = "def" | false |
| s1 = "deg",s2 = "def" | false |
| **Boundary value analysis**|
| s1= "abcd",s2 = "abcd" | true |
| s1= "",s2 = "" | true |
| s1= "abcd",s2 = "" | false |
| s1= "",s2 = "abcd" | true |
| s1 = "aef",s2 = "def" | false |
| s1 = "def",s2 = "deg" | false |
| s1 = "a",s2 = "att" | true |
| s1 = "harsh",s2 = "patel" | false |


### P6: Consider again the triangle classification program (P4) with a slightly different specification: The programreads floating values from the standard input. The three values A, B, and C are interpreted asrepresenting the lengths of the sides of a triangle. The program then prints a message to the standard output that states whether the triangle, if it can be formed, is scalene, isosceles, equilateral, or right angled. Determine the following for the above program:

**a) Identify the equivalence classes for the system**
Equivalence Classes:<br>
EC1: Invalid inputs (negative or zero values)<br>
EC2: Non-triangle (sum of the two shorter sides is not greater than the longest side)<br>
EC3: Scalene triangle (no sides are equal)<br>
EC4: Isosceles triangle (two sides are equal)<br>
EC5: Equilateral triangle (all sides are equal)<br>
EC6: Right-angled triangle (satisfies the Pythagorean theorem)<br>

**b) Identify test cases to cover the identified equivalence classes. Also, explicitly mention which test case would cover which equivalence class. (Hint: you must need to be ensure that the identified set of test cases cover all identified equivalence classes)**
Test cases:<br>
TC1: -1, 0 <br>
TC2: 1, 2, 5<br>
TC3: 3, 4, 5<br>
TC4: 5, 5, 7<br>
TC5: 6, 6, 6<br>
TC6: 3, 4, 5<br>

Test case 1 covers class 1, test case 2 covers class 2, test case 3 covers class 3, test case 4 covers class 4, test case 5 covers class 5, and test case 6 covers class 6

**c) For the boundary condition A + B > C case (scalene triangle), identify test cases to verify the boundary.**
2, 3, 6<br>
3, 4, 8<br>
Both test cases have two sides that are shorter than the third side, and should not form a triangle

<br>

**d) For the boundary condition A = C case (isosceles triangle), identify test cases to verify the boundary.**
1, 2, 1<br>
0, 2, 0<br>
5, 6, 5<br>
Both test cases have two sides that are equal, but only test case 2 should form an isosceles triangle, other input are invalid.

<br>

**e) For the boundary condition A = B = C case (equilateral triangle), identify test cases to verify the boundary.**
5, 5, 5<br>
0, 0, 0<br>
Both test cases have all sides equal, but only test case 1 should form an equilateral triangle, other input are invalid.

<br>

**f) For the boundary condition A2 + B2 = C2 case (right-angle triangle), identify test cases to verify the boundary.**
3, 4, 5
0, 0, 0
-3, -4, -5
Both test cases satisfy the Pythagorean theorem, but only test case 1 should form right-angled triangle, other input are invalid.
triangle

<br>

**g) For the non-triangle case, identify test cases to explore the boundary.**
Test cases for the non-triangle case:<br>
TC11 (EC3): A=2, B=2, C=4 (sum of A and B is less than C)<br>

<br>

**h) For non-positive input, identify test points.**
Test points for non-positive input:<br>
TP1 (EC2): A=0, B=4, C=5 (invalid input)<br>
TP2 (EC2): A=-2, B=4, C=5 (invalid input)<br>
Note: Test cases TC1 to TC10 covers all identified equivalence classes.<br>

# Section B:
**1. Control flow diagram**<br>
<img src="https://user-images.githubusercontent.com/95064151/231530191-f34ad7e4-3bb6-4f02-90b5-2d84a206290e.png">

**2. Test sets**<br>

Statement coverage test sets: To achieve statement coverage, we need to make sure that every statement in the code is executed at least once.<br>
Test 1: p = empty vector<br>
Test 2: p = vector with one point<br>
Test 3: p = vector with two points with the same y component<br>
Test 4: p = vector with two points with different y components<br>
Test 5: p = vector with three or more points with different y components<br>
Test 6: p = vector with three or more points with the same y component<br>


Branch coverage test sets: To achieve branch coverage, we need to make sure that every possible branch in the code is taken at least once<br>
Test 1: p = empty vector<br>
Test 2: p = vector with one point<br>
Test 3: p = vector with two points with the same y component<br>
Test 4: p = vector with two points with different y components<br>
Test 5: p = vector with three or more points with different y components, and none of them have the same x component<br>
Test 6: p = vector with three or more points with the same y component, and some of them have the same x component<br>
Test 7: p = vector with three or more points with the same y component, and all of them have the same x component<br>


Basic condition coverage test sets: To achieve basic condition coverage, we need to make sure that every basic condition in the code (i.e., every Boolean subexpression) is evaluated as both true and false at least once<br>
Test 1: p = empty vector<br>
Test 2: p = vector with one point<br>
Test 3: p = vector with two points with the same y component, and the first point has a smaller x component<br>
Test 4: p = vector with two points with the same y component, and the second point has a smaller x component<br>
Test 5: p = vector with two points with different y components<br>
Test 6: p = vector with three or more points with different y components, and none of them have the same x component<br>
Test 7: p = vector with three or more points with the same y component, and some of them have the same x component<br>
Test 8: p = vector with three or more points with the same y component, and all of them have the same x component.<br>



Here is the screenshot of Eclipse:

Step 1: Install Eclipse IDE

![image](https://user-images.githubusercontent.com/111455228/232731823-fc115587-cd24-4953-a5ce-db8914a63220.png)

Step 2: Add JUNIT in Eclipse

![image](https://user-images.githubusercontent.com/111455228/232732046-69abc525-33e0-4113-9dd0-43940279e112.png)

### P1

    package tests;
    public class UnitTesting {
      public int linearSearch(int v,int a[]) {
        int i = 0;
        while (i < a.length)
        {
          if (a[i] == v)
            return(i);
          i++;
        }
        return (-1);
      }


![image](https://user-images.githubusercontent.com/111455228/232732422-df7cb320-6c4f-4ade-b331-ce047742ae14.png)


![image](https://user-images.githubusercontent.com/111455228/232733534-b1a7a282-1e2e-4417-a007-56b7b163389f.png)

![image](https://user-images.githubusercontent.com/111455228/232733668-d0c1cc3f-4510-45d3-b61d-cf1768e76172.png)

As we can see that first three test cases are correct and last one is incorrect.
Left Index shows us the test case results.
We also see that if we input v as double than it gives an error.So input should only be an integer.

### P2

    package tests;
    public class UnitTesting {
      public int linearSearch(int v,int a[]) {
        int count = 0;
        for (int i = 0; i < a.length; i++)
        {
        if (a[i] == v)
        count++;
        }
        return (count);
      }
    }
    
![image](https://user-images.githubusercontent.com/111455228/232733906-4bdec77b-8d47-4269-8028-0e0af269ba39.png)

![image](https://user-images.githubusercontent.com/111455228/232734026-454238c7-99d3-4e0b-ab0a-f9f41bc8b8e6.png)

![image](https://user-images.githubusercontent.com/111455228/232734133-91420a20-aea4-4a51-820a-c55cefa91419.png)

This proves our table and shows the result of testcases on left index.

    package tests;
    import org.junit.Test;
    import org.junit.FixMethodOrder;
    import org.junit.runners.MethodSorters;
    import static org.junit.Assert.*;
    //import org.junit.Test;
    @FixMethodOrder(MethodSorters.NAME_ASCENDING)
    public class squareUnit {
      @Test
    public void test1() {
        UnitTesting obj1= new UnitTesting();
        int[] n={1,2,3,4,4};  
        int output_f = obj1.linearSearch(4, n);

        assertEquals(2, output_f);
      }
      @Test
      public void test2() {
        UnitTesting obj1= new UnitTesting();
        int[] n={12,-24,2,89,34,45};  
        int output_f = obj1.linearSearch(24, n);

        assertEquals(1, output_f);
      }
      @Test
      public void test3() {
        UnitTesting obj1= new UnitTesting();
        int[] n={1,2,3,4,5};  
        int output_f = obj1.linearSearch(24, n);

        assertEquals(0, output_f);
      }
      @Test
      public void test4() {
        UnitTesting obj1= new UnitTesting();
        int[] n={12,24,2,89,34,45};  
        int output_f = obj1.linearSearch(24, n);

        assertEquals(1, output_f);
      }
      @Test
      public void test5() {
        UnitTesting obj1= new UnitTesting();
        int[] n={};  
        int output_f = obj1.linearSearch(24, n);
        assertEquals(1, output_f);
      }
    }
    P3
    package tests;
    public class UnitTesting {
      public int linearSearch(int v,int a[]) {
        int lo,mid,hi;
        lo = 0;
        hi = a.length-1;
        while (lo <= hi)
        {
        mid = (lo+hi)/2;
        if (v == a[mid])
        return (mid);
        else if (v < a[mid])
        hi = mid-1;
        else
        lo = mid+1;
        }
        return(-1);
      }
    }


![image](https://user-images.githubusercontent.com/111455228/232734413-b8dfa609-ba6d-4aad-9dc2-6dfa3f9d4df1.png)

![image](https://user-images.githubusercontent.com/111455228/232734595-990f1821-5794-48ca-9929-37c3c4a411b0.png)

![image](https://user-images.githubusercontent.com/111455228/232734596-bac6908f-79c2-4fe6-9a30-0e633718e4aa.png)

    package tests;
    import org.junit.Test;
    import org.junit.FixMethodOrder;
    import org.junit.runners.MethodSorters;
    import static org.junit.Assert.*;
    //import org.junit.Test;
    @FixMethodOrder(MethodSorters.NAME_ASCENDING)
    public class squareUnit {
      @Test
      public void test1() {
        UnitTesting obj1= new UnitTesting();
        int[] n={1};  
        int output_f = obj1.linearSearch(4, n);

        assertEquals(-1, output_f);
      }
      @Test
      public void test2() {
        UnitTesting obj1= new UnitTesting();
        int[] n={24,26,90};  
        int output_f = obj1.linearSearch(24,n);

        assertEquals(0, output_f);
      }
      @Test
      public void test3() {
        UnitTesting obj1= new UnitTesting();
        int[] n={1,2,3,4,5};  
        int output_f = obj1.linearSearch(4, n);

        assertEquals(1, output_f);
      }
      @Test
      public void test4() {
        UnitTesting obj1= new UnitTesting();
        int[] n={};  
        int output_f = obj1.linearSearch(24, n);

        assertEquals(-1, output_f);
      }
      @Test
      public void test5() {
        UnitTesting obj1= new UnitTesting();
        int[] n={};  
        int output_f = obj1.linearSearch(24, n);
        assertEquals(1, output_f);
      }
    }


### P4

    package tests;
    public class UnitTesting {
      final int EQUILATERAL = 0;
      final int ISOSCELES = 1;
      final int SCALENE = 2;
      final int INVALID = 3;
      public int linearSearch(int a,int b,int c) {
        if (a >= b+c || b >= a+c || c >= a+b)
          return(INVALID);
        if (a == b && b == c)
          return(EQUILATERAL);
        if (a == b || a == c || b == c)
          return(ISOSCELES);

          return(SCALENE);
      }
    }

![image](https://user-images.githubusercontent.com/111455228/232734703-567b9088-2740-48a0-ba7d-213090d292dc.png)

    package tests;
    import org.junit.Test;
    import org.junit.FixMethodOrder;
    import org.junit.runners.MethodSorters;
    import static org.junit.Assert.*;
    //import org.junit.Test;
    @FixMethodOrder(MethodSorters.NAME_ASCENDING)
    public class squareUnit {
      @Test
      public void test1() {
        UnitTesting obj1= new UnitTesting();
        int output_f = obj1.linearSearch(6,6,6);
        assertEquals(0, output_f);
      }
      @Test
      public void test2() {
        UnitTesting obj1= new UnitTesting();
        int output_f = obj1.linearSearch(10000,10000,9999);
        assertEquals(1, output_f);
      }

      @Test
      public void test3() {
        UnitTesting obj1= new UnitTesting();
        int output_f = obj1.linearSearch(10000,10000,99999);
        assertEquals(1, output_f);
      }
      @Test
      public void test4() {
        UnitTesting obj1= new UnitTesting();
        int output_f = obj1.linearSearch(0,0,0);
        assertEquals(0, output_f);
      }
    }

![image](https://user-images.githubusercontent.com/111455228/232734739-2e74a4a4-3254-4de8-8a5e-739bdac46a23.png)

![image](https://user-images.githubusercontent.com/111455228/232734756-ed74f691-96de-487b-8942-e9369f9fc386.png)

### P5

![image](https://user-images.githubusercontent.com/111455228/232734799-258039ea-ba5f-4f19-96ed-bc302c8791b2.png)

    package tests;
    import static org.junit.Assert.*;
    import org.junit.Test;
    public class prefixtest {
    @Test
    public void test1() {
    unittesting obj1= new unittesting();
    // int[] n={1,2,3,4,5,6,7,8};
    boolean output_f = obj1.prefix("maharth", "maharththakar");
    assertEquals(true, output_f);
    }
    @Test
    public void test2() {
    unittesting obj1= new unittesting();
    // int[] n={11,12,13,14,15,16,17};
    boolean output_f = obj1.prefix("hihello","hi" );
    assertEquals(true, output_f);
    }
    @Test
    public void test3() {
    unittesting obj1= new unittesting();
    // int[] n={11,12,13,14,15,16,17};
    boolean output_f = obj1.prefix("hello","helluhow" );
    assertEquals(true, output_f);
    }
    }

Class 1: Invalid inputs (negative or zero values)
Class 2: Non-triangle (sum of the two shorter sides is not greater than the longest side)
Class 3: Scalene triangle (no sides are equal)
Class 4: Isosceles triangle (two sides are equal)
Class 5: Equilateral triangle (all sides are equal)
Class 6: Right-angled triangle (satisfies the Pythagorean theorem)


Class 1: -1, 0
Class 2: 1, 2, 5
Class 3: 3, 4, 5
Class 4: 5, 5, 7
Class 5: 6, 6, 6
Class 6: 3, 4, 5

Test case 1 covers class 1, test case 2 covers class 2, test case 3 covers class 3, test case 4 covers class 4, test case 5 covers class 5, and test case 6 covers class 6.

c) Test cases to verify the boundary condition A + B > C for the scalene triangle:

2, 3, 6

3, 4, 8

Both test cases have two sides that are shorter than the third side, and should not form a triangle.

d) Test cases to verify the boundary condition A = C for the isosceles triangle:

2, 3, 3

5, 6, 5

Both test cases have two sides that are equal, and should form an isosceles triangle.

e) Test cases to verify the boundary condition A = B = C for the equilateral triangle:

5, 5, 5

9, 9, 9

Both test cases have all sides equal, and should form an equilateral triangle.

f) Test cases to verify the boundary condition A^2 + B^2 = C^2 for the right-angled triangle:

3, 4, 5

5, 12, 13

Both test cases satisfy the Pythagorean theorem and should form a right-angled triangle.

g) For the non-triangle case, identify test cases to explore the boundary.

2, 2, 4

3, 6, 9

Both test cases have two sides that add up to the third side, and should not form a triangle.

h) For non-positive input, identify test points.

0, 1, 2

1, -2, -3
Both test cases have at least one non-positive value, which is an invalid input.
