


<span style="text-decoration:underline;">Group # 22:</span>

Fanny Lo 

Caroline Basta

Dhyey Lalseta

Sukriti Sharma



1. Introduction

    The purpose of this lab us to advance our knowledge of the JUnit framework by developing test cases via the whitebox-testing method. We created various test cases with this method and also used code coverage tools to verify the coverage of our cases. 

2. Manual data-flow coverage calculations for X and Y methods

<span style="text-decoration:underline;">DataUtilities.calculateColumnTotal</span>


DataUtilities.calculateColumnTotal is an overloaded method with different implementations. For data flow coverage measures, we will arbitrarily DataUtilities.calculateColumnTotal(Values2D data, int column) to perform the analysis.


 The code implementation for DataUtilities.calculateColumnTotal(Values2D data, int column) is as follows:


```
    1.     public static double calculateColumnTotal(Values2D data, int column) {
    2.         ParamChecks.nullNotPermitted(data, "data");
    3.         double total = 0.0;
    4.         int rowCount = data.getRowCount();
    5.         for (int r = 0; r < rowCount; r++) {
    6.             Number n = data.getValue(r, column);
    7.             if (n != null) {
    8.                 total += n.doubleValue();
    9.             }
    10.         }
    11.         for (int r2 = 0; r2 > rowCount; r2++) {
    12.             Number n = data.getValue(r2, column);
    13.             if (n != null) {
    14.                 total += n.doubleValue();
    15.             }
    16.         }
    17.         return total;
    18.     }
```


<span style="text-decoration:underline;">Data flow graph</span>

Refer to Figure 1 in Images pdf.

<span style="text-decoration:underline;">Def-use sets per statement</span>

DEF(1) := {data, column}, USE(1) :=  {}

DEF(2) := {}, USE(2) := {data}

DEF(3) :=  {}, USE(3) := {total}

DEF(4) := {rowCount}, USE(4) := {data}

DEF(5) := {r}, USE(5) := {r, rowCount}

DEF(6) := {n}, USE(6) := { data, r, column}

DEF(7) :=  {}, USE(7) := {n}

DEF(8) :=  {}, USE(8) := {total, n}

DEF(9) :=  {}, USE(9) :=  {}

DEF(10) :=  {}, USE(10) :=  {}

DEF(11) := {r2}, USE(11) := {r2, rowCount}

DEF(12) := {n}, USE(12) := {data, r2, column}

DEF(13) :=  {}, USE(13) := {n}

DEF(14) :=  {}, USE(14) := {total, n}

DEF(15) := {}, USE(15) :=  {}

DEF(16) :=  {}, USE(16) :=  {}

DEF(17) :=  {}, USE(17) := {total}

DEF(18) :=  {}, USE(18) :=  {}

<span style="text-decoration:underline;">DU-pairs per variable</span>


<table>
  <tr>
   <td>Variable (v)
   </td>
   <td>Defined at node (n)
   </td>
   <td>dcu (v,n)
   </td>
   <td>dpu (v,n)
   </td>
   <td>Du pairs
   </td>
  </tr>
  <tr>
   <td>total
   </td>
   <td>1
   </td>
   <td>{3,7,9}
   </td>
   <td>{}
   </td>
   <td>{(1,3),(1,7),(1,9)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{}
   </td>
   <td>{(1,2), (1,5), (5,6), (5,9)}
   </td>
   <td>{(1,1), (1,5)}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{1,2}
   </td>
   <td>{(1,2), (1,5)}
   </td>
   <td>{(1,1), (1,2)}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{1,2,6}
   </td>
   <td>{}
   </td>
   <td>{(1,1), (1,2), (1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{2,6}
   </td>
   <td>{}
   </td>
   <td>{(1,2), (1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{5,6}
   </td>
   <td>{(5,6), (5,9)}
   </td>
   <td>{(5,5), (5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{3}
   </td>
   <td>{(2,3), (2,4)}
   </td>
   <td>{(2,2), (2,3)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{7}
   </td>
   <td>{(6,7), (6,8)}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td>Total Tally
   </td>
   <td>
   </td>
   <td>14
   </td>
   <td>12
   </td>
   <td>18
   </td>
  </tr>
</table>


<span style="text-decoration:underline;">Test case analysis</span>


<table>
  <tr>
   <td>Test Case
   </td>
   <td>Variable
   </td>
   <td>Defined at node
   </td>
   <td>DU pairs covered
   </td>
   <td>DU pairs not covered
   </td>
  </tr>
  <tr>
   <td rowspan="8" >posColSum
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >negColSum
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >zeroColSum
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >dblColSum
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >posInvColIndex
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >negInvColIndex
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,9)}
   </td>
   <td>{(1,3),(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2)}
   </td>
   <td>{(2,3)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
  <tr>
   <td rowspan="8" >singleColSum
   </td>
   <td>total
   </td>
   <td>1
   </td>
   <td>{(1,3),(1,9)}
   </td>
   <td>{(1,7)}
   </td>
  </tr>
  <tr>
   <td>rowCount
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,5)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>r
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>data
   </td>
   <td>1
   </td>
   <td>{(1,1), (1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>column
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
   <td>{(1,6)}
   </td>
  </tr>
  <tr>
   <td>r2
   </td>
   <td>5
   </td>
   <td>{(5,5)}
   </td>
   <td>{(5,6)}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>2
   </td>
   <td>{(2,2), (2,3)}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>n
   </td>
   <td>6
   </td>
   <td>{}
   </td>
   <td>{(6,6), (6,7)}
   </td>
  </tr>
</table>


DU-Pair coverage

From the above table, we know that there are 6 DU paris that is never reached, and they are (1,7) for variable total, (1,6) for variable data, (1,6) for variable column, (5,6) for variable r2, and (6,6) and (6,7) for variable n that is defined at node 6. The reason why these DU pair were not covered is because they involve a node that is part of the infinite loop from line 11 to 16 of the code implementation. Since there are a total of 18 DU pairs and 6 of those are not covered. The DU pair coverage of our test suite is 

DU coverage % = 12/18 = 67% 



Refer to figure 2 in Images doc.


```
1.     public boolean equals(Object obj) {
2.         if (!(obj instanceof Range)) {
3.             return false;
4.         }
5.         Range range = (Range) obj;
6.         if (!(this.lower == range.lower)) {
7.             return false;
8.         }
9.         if (!(this.upper == range.upper)) {
10.             return false;
11.         }
12.         return true;
13.     }
```


def-use sets per statement:

DEF(0) = {}, USE(0) = {}

DEF(1) = {obj}, USE(1) = {}

DEF(2) = {range,lower,upper}, USE(2) = {lower, upper, range}

DEF(3) = {}, USE(3) = {range,obj}

DEF(4) = {}, USE(4) = {range, obj}

DU pairs per variable:


<table>
  <tr>
   <td>variable
   </td>
   <td>Defined at node
   </td>
   <td>vcu
   </td>
  </tr>
  <tr>
   <td>obj
   </td>
   <td>1
   </td>
   <td>{(1,2)}
   </td>
  </tr>
  <tr>
   <td>upper
   </td>
   <td>2
   </td>
   <td>{(2,4)}
   </td>
  </tr>
  <tr>
   <td>lower
   </td>
   <td>2
   </td>
   <td>{(2,3)}
   </td>
  </tr>
  <tr>
   <td>range
   </td>
   <td>2
   </td>
   <td>{(2,3), (2,3)}
   </td>
  </tr>
</table>


pairs covered per test case:


<table>
  <tr>
   <td>Test case
   </td>
   <td>Covered pairs
   </td>
  </tr>
  <tr>
   <td>sameRangeTrue()
   </td>
   <td>(1,2), (1,1)
   </td>
  </tr>
  <tr>
   <td>sameLBRange()
   </td>
   <td>(2,3), (1,2),(2,2)
   </td>
  </tr>
  <tr>
   <td>sameUBRange()
   </td>
   <td>(2,4),(1,2),(2,2)
   </td>
  </tr>
  <tr>
   <td>oneNullRange()
   </td>
   <td>(1,2), (1,1)
   </td>
  </tr>
</table>


DU pair coverage:

PU total: 3

CU total: 0

PU per test: 3, 0 infeasable

CU per test: 0, 0 infeasable 

DU coverage = (CUc +PUc)/ ((CU +PU) - (CUf +PUf)

                      = (3+0) / ((3+0) - (0+0))

                      = 100%



3. A detailed description of the testing strategy for the new unit test

    For our strategy, we fist ran the coverage tool using our old test cases from the previous assignment to get a understanding of the completeness of our existing test cases. We prioritized our focus on methods that have no test cases developed or have very low statement and/or branch coverage. Since we now have the code implementation and doing white box testing, we examined the data flow of the variables and try to create test cases that capture the most def-use pairs for each variable.


    In terms of delegating of tasks, we have two members working on the Range class and two members working on DataUtilities. For the range class, in addition to the previous test cases developed for assignment 2, Sukriti will create test cases for contains, intersects, constrain, combine, and hashcode; and Caroline will create test cases for constrain, isNaNRange, combineIgnoringNaN, expand, expandToInclude, and toString. These methods ensured that the code coverage will span all types of caes include edge cases so that we can maximize our code coverage for range class. 


    For the DataUtilities class, Dhyey & Fanny worked on adding more test cases for the methods included in assignment 2 while also accounting for null inputs. 


    The test cases developed ensured that we cover different cases and different ways of approaching inputs (such as no number inputs and null inputs). This allowed us to be as comprehensive as possible, which ensured that we received a high code coverage. 

4. A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage

    For the Range class, three of the methods that we didn’t include in assignment 2 were toString, combine, and constrain. Without these three methods included in our testing, we had an overall code coverage of 26.1%. After careful consideration and brainstorming, we have noticed that these three methods use the variables for the upper and lower bounds. This meant that some calculations were not accounted for in the methods we tested in assignment 2. When we included test cases for these 3 (among others) in our range class, our overall code coverage has jumped to 100%, showing that our plan was effective in covering all required cases from different methods. 


    1. For the combine method, we created a test case calledtestCombineFirstRangeNull() to test if combining a range with null with another range that contains values will give the correct new range or not. 


    2. For the toString method, we created rangeTestToString() to see if it will return the range as a string or not, keeping the same upper and lower bounds correctly. 


    3. As for the constrain method, we created a test case called valueInConstraintRange() to test if a value is within a specific range. 


    4. For method DataUtilities.calculateColumnTotal(), having seen the code implementation and the coverage information, in an attempt to get 100% statement coverage, we were able to identify an infeasible path in the code. Without using statement coverage, we may not be able to identify this “defect” in the implementation, as it doesn’t negatively impact the output. 


    5. For method DataUtilities.createNumberArray(), after examining the coverage information and identifying statements where none of the test cases covers, we created test cases that contained null inputs to increase code coverage.

5. A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)

**For all coverage images, please refer to figure 3 in Images doc.**

We were not able to achieve 100% method coverage because DataUtilities is an abstract class, and we were not able to create an instance of the class. Since the constructor is not called, EclEmma doesn't consider that as 100% method coverage.

We were not able to achieve 90% statement coverage for DataUtilities because there are infeasible paths of the implementation. For example in calcualteRowTotal, the second for loop is a infinite loop where r2 is incremented indefinitely. We couldn't create a test case that will enter the infinite loop, therefore there is no line coverage for that loop. In calculateColumnTotal(Values2D data, int column,int[] validRows), there is an infeasible if statement. The part of the implementation is as such:


```
        double total = 0.0;
        if (total > 0){
            total = 100;
        }
```


Since total is defined as 0, the if statement followed immediate with the condition total > 0 is never entered.



6. Pros and Cons of coverage tools used and Metrics you report

    <span style="text-decoration:underline;">Comparison of coverage tools:</span>


Eclemma:


Pros:

* Unit testing
* Color coded explanations of teste
* Built into eclipse, easy to run
* Real time code coverage

Cons:

* Difficult to set up
* No condition coverage 
* Limited functionalities
* Doesn’t have condition coverage

 JaCoCo:


Pros:

* Can be used variety of tools, not confined to just eclipse
* More comprehensive coverage analysis

Cons:

* More advanced UI, a bit more difficult to understand
* The name is difficult to pronounce for people with accents

    Statement coverage measures the number of statements your test suite covers. A higher percentage means that more statements in your code has been covered. A pro of this is that it’s easy to implement and understand. However, it has limited scope and does not accurately reflect the number of paths covered in your code.


    Branch coverage measures the number of branches in your code that have been covered. Each branch is a point where the code has to make a decision, so for example, an _if_ statement would have two branches. The higher the branch coverage percentage, the more branches you have covered in your code. A pro is that this is quite comprehensive, therefore representing the test suite more accurately. Unfortunately, this is a bit more complicated to understand and requires more test cases and inputs. 


    Method coverage refers to the percentage of methods that have been covered by the test suite. A pro is that this is more comprehensive than both statement and  branch coverage, it ensures all methods have been covered. However, this is even more complex and requires a heftier test suite.

7. A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

    One advantage of requirement-based test generation is that it’s intuitive and tests the actual functionality of the code. By testing the software against the specified requirements, it ensures that the software meets the intended functionality. The disadvantage of Requirements-based test generation is its limited test coverage: Requirements-based testing may not test all the possible scenarios and combinations that the software may encounter in real-world usage. It also requires a well-defined and complete set of requirements, and it’s reliant on the creation and development of good requirements documentation to have effective testing.


    The advantage of coverage-based testing is that it’s more complete, less bias, and considers more boundary scenarios. Coverage-based testing can help to ensure that all the possible paths and conditions in the software have been tested. The disadvantage is that it may not capture any functional defects. Even if a program passes 100% of coverage tests, it still may not perform the functional requirements. Focusing too much on code coverage may result in overlooking other important aspects of testing, such as functional testing, usability testing, and performance testing. It is also resource intensive, time-consuming and expensive.

8. A discussion on how the team work/effort was divided and managed

    The group was divided in the same fashion it was divided for assignment 2. Caroline & Sukriti worked on improving the Range class, Fanny & Dhyey worked on improving DataUtilities class. After both groups were done with their parts, each group explained what they did and how they had improved the code coverage for the class. We set internal deadlines to when each part should be done to account for any troubleshooting and editing that would be done. The whole team collectively worked on the report and each added their insight and what they worked on in detail.

9. Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

    One challenge we had is that the library files included in assignment 3 didn’t include the hamcrest library, and the verison of hamcrest-core is different from assignment 2. Due to these library issues, the matcher methods and mock methods were not compatible between assignments. Trying to identify the error and resolve the issue is challenging and a good learning experience.


    We also had difficulties trying to achieve 100% method coverage for DataUtilities, since the class is abstract, the inability to instantiate the class and therefore couldn’t call the constructor resulted in only 90% method coverage, and we as a group struggled to identify the cause.


    There was a lot of overhead in the set up of the coverage tooling. Due to the various configuration options each coverage tooling provided, it took a lot of time to learn and set the correct configurations for our use case. We were able to overcome this simply through extended research and trial-and-error, learning the valuable lesson that sometimes things just take time. 


    We also had difficulties tring to locate a tool that would provide condition coverage. We experimented with both EclEmma and JaCoCo, and were unable to calculate condition coverage. We ended up switching condition coverage to method coverage and used EclEmma as our coverage tool. 

10. Comments/feedback on the lab itself

    The assignment was an interesting and exciting introduction to white-box testing. We have learned how white-box testing gives us access to more information about the code which helped us design our test cases better and fix anything that we couldn’t fix with black-box testing. The lab document was very comprehensive in explaining what needs to be done. Overall, we learned a lot about the importance of testing and how to create effective test cases that would directly increase code coverage for a better code. 


**Test Cases Developed**

<span style="text-decoration:underline;">Range Class Test Suite</span>


<table>
  <tr>
   <td><strong>TC#</strong>
   </td>
   <td><strong>Test Case Name</strong>
   </td>
   <td><strong>Function under</strong>
<p>
<strong>test</strong>
   </td>
   <td><strong>Input(2 Range objects)</strong>
   </td>
   <td><strong>Expected Output</strong>
   </td>
  </tr>
  <tr>
   <td>1
   </td>
   <td>sameRangeTrue
   </td>
   <td>Equals
   </td>
   <td>(-100,-80) and
<p>
(-100,-80)
   </td>
   <td>True
   </td>
  </tr>
  <tr>
   <td>2
   </td>
   <td>sameLBRange
   </td>
   <td>Equals
   </td>
   <td>(100,1000) and
<p>
(100,150)
   </td>
   <td>False
   </td>
  </tr>
  <tr>
   <td>3
   </td>
   <td>sameUBRange
   </td>
   <td>Equals
   </td>
   <td>(100,1000) and
<p>
(20,1000)
   </td>
   <td>False
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>oneNullRange
   </td>
   <td>Equals
   </td>
   <td>(-100,1000) and
<p>
null
   </td>
   <td>False
   </td>
  </tr>
  <tr>
   <td>5
   </td>
   <td>negativeLowerBound
   </td>
   <td>getLowerBound
   </td>
   <td>(-100,-80)
   </td>
   <td>-100
   </td>
  </tr>
  <tr>
   <td>6
   </td>
   <td>positiveLowerBound
   </td>
   <td>getLowerBound
   </td>
   <td>(100,1000)
   </td>
   <td>100
   </td>
  </tr>
  <tr>
   <td>7
   </td>
   <td>LowerBoundWhenEqualToUpperBound
   </td>
   <td>getLowerBound
   </td>
   <td>(1,1)
   </td>
   <td>1
   </td>
  </tr>
  <tr>
   <td>8
   </td>
   <td>smallestLowerBound
   </td>
   <td>getLowerBound
   </td>
   <td>(4.9E-324, 7)
   </td>
   <td>4.9E-324
   </td>
  </tr>
  <tr>
   <td>9
   </td>
   <td>largestLowerBound
   </td>
   <td>getLowerBound
   </td>
   <td>(1.7976931348623157E308, 1.7976931348623157E308)
   </td>
   <td>1.7976931348623157E308
   </td>
  </tr>
  <tr>
   <td>10
   </td>
   <td>lowerBoundIsZero
   </td>
   <td>getLowerBound
   </td>
   <td>(0,1000)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>11
   </td>
   <td>lowerBoundIsAFloat
   </td>
   <td>getLowerBound
   </td>
   <td>(1.234,7.899)
   </td>
   <td>1.234
   </td>
  </tr>
  <tr>
   <td>12
   </td>
   <td>negativeUpperBound
   </td>
   <td>getUpperBound
   </td>
   <td>(-100,-80)
   </td>
   <td>-80
   </td>
  </tr>
  <tr>
   <td>13
   </td>
   <td>positiveUpperBound
   </td>
   <td>getUpperBound
   </td>
   <td>(100,1000)
   </td>
   <td>1000
   </td>
  </tr>
  <tr>
   <td>14
   </td>
   <td>UpperBoundWhenEqualToLowerBound
   </td>
   <td>getUpperBound
   </td>
   <td>(1,1)
   </td>
   <td>1
   </td>
  </tr>
  <tr>
   <td>15
   </td>
   <td>smallestUpperBound
   </td>
   <td>getUpperBound
   </td>
   <td>(4.9E-324,4.9E-32)
   </td>
   <td>4.9E-32
   </td>
  </tr>
  <tr>
   <td>16
   </td>
   <td>largestUpperBound
   </td>
   <td>getUpperBound
   </td>
   <td>(4.9E-324,1.7976931348623157E308)
   </td>
   <td>1.7976931348623157E308
   </td>
  </tr>
  <tr>
   <td>17
   </td>
   <td>upperBoundisZero
   </td>
   <td>getUpperBound
   </td>
   <td>(-1000,0)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>18
   </td>
   <td>upperBoundisFloat
   </td>
   <td>getUpperBound
   </td>
   <td>(1.234,7.899)
   </td>
   <td>7.899
   </td>
  </tr>
  <tr>
   <td>19
   </td>
   <td>negPosIntsTest
   </td>
   <td>getLength
   </td>
   <td>(-50,50)
   </td>
   <td>100
   </td>
  </tr>
  <tr>
   <td>20
   </td>
   <td>positiveIntsTest
   </td>
   <td>getLength
   </td>
   <td>(5, 100)
   </td>
   <td>95
   </td>
  </tr>
  <tr>
   <td>21
   </td>
   <td>negativeIntsTest
   </td>
   <td>getLength
   </td>
   <td>(-100,-5)
   </td>
   <td>95
   </td>
  </tr>
  <tr>
   <td>22
   </td>
   <td>zeroTest
   </td>
   <td>getLength
   </td>
   <td>(0,0)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>23
   </td>
   <td>zeroWithIntTest
   </td>
   <td>getLength
   </td>
   <td>(0,10)
   </td>
   <td>10
   </td>
  </tr>
  <tr>
   <td>24
   </td>
   <td>negPosFloatTest
   </td>
   <td>getLength
   </td>
   <td>(-3.457,8.535)
   </td>
   <td>11.992
   </td>
  </tr>
  <tr>
   <td>25
   </td>
   <td>negFloatTest
   </td>
   <td>getLength
   </td>
   <td>(-7.442,-5.632)
   </td>
   <td>1.81
   </td>
  </tr>
  <tr>
   <td>26
   </td>
   <td>posFloatTest
   </td>
   <td>getLength
   </td>
   <td>(6.424,9.324)
   </td>
   <td>2.9
   </td>
  </tr>
  <tr>
   <td>27
   </td>
   <td>zerowithNegIntTest
   </td>
   <td>getLength
   </td>
   <td>(-10,0)
   </td>
   <td>10
   </td>
  </tr>
  <tr>
   <td>28
   </td>
   <td>negPosIntsCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(-50,50)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>29
   </td>
   <td>positiveIntCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(5, 100)
   </td>
   <td>52.5
   </td>
  </tr>
  <tr>
   <td>30
   </td>
   <td>negativeIntsCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(-100,-5)
   </td>
   <td>-52.5
   </td>
  </tr>
  <tr>
   <td>31
   </td>
   <td>zeroNumCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(0,0)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>32
   </td>
   <td>zeroWithIntCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(0,10)
   </td>
   <td>5
   </td>
  </tr>
  <tr>
   <td>33
   </td>
   <td>negPosFloatCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(-3.457,8.535)
   </td>
   <td>2.539
   </td>
  </tr>
  <tr>
   <td>34
   </td>
   <td>negativeFloatCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(-7.442,-5.632)
   </td>
   <td>-6.537
   </td>
  </tr>
  <tr>
   <td>35
   </td>
   <td>positiveFloatCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(6.424,9.324)
   </td>
   <td>7.874
   </td>
  </tr>
  <tr>
   <td>36
   </td>
   <td>zeroWithNegIntCentralValueTest
   </td>
   <td>getCentralValue
   </td>
   <td>(-10,0)
   </td>
   <td>-5
   </td>
  </tr>
</table>


The above test suite was for assignment 2. To expand our new test suite, we followed a similar approach for all the methods, including edge cases and null ranges.

<span style="text-decoration:underline;">Data Utilites Class Test</span>

Stub for input data (Values2D): values1


<table>
  <tr>
   <td>1
   </td>
   <td>3
   </td>
   <td>3
   </td>
   <td>1
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>-6
   </td>
   <td>2
   </td>
   <td>2
   </td>
  </tr>
  <tr>
   <td>7
   </td>
   <td>1
   </td>
   <td>0
   </td>
   <td>3
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>1
   </td>
   <td>2
   </td>
   <td>3.0
   </td>
  </tr>
</table>


Stub for input data (Values2D): values2


```
2
```


Test suite for calculateColumnTotal(Values2D data, int column)


<table>
  <tr>
   <td>TC#
   </td>
   <td>Test Name
   </td>
   <td>Method under test
   </td>
   <td>Input data
   </td>
   <td>Input Column
   </td>
   <td>Expected output
   </td>
  </tr>
  <tr>
   <td>1
   </td>
   <td>posColSum
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1
   </td>
   <td>0 (contains all positive entries)
   </td>
   <td>16
   </td>
  </tr>
  <tr>
   <td>2
   </td>
   <td>negColSum
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1
   </td>
   <td>1 (Column contains negative entry)
   </td>
   <td>-1
   </td>
  </tr>
  <tr>
   <td>3
   </td>
   <td>zeroColSum
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1
   </td>
   <td>2(Column contains zero as entry)
   </td>
   <td>7
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>dblColSum
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1 
   </td>
   <td>3 (Column contains entry of type zero)
   </td>
   <td>9.0
   </td>
  </tr>
  <tr>
   <td>5
   </td>
   <td>posInvColIndex
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1
   </td>
   <td>4 (Positive index out of bound)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>6
   </td>
   <td>negInvColIndex
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values1
   </td>
   <td>-1 (Negative index out of bound)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>7
   </td>
   <td>singleColSum
   </td>
   <td>calculateColumnTotal(Values2D data, int column)
   </td>
   <td>values2
   </td>
   <td>0 (only 1 column)
   </td>
   <td>2
   </td>
  </tr>
</table>


Test suite for calculateColumnTotal(Values2D data, int column)


<table>
  <tr>
   <td>TC#
   </td>
   <td>Test Name
   </td>
   <td>Method under test
   </td>
   <td>Input data
   </td>
   <td>Input Column
   </td>
   <td>Expected output
   </td>
  </tr>
  <tr>
   <td>8
   </td>
   <td>posRowSum
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1
   </td>
   <td>0 (contains all positive entries)
   </td>
   <td>8
   </td>
  </tr>
  <tr>
   <td>9
   </td>
   <td>negRowSum
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1
   </td>
   <td>1 (row contains negative entry)
   </td>
   <td>2
   </td>
  </tr>
  <tr>
   <td>10
   </td>
   <td>zeroRowSum
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1
   </td>
   <td>2(row contains zero as entry)
   </td>
   <td>11
   </td>
  </tr>
  <tr>
   <td>11
   </td>
   <td>dblRowSum
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1 
   </td>
   <td>3 (row contains entry of type zero)
   </td>
   <td>10.0
   </td>
  </tr>
  <tr>
   <td>12
   </td>
   <td>posInvRowIndex
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1
   </td>
   <td>4 (Positive index out of bound)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>13
   </td>
   <td>negInvRowIndex
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values1
   </td>
   <td>-1 (Negative index out of bound)
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>14
   </td>
   <td>singleRowSum
   </td>
   <td>calculateRowTotal(Values2D data, int row)
   </td>
   <td>values2
   </td>
   <td>0 (only 1 row)
   </td>
   <td>2
   </td>
  </tr>
</table>


Test suite for calculateColumnTotal(Values2D data, int column, int[] validRows)


<table>
  <tr>
   <td>TC#
   </td>
   <td>Test Name
   </td>
   <td>Method under test
   </td>
   <td>Input data
   </td>
   <td>Input Column
   </td>
   <td>validRows
   </td>
   <td>Expected output
   </td>
  </tr>
  <tr>
   <td>15
   </td>
   <td>posColSumArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1
   </td>
   <td>0 (contains all positive entries)
   </td>
   <td>{0,1}
   </td>
   <td>5.0
   </td>
  </tr>
  <tr>
   <td>16
   </td>
   <td>negColSumArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1
   </td>
   <td>1 (Column contains negative entry)
   </td>
   <td>{0,1}
   </td>
   <td>-3.0
   </td>
  </tr>
  <tr>
   <td>17
   </td>
   <td>zeroColSumArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1
   </td>
   <td>2(Column contains zero as entry)
   </td>
   <td>{0,2}
   </td>
   <td>3.0
   </td>
  </tr>
  <tr>
   <td>18
   </td>
   <td>dblColSumArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1 
   </td>
   <td>3 (Column contains entry of type zero)
   </td>
   <td>{0,3}
   </td>
   <td>4.0
   </td>
  </tr>
  <tr>
   <td>19
   </td>
   <td>posInvColIndexArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1
   </td>
   <td>4 (Positive index out of bound)
   </td>
   <td>{0,1}
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>20
   </td>
   <td>negInvColIndexArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values1
   </td>
   <td>-1 (Negative index out of bound)
   </td>
   <td>{0,1}
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>21
   </td>
   <td>singleColSumArr
   </td>
   <td>calculateColumnTotal(Values2D data,
<p>
 int column,
<p>
 int[] validRows)
   </td>
   <td>values2
   </td>
   <td>0 (only 1 column)
   </td>
   <td>{0}
   </td>
   <td>2
   </td>
  </tr>
</table>


Test suite for calculateRowTotal(Values2D data, int row, int[] validCols)


<table>
  <tr>
   <td>TC#
   </td>
   <td>Test Name
   </td>
   <td>Method under test
   </td>
   <td>Input data
   </td>
   <td>Input Column
   </td>
   <td>ValidCols
   </td>
   <td>Expected output
   </td>
  </tr>
  <tr>
   <td>22
   </td>
   <td>posRowSumArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1
   </td>
   <td>0 (contains all positive entries)
   </td>
   <td>{0,1}
   </td>
   <td>4
   </td>
  </tr>
  <tr>
   <td>23
   </td>
   <td>negRowSumArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1
   </td>
   <td>1 (row contains negative entry)
   </td>
   <td>{0,1}
   </td>
   <td>-2
   </td>
  </tr>
  <tr>
   <td>24
   </td>
   <td>zeroRowSumArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1
   </td>
   <td>2(row contains zero as entry)
   </td>
   <td>{0,2}
   </td>
   <td>7
   </td>
  </tr>
  <tr>
   <td>25
   </td>
   <td>dblRowSumArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1 
   </td>
   <td>3 (row contains entry of type zero)
   </td>
   <td>{0,3}
   </td>
   <td>7.0
   </td>
  </tr>
  <tr>
   <td>26
   </td>
   <td>posInvRowIndexArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1
   </td>
   <td>4 (Positive index out of bound)
   </td>
   <td>{0,1}
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>27
   </td>
   <td>negInvRowIndexArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values1
   </td>
   <td>-1 (Negative index out of bound)
   </td>
   <td>{0,1}
   </td>
   <td>0
   </td>
  </tr>
  <tr>
   <td>28
   </td>
   <td>singleRowSumArr
   </td>
   <td>calculateRowTotal(Values2D data,
<p>
 int row,
<p>
 int[] validCols)
   </td>
   <td>values2
   </td>
   <td>0 (only 1 row)
   </td>
   <td>{0}
   </td>
   <td>2
   </td>
  </tr>
</table>


Test suite for createNumberArray()


<table>
  <tr>
   <td>TC #
   </td>
   <td>Test Name
   </td>
   <td>Method under test
   </td>
   <td>Input
   </td>
   <td>Expected Output
   </td>
  </tr>
  <tr>
   <td>29
   </td>
   <td>testCreateNumberArray
   </td>
   <td>creatNumberArray
   </td>
   <td>{1.0, 2.0, 3.0}
   </td>
   <td>{1.0, 2.0, 3.0}
   </td>
  </tr>
  <tr>
   <td>30
   </td>
   <td>testCreateNumberArrayWithEmptyArray
   </td>
   <td>creatNumberArray
   </td>
   <td>{}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>31
   </td>
   <td>testCreateNumberArray2d
   </td>
   <td>creatNumberArray2D
   </td>
   <td>{{1.0, 2.0, 3.0}, {1.0, 2.0, 3.0}}
   </td>
   <td>{{1.0, 2.0, 3.0}, {1.0, 2.0, 3.0}}
   </td>
  </tr>
  <tr>
   <td>32
   </td>
   <td>testCreateNumberArray2dWithEmptyArray
   </td>
   <td>creatNumberArray2D
   </td>
   <td>{{}}
   </td>
   <td>{{}}
   </td>
  </tr>
  <tr>
   <td>33
   </td>
   <td>testCreateNumberArrayWithNullInput
   </td>
   <td>createNumberArray
   </td>
   <td>null
   </td>
   <td>InvalidParameterException
   </td>
  </tr>
  <tr>
   <td>34
   </td>
   <td>testCreateNumberArray2dWithNullInput
   </td>
   <td>createNumberArray2D
   </td>
   <td>null
   </td>
   <td>InvalidParameterException
   </td>
  </tr>
  <tr>
   <td>35
   </td>
   <td>testGetCumulativeAveragesNull
   </td>
   <td>getCumulativeAverages
   </td>
   <td>null
   </td>
   <td>InvalidParameterException
   </td>
  </tr>
</table>


Test suite for getCumulativeAverages()


<table>
  <tr>
   <td>TC #
   </td>
   <td>Test name
   </td>
   <td>Input (KeyedValues mock)
   </td>
   <td>Expected Output
   </td>
  </tr>
  <tr>
   <td>36
   </td>
   <td>testGetCumulativeAverages
   </td>
   <td>{5.0, 9.0, 2.0}
   </td>
   <td>{0.3125, 0.875, 1.0}
   </td>
  </tr>
  <tr>
   <td>37
   </td>
   <td>testGetCumulativeAveragesEmptyKeys
   </td>
   <td>{}
   </td>
   <td>{}
   </td>
  </tr>
  <tr>
   <td>38
   </td>
   <td>testGetCumulativePercentagesNull
   </td>
   <td>null
   </td>
   <td>InvalidParameterException
   </td>
  </tr>
</table>


Test suite for clone(double[][] source)


<table>
  <tr>
   <td>TC #
   </td>
   <td>Test name
   </td>
   <td>Input ()
   </td>
   <td>Expected Output
   </td>
  </tr>
  <tr>
   <td>39
   </td>
   <td>testClone
   </td>
   <td>
   </td>
   <td>
   </td>
  </tr>
</table>


Test suite for equals(double[][] a, double[][] b)


<table>
  <tr>
   <td>TC #
   </td>
   <td>Test name
   </td>
   <td>Input
   </td>
   <td>Expected Output
   </td>
  </tr>
  <tr>
   <td>40
   </td>
   <td>testEqualABNull
   </td>
   <td>a=null, b=null
   </td>
   <td>true
   </td>
  </tr>
  <tr>
   <td>41
   </td>
   <td>testEqualBNull
   </td>
   <td>a={{1.0}}, b=null
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>42
   </td>
   <td>testDifferentLengthAB
   </td>
   <td>a={{1.0},{2.0}}, b={{1.0}}
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>43
   </td>
   <td>testDifferentValuesAB
   </td>
   <td>a={{1.0}}, b={{2.0}}
   </td>
   <td>false
   </td>
  </tr>
  <tr>
   <td>44
   </td>
   <td>testSameValuesAB
   </td>
   <td>a={{1.0, 2.0}, {3.0}}, b={{1.0, 2.0}, {3.0}}
   </td>
   <td>true
   </td>
  </tr>
</table>

