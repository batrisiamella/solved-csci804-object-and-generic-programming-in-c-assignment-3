Download Link: https://assignmentchef.com/product/solved-csci804-object-and-generic-programming-in-c-assignment-3
<br>
<h1>Task One: Stack and expression (5 marks)</h1>

Human generally write expressions like 3 + 4 and 7 / 9 in which the operator (+ or / here) is written between its operands-this is called <em>infix notation</em>. Computers “prefer” <em>postfix notation</em> in which the operator is written to the right of its two operands. The preceding infix expressions would appear in postfix notation as 3 4 + and 7 9 /, respectively.

To evaluate a complex infix expression, a compiler would first convert the expression to postfix notation and then evaluate the postfix version of the expression. Each of these algorithms requires only a single left-to-right pass of the expression. Each algorithm uses a stack object in support of its operation, and in each algorithm the stack is used for a different purpose.

In this task, you are to write a C++ program of the infix-to-postfix conversion algorithm.

Define and implement a <strong>Stack</strong> template class in a file <strong>stack.h</strong>. Your Stack template class must have the following public functions:

<ul>

 <li>void push(T): to insert a data to the Stack.</li>

 <li>T pop(): to retrive a data from the Stack.</li>

 <li>bool isEmpty(): this function will return 1 if the Stack is empty or 0 otherwise.</li>

 <li>void print() : this function will print the contents of the Stack WITHOUT destroying the contents of the Stack.</li>

 <li>T stackTop() : this function will return the TOP element of the Stack WITHOUT destroying the contents of the original Stack.</li>

</ul>

Define a class called <strong>InfixToPostfix</strong> in a file <strong>postfix.h</strong>, which is able to convert an infix notation to a postfix notation. The class has two private variables:

string infix;

string postfix;

These variables are used to hold the infix and postfix notations, respectively.




Define the following public member functions for the class <strong>InfixToPostfix</strong>:

<ul>

 <li>void setInfix(const std::string &amp;) : This is a function to set initial value to the data member <em>infix</em>.</li>

 <li>void convert (): This is a function that convert the infix notation hold in the infix variable to a</li>

</ul>

postfix notation variable. You will use the template class Stack defined above in this function.

<ul>

 <li>std::string getPostfix(): This is a function that returns a postfix notation from the data member <em>postfix</em>.</li>

</ul>




Implement the member functions for the class Infix2Postfix in a file <strong>postfix.cpp</strong>.




The algorithm to convert an infix notation to a postfix notation is as follows:

<ol>

 <li>Push the left parenthesis ‘(‘ to the stack.</li>

 <li>Append a right parenthesis ‘)’ to the end of infix expression.</li>

 <li>While the stack is not empty, read infix from left to right and do the following:

  <ul>

   <li>If the current input in infix is an operand, copy it to the next element of postfix. o If the current input in infix is a left parenthesis, push it onto the stack.</li>

   <li>If the current input in infix is an operator, then:</li>

  </ul></li>

</ol>

Pop operators (if there are any) at the top of the stack while they have equal or higher precedence than the current operator, and insert the popped operators in postfix.

Push the current operator in infix onto the stack.

<ul>

 <li>If the current input in infix is a right parenthesis, then:</li>

</ul>

Pop operators from the top of the stack and insert them in postfix until a left parenthesis is at the top of the stack.

Pop (and discard) the left parenthesis from the stack.




The following arithmetic operations are allowed in an expression: +    addition

–     subtraction

<ul>

 <li>multiplication</li>

</ul>

/    division

%     modulus

The precedence of operators from the lowest to highest is defined as following:




+   –

<ul>

 <li>/ %</li>

</ul>




Write a driver program include main function in a file <strong>task1Main.cpp</strong> to declare an instance of <strong>InfixToPostfix</strong>. Then get an infix notation from the keyboard and convert the infix notation to the postfix notation. Finally print out the postfix notation.

For example, when the input is

1 + 3

The output of postfix notation should be 1 3


You can download the files <strong>exp1.txt</strong> and <strong>exp2.txt</strong> to test your program. See the testing for more details.

<strong>Testing: </strong>

You can compile the program by g++ -o task1 task1Main.cpp postfix.cpp

Run the program like

./task1 &lt; exp1.txt

AB  CDE  *  RST  UV  XX  /  –  3  *  +  X5  –

Test the program by exp2.txt like

./task1 &lt; exp2.txt

12.53  21.2  33.2  15.4  2  /  –  *  +  8.5  2.6  12  2  /  +  *  –

<strong> </strong>

<h2>Task Two: Templates &amp; manipulators for matrices (5 marks)</h2>




<strong>Background Information </strong>

A matrix is a set of numbers arranged in rows and columns as in a conventional 2D array. If <em>M</em> is a matrix with <strong>R</strong> rows and <strong>C</strong> columns, we say the matrix <em>M</em> is of the size RxC. Every element of a matrix has a row position <em>i</em> and a column position <em>j</em>. For example, <em>M[1,3]</em> is an element of the matrix <em>M</em> with the row position 1 and column position 3. In the context of this assignment, matrix elements can be real numbers, or complex numbers. Two matrixes A and B can be added, but only if they have the same size, by adding elements from the corresponding positions.

<em>C = A + B</em>, where <em>C[i,j] = A[i,j] + B[i,j]. </em>

Two matrixes A and B can be subtracted, again only if they have the same size, by subtracting elements from the corresponding positions.

<em>C = A – B</em>, where <em>C[i,j] = A[i,j] – B[i,j].</em>




Two matrices A and B, of sizes R<sub>a</sub>xC<sub>a</sub> and R<sub>b</sub>xC<sub>b</sub> respectively, can be multiplied together if and only if C<sub>a</sub>=R<sub>b</sub>. Multiplication is performed using the following algorithm:




<strong>For</strong> i=1 to R<sub>a</sub>

<strong>For</strong> j=1 to C<sub>b </sub>

C[i,j]=0

<strong>For</strong> k=1 to C<sub>a</sub>

C[i,j]=C[i,j]+A[i,k]*B[k,j]

<h3>          End For   End For End For</h3>




If elements of a matrix are complex, the matrix is called a complex matrix. A complex number <em>(r,m)</em> is a pair that consist of a real part <em>r</em> and an imaginary part <em>m</em>, where r and m are themselves both real numbers. Two complex numbers can be added and subtracted, that is defined by the following rules:

(a,b) + (c,d) = (a+c, b+d)

(a,b) – (c,d) = (a-c, b-d)

(a,b)*(c,d) = (ac-bd,bc+ad)




The magnitude of a complex number <em>(a, b)</em> is a real number <em>g </em>= <em>a</em><sup>2 </sup>+ <em>b</em><sup>2 </sup>.

<strong>Design Requirements </strong>

Define a class template matrix that can be instantiated to support basic operations on matrixes with <strong>real,</strong> or <strong>complex elements</strong>. The class shall input matrixes of any size using streams. It must have a constructor matrix(int rows, int columns), the operators +, -, *, &lt;&lt;, and &gt;&gt; overloaded and <strong>two</strong> <strong>new manipulators</strong>. A manipulator info should be used to complement the matrix output with its size. For example:




cout&lt;&lt;info&lt;&lt;M&lt;&lt;endl;




produces the following output:

3×4 matrix

2.1  4.3   0.1      1.3

0.4  18.2   7.3     2.5

45.3  5.0   5.3       7.6




Another manipulator, noinfo, shall be used to reset output to being without the matrix size information.




As addition and subtraction are defined only for matrixes of the same size, and a similar rule was stated earlier for multiplication, an exception must be thrown and handled if the sizes, or the types (complex, real) of two matrixes do not match. (Note that in practice complex and real matrices can be added.)




Define a class complexn to represent elements of complex matrices. The class must have a constructor complexn(float real, float img), the operators +, -, *, &lt;&lt;, &gt;&gt; overloaded, and four new manipulators.

cplx – set output to complex format <em>(a, b).</em> real – set output only to the real part <em>a</em> of the complex number.

img – set output only to the imaginary part <em>b</em> of the complex number. magnitude – set output only to the magnitude <em>g </em>of the complex number.




After that, the output &lt;&lt; of complex numbers shall follow the specified format. Output of numbers shall be with one decimal point precision.




Input of complex numbers will use two real numbers. To represent real numbers you can use the float data type.




<strong>You should have a simple </strong><strong>main</strong><strong>() function which </strong>

<ol>

 <li><strong>inputs four matrices, two real and two complex, of size at least 3 in each dimension and not more than 5 in each dimension. </strong></li>

 <li><strong>For the real matrices, outputs </strong>

  <ol>

   <li><strong>each matrix using </strong><strong>info </strong><strong>manipulator, </strong></li>

   <li><strong>their sum and difference using </strong><strong>noinfo </strong><strong>manipulator</strong><strong>,</strong><strong> and, </strong></li>

   <li><strong>their product using the </strong><strong>info</strong></li>

  </ol></li>

 <li><strong>For the complex matrices, outputs </strong>

  <ol>

   <li><strong>each matrix in complex format using </strong><strong>info</strong><strong>. </strong></li>

   <li><strong>the imaginary part, real part and magnitude of their sum, difference and product using the </strong><strong>noinfo</strong></li>

  </ol></li>

</ol>




You should provide a file, <strong>testmatrix.txt</strong> which contains the input values for use with the following command:




<strong>cat testmatrix.txt | ./Matrix </strong>

<strong> </strong>

where <strong>Matrix</strong> has been generated, on Banshee, using the directive:




<h3>g++ task2Main.cpp –o Matrix</h3>

<strong> </strong>

To facilitate an automatic compilation and testing, organize the code into:




<strong>matrix.h</strong>                 // declaration    <strong>matrix.cpp</strong> // implementation            <strong>task2Main.cpp</strong>                  // main() function <strong>testmatrix.txt       </strong>// test data




Inclusion model will be assumed in compiling the code.

<strong> </strong>


