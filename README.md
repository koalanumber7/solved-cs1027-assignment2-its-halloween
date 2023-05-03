Download Link: https://assignmentchef.com/product/solved-cs1027-assignment2-its-halloween
<br>
To gain experience with

<ul>

 <li>Solving problems with the stack data type</li>

 <li>The design of algorithms in pseudocode and their implementations in Java</li>

 <li>Handling exceptions</li>

</ul>




<h1>Introduction</h1>




It’s Halloween! You know what that means, right? It’s time to go trick-or-treating! With all the restrictions in place this year, it’s more important than ever to plan out the ideal routes. To minimize the number of people on the doorsteps at once, everyone has agreed to only trick-ortreat for so long and to take turns. The hero of our assignment, Bryan the Bold, needs your help making sure that his friends and him can collect as much candy as possible before their designated trick-or-treating time ends. He brought a map of the neighbourhoods he’s going to go trick or treating in and heard that you’ve been studying some computer science recently that will help him plan this all out. To help Bryan the Bold out, you will create a Java program to help him navigate the neighbourhood. The program needs to determine whether Bryan or a friend can reach enough candy to fill his bag from a starting point on the map, given a maximum distance from the start point (Bryan and friends can only run so fast!).

You are given a map of the neighbourhood, which is divided into rectangular cells to simplify the task of computing the required path. There are different types of map cells:

<ul>

 <li>The starting point that Bryan wants to use</li>

 <li>Map cells where the candy is located,</li>

 <li>Map cells indicating roadblocks or other barriers</li>

 <li>Map cells containing pathways. There are 3 types of pathways:

  <ul>

   <li>Cross paths. A cross path located in cell L can be used to interconnect all the neighbouring map cells of L. A cell L has at most 4 neighbouring cells that we denote as the north, south, east, and west neighbours. The cross path can be used to interconnect all neighbours of L;</li>

   <li>Vertical paths. A vertical path can be used to connect the north and south neighbours of a map cell; and</li>

   <li>Horizontal paths. A horizontal path can be used to connect the east and west neighbours of a map cell.</li>

  </ul></li>

</ul>

Map cells containing candy are allowed to function like cross paths; Bryan the Bold can sneak through backyards if need be (but not road blocks).

<strong>Figure 1</strong> shows an example of a map divided into cells.




Each map cell has up to 4 neighbouring cells indexed from 0 to 3.




Given a cell, the north neighbouring cell has index 0 and the remaining neighbouring cells are indexed in clockwise order. For example, in Figure 1 the neighbouring cells of cell 8 are indexed from 0 to 3 as follows: neighbour with index 0 1 is cell 5, neighbour with index 1 is cell 9, neighbour with index 2 is cell 11, and neighbour with index 3 is cell 7 (note that even though there are 4 neighbours, only 2 of them are accessible: cell 5 and cell 11, because cell 8 is a vertical path and thus does not connect on the east or west sides).




Some cells have fewer than 4 neighbours and the indices of these neighbours might not be consecutive numbers; for example, cell 6 in Figure 1 has 2 neighbours indexed 1 and 2 (no 0 or 3 neighbours).




A path from Bryan (cell number 1 in the figure) to a candy (cell number 7) is the following:

1, 2, 3, 4, 5, 6, 7. A path from Bryan to another candy (cell number 10) is the following: 1, 2, 3, 4, 9, 10. Notice that the two other candies in the figure are inaccessible because of the path types of their neighbouring cells.




<h1>Valid Paths</h1>

When looking for a path the program must satisfy the following conditions:

<ul>

 <li>The path can go from Bryan, a cross path cell, or a candy cell to the following neighbouring cells: o A candy cell, o A cross path cell,

  <ul>

   <li>The north cell or the south cell, if such a cell is a vertical path, or o The east cell or the west cell, if such a cell is a horizontal path.</li>

  </ul></li>

</ul>




<ul>

 <li>The path can go from a vertical path cell to the following neighbouring cells:

  <ul>

   <li>The north cell or the south cell, if such a cell is either Bryan, a cross path cell, a candy cell, or a vertical path cell.</li>

  </ul></li>

 <li>The path can go from a horizontal path cell to the following neighbouring cells:

  <ul>

   <li>The east cell or the west cell, if such a cell is either Bryan, a cross path cell, a</li>

  </ul></li>

</ul>

candy cell, or a horizontal path cell.







<strong>Figure 1</strong>. A sample of one of Bryan’s neighbourhood maps represented as a grid of cells

<strong> </strong>

<strong>Limitation:</strong>

If while looking for a path the program finds that from the current cell there are several choices as to which adjacent cell to use to continue the path, your program must select the next cell for the path in the following manner:




<ul>

 <li>The program prefers a candy cell over the other cells.</li>

 <li>If there is no candy cell adjacent to the current cell, then the program must prefer the cross path cell over the other cells; and</li>

 <li>If there is no cross-path cell, then the program chooses the smallest indexed cell that satisfies the conditions described above.</li>

 <li>When considering path length, adding a new cell to the stack or removing a cell from the stack counts as adding to the path length; Bryan takes time to move to and from a cell.</li>

</ul>

<h1>Provided files</h1>




The following is a list of files provided to you for this assignment. You do not need alter these files in any way and should assume we will mark them with unmodified ones. Studying these will help improve your understanding of Java.

<ul>

 <li>java – This class represents the map of the neighbourhood, including Bryan’s starting location and the candy houses. The public methods from this class you might use include:</li>

</ul>




<ul>

 <li><em>Map (String inputFile) throws InvalidMapException, FileNotFoundException, IOException</em>. This method reads the input file and displays the map on the screen. An <em>InvalidMapException</em> is thrown if the <em>inputFile</em> has the wrong format.</li>

 <li><em>MapCell getStart()</em>. Returns a <em>MapCell</em> object for the cell that Bryan starts in.</li>

 <li><em>Int bagSize()</em>. Returns the number of candies that can fit in Bryan’s bag.</li>

 <li><strong>Note: </strong>Lines 45-47 set the delay times for showing the path. You may wish to enable line 47 when testing many maps to have it go quicker.</li>

</ul>




<ul>

 <li>java – This class represents the cells of the map. Objects of this class are created inside the class <em>Map</em> when its constructor reads the map file. The methods that you might use from this class are:</li>

</ul>




<ul>

 <li><em>MapCell neighbourCell(int i) throws InvalidNeighbourIndexException</em>. As explained in Section 1, each cell of the map has up to four neighbouring cells, indexed from 0 to 3. This method returns either a <em>MapCell</em> object representing the i-th neighbour of the current cell or null if such a neighbour does not exist. Remember that if a cell has fewer than 4 neighbouring cells, these neighbours do not necessarily need to appear at consecutive index values. So, it might be, for example, that <em>getNeighbour(2)</em> is null, but <em>this.getNeighbour(i)</em> for all other values of i are not null. An <em>InvalidNeighbourIndexException</em> exception is thrown if the value of the parameter i is negative or larger than 3.</li>

</ul>




<ul>

 <li>boolean methods:<em> isBlocked(), isCrossPath(), isVerticalPath(), isHorizontalPath(), isBryan(), isCandy(),</em> return true if this <em>MapCell</em> object represents a cell corresponding to a blocked path, a cross path, a vertical path, a horizontal path, Bryan, or a candy respectively.</li>

 <li><em>boolean isMarked()</em> returns true if this MapCell object represents a cell that has been marked as <em>inStack</em> or</li>

 <li><em>void markInStack() </em>marks this<em> MapCell </em>object as</li>

 <li><em>void markOutStack() </em>marks this<em> MapCell </em>object as</li>

</ul>

<em> </em>

<em> </em>

<ul>

 <li>Other classes provided:

  <ul>

   <li><em>java, CellColors.java, CellComponent.java, InvalidNeighbourIndexException.java, CellLayout.java, </em></li>

  </ul></li>

</ul>

<em>InvalidMapException.java, IllegalArgumentException.java. </em>

<h1>Classes to implement</h1>




A description of the classes that you are required to implement for full marks in this assignment are given below. You may implement more classes if you want; you must submit the code for these with your assignment.

In all these classes, you may implement more private (helper) methods as desired, but you may<strong> not</strong> implement more public methods. You may<strong> not</strong> add static methods or instance variables. Penalties will be applied if you implement these.

For this assignment, you may not use Java’s <em>Stack</em> class, although reading and understanding the code there may help you better understand stacks. You also may not use any other premade Java collections libraries. The data structure required for this assignment is an array, described below:




<h2>ArrayStack.java</h2>




This class implements a stack using an array. The header for this class must be this:




<em>public class ArrayStack&lt;T&gt; implements ArrayStackADT&lt;T&gt;</em>

<em> </em>




This class will have the following private instance variables:

<ul>

 <li>T[] stack.

  <ul>

   <li>This array stores the data items of the stack.</li>

  </ul></li>

</ul>




<ul>

 <li>int top.

  <ul>

   <li>This variable stores the position of the last data item in the stack. In the constructor this variable must be initialized to +1, this means the stack is empty.</li>

   <li>Note that this is different from the way in which the variable top is used in the lecture notes.</li>

  </ul></li>

</ul>




<ul>

 <li>String sequence – used for TestSearch.java</li>

</ul>

This class needs to provide the following public methods:




<ul>

 <li>ArrayStack() o Creates an empty stack.

  <ul>

   <li>The default initial capacity of the array used to store the items of the stack is 5.</li>

  </ul></li>

</ul>




<ul>

 <li>ArrayStack(int initialCapacity).

  <ul>

   <li>Creates an empty stack using an array of length equal to the value of the parameter.</li>

  </ul></li>

</ul>




<ul>

 <li>void push(T dataItem) o Adds dataItem to the top of the stack. If the array storing the data items is full, you will increase its capacity as follows:

  <ul>

   <li>If the capacity of the array is smaller than 50, then the capacity of the array will be increased by a factor of 10.</li>

   <li>Otherwise, the capacity of the array will increase by 50. So, if, for example, the size of the array is 225 and the array is full, when a new item is added the size of the array will increase to 275.</li>

  </ul></li>

</ul>




At the end of this method, at the following. This is used in TestSearch to make sure you are following a correct path.:




if (dataItem instanceof MapCell) {




sequence += “push” + ((MapCell)dataItem).getIdentifier();




}

else {




sequence += “push” + dataItem.toString();




}







<ul>

 <li>T pop() throws EmptyStackException o Removes and returns the data item at the top of the stack. An EmptyStackException is thrown if the stack is empty.  o If after removing a data item from the stack the number of data items remaining is smaller than one fourth of the length of the array and the length of the array is larger than 50 you need to shrink the size of the array by 25;

  <ul>

   <li>To do this create a new array of size equal to half of the size of the original array and copy the data items there.</li>

   <li>For example, if the stack is stored in an array of size 100 and it contains 25 data items, after performing a pop operation the stack will contain only 24 data items. Since 24 &lt; 100/4 then the size of the array will be reduced to 75. When creating an EmptyStackException an appropriate String message must be passed as parameter.</li>

  </ul></li>

</ul>

At the end of pop(), add the following lines:




if (result instanceof MapCell) {




sequence += “pop” + ((MapCell)result).getIdentifier();




}




else {




sequence += “pop” + result.toString();




}







<ul>

 <li>T peek() throws EmptyStackException.

  <ul>

   <li>Returns the data item at the top of the stack without removing it. An EmptyStackException is thrown if the stack is empty.</li>

  </ul></li>

</ul>




<ul>

 <li>boolean isEmpty().

  <ul>

   <li>Returns true if the stack is empty and returns false otherwise.</li>

  </ul></li>

</ul>




<ul>

 <li>int size() o Returns the number of data items in the stack.</li>

</ul>




<ul>

 <li>int length() o Returns the capacity of the array stack.</li>

</ul>




<ul>

 <li>String toString() o Returns a String representation of the stack of the form:</li>

</ul>

“Stack: elem1, elem2, …” where element i is a String representation of the i-th element of the stack.

<ul>

 <li>If, for example, the stack is stored in an array called s, then element 1 is s[0].toString(), element 2 is s[1].toString(), and so on.</li>

</ul>




You can implement other methods in this class, if you want to, but they must be declared as private.

<h2>StartSearch.java</h2>




This class will have the following private instance variable




<ul>

 <li>Map neighbourhoodMap;</li>

 <li>This variable will reference the object representing the neighbourhood map where Bryan and the candies are located. This variable must be initialized in the constructor for the class, as described below.</li>

</ul>




You must implement the following methods in this class:




<ul>

 <li>StartSearch(String filename, int maxPathLength) o This is the constructor for the class. It receives as input the name of the file containing the description of the neighbourhood map. In this method you must create an object of the class Map (described in the provided files) passing as parameter the given input file; this will display the map on the screen.

  <ul>

   <li>Read them if you want to know the format of the input files.</li>

  </ul></li>

 <li>static void main(String[] args).

  <ul>

   <li>This method will first create an object of the class <em>StartSearch</em> using the constuctor <em>StartSearch(args[0]).</em></li>

   <li><em>Args[0] </em>will be the name of a map file, <em>args[1]</em> will be the number of cells that can be traveled to during his designated trick-or-treating time.</li>

   <li>If and only if a size argument is provided, your algorithm should count how many candies can be found in a path that is at most <em>args[1]</em></li>

   <li>Otherwise, it should count how many candies are reachable on the map.</li>

   <li>When you run the program, you will pass as command line arguments the name of the input file (see following section after Java classes), and the number of cells that Bryan can travel from his starting point to find candy. o Your main method then will try to find a path from Bryan to the candies according to the restrictions specified above.</li>

   <li>The algorithm that looks for a path from the initial cell to the destinations must use a stack and it cannot be recursive. o Suggestions on how to look for this path are given in the next section. The code provided to you will show the path selected by the algorithm as it tries to reach the candy cells, so you can visually verify if your program works.</li>

   <li>The main method should exit by printing out the number of candies found given the maximum path length if one is given, and the number of candies discoverable if no maximum path length is given.</li>

  </ul></li>

</ul>







<ul>

 <li>MapCell bestCell(MapCell cell).

  <ul>

   <li>The parameter is the current cell.</li>

   <li>This method returns the best cell to continue the path from the current one, as specified early in the limitations.</li>

   <li>Refer to those priorities when coding this section. o If several unmarked cells are adjacent to the current one and can be selected as part of the path, then this method must return one of them in the following order:

    <ul>

     <li>A candy cell A cross path cell.</li>

     <li>If there are several possible cross path cells, then the one with the smallest index is returned.</li>

     <li>A vertical path cell or a horizontal path cell with smallest index</li>

     <li>Read the description of the class MapCell below to learn how to get the index of a neighbouring cell.</li>

     <li>If there are no unmarked cells adjacent to the current one that can be used to continue the path, this method returns null.</li>

    </ul></li>

   <li>Your program must catch any exceptions that are thrown by the provided code. o For each exception caught, an appropriate message must be printed.</li>

   <li>The message must explain what caused the exception to be thrown.</li>

  </ul></li>

</ul>




You can write more methods in this class but they must be declared as private.




<h1>Algorithm for Computing a Path</h1>

Below is a description for an algorithm that will look for a path for Bryan to the candies. It will be helpful to understand the algorithm deeply before attempting to implement it. There are better algorithms for finding candies given a maximum path length, but they may not pass all the tests. Implement the algorithm as described to make sure your code passes the test cases.

You must use a stack to keep track of which cells are in the path, and it cannot be recursive. Writing your algorithm in pseudocode will make coding it in Java easier and is helpful to show to the TAs and the instructors if you need help.

<ul>

 <li>Initialize the number of found candies to 0.</li>

 <li>Create a stack based on the command line inputs</li>

 <li>Get the start cell (Bryan) using the methods of the supplied class Map.</li>

 <li>Push the starting cell into the stack and mark the cell as inStack.</li>

 <li>You will use methods of the class MapCell to mark a cell.</li>

 <li>While the stack is not empty and Bryan’s bag is not full perform the following steps:

  <ul>

   <li>Peek at the top of the stack to get the current cell.</li>

   <li>Find the best unmarked neighbouring cell (use method bestCell from class StartSearch to do this).</li>

   <li>If one exists:</li>

  </ul></li>

 <li>Push the neighbouring cell into the stack and mark it as inStack.</li>

 <li>(If max path length given) Increase the path length counter</li>

 <li>If the best neighbouring cell is a candy, increase the number of candies found.

  <ul>

   <li>Otherwise, since there are no unmarked neighbouring cells that can be added to the path, pop the top cell (and increase the path length counter) from the stack and mark it as outOfStack.</li>

  </ul></li>

 <li>While the stack is not empty perform the following:

  <ul>

   <li>Pop the top cell from the stack and mark is as outOfStack.</li>

  </ul></li>

</ul>




Your program must print a message indicating how many candies were collected.

Note that your algorithm does not need to find the shortest path from Bryan to all the candies.




<h1>Command Line Arguments</h1>

Your program must read the name of the input map file from the command line.

You can run the program with the following command:

<strong><em>java StartSearch nameOfMapFile (optional)maxPathLength </em></strong>




Where nameOfMapFile is the name of the file containing the desert map, and maxPathLength is the longest path that Bryan can take to find candies.

You can use the following code to verify that the program was invoked with the correct number of arguments:




public class StartSearch { public static void main (String[] args) { if (args.length &lt; 1) {

System.out.println(“You must provide the name of the input file”); System.exit(0);

}

String mapFileName = args[0];

int maxPathLength = Integer.parseInt(args[1]);

…




You can access run configurations as follows:




In the text box for ‘Program arguments’, you can type your arguments in. Ex: map3.txt above, or map3.txt 20 for map 3 with a maximum of 20 steps.

<h1>Image Files and Sample Input Files Provided</h1>

<ul>

 <li>You are given several image files that are used by the provided Java code to display the different kinds of map cells on the screen.</li>

 <li>You are also given several input map files that you can use to test your program.</li>

 <li>In Eclipse put all these files inside your project file in the same folder where the src folder is.</li>

 <li>Do not put them <strong>inside</strong> the src folder as Eclipse will not find them there.</li>

 <li>If your program does not display the map correctly on your monitor, you might need to move these files to another folder, depending on how your installation of Eclipse has been configured.</li>

</ul>

<h1>Marking notes</h1>




Marking categories

<ul>

 <li>Functional specifications o Does the program behave according to specifications? o Does it produce the correct output and pass all tests? o Are the class implemented properly?

  <ul>

   <li>Are you using appropriate data structures?</li>

  </ul></li>

 <li>Non-functional specifications o Are there Javadocs comments and other comments throughout the code? o Are the variables and methods given appropriate, meaningful names? o Is the code clean and readable with proper indenting and white-space?

  <ul>

   <li>Is the code consistent regarding formatting and naming conventions?</li>

  </ul></li>

 <li>Penalties o Lateness: 10% per day

  <ul>

   <li>Submission error (i.e. missing files, too many files, ZIP, etc.): 5% o “package” line at the top of a file: 5%</li>

  </ul></li>

</ul>




Remember you must do all the work on your own. Do not copy or even look at the work of another student. All submitted code will be run through cheating-detection software.


