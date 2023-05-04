Download Link: https://assignmentchef.com/product/solved-csci316-assignment5
<br>
<strong>SECTION 1 (Nonrecursive Preliminary Problems) </strong>

<strong>The three problems in this section (A – C) do not carry direct credit, but are intended to help you solve problems 1 – 3 in Part I of Section 2.  Note that there <em>may</em> be questions on exam 1 or on the final exam that are of a similar nature to A – C.</strong>

<strong>         Your solutions to problems A – C <em>must not be recursive</em>.  You can test your solutions to these three problems on <em>venus</em> or <em>euclid</em>: Functions INDEX, MIN-FIRST, and SSORT with the stated properties are predefined for you when you start Lisp using  </strong><strong>cl  on those machines.  </strong>




<ol>

 <li>INDEX is a function that is already defined on euclid and venus. If N <em>is any positive integer</em> <em>and </em></li>

</ol>

<em>     </em>L <em>is any list</em>, then (INDEX N L) returns the Nth element of L if N does not exceed the length of         L; if N exceeds the length of the list L, then (INDEX N L) returns the symbol ERROR.   For          example,    (INDEX 3 ‘(A S (A S) (A) D)) =&gt; (A S)     (INDEX 6 ‘(A S (A S) (A) D)) =&gt; ERROR      Complete the following definition of a function MY-INDEX <strong><em>without making further calls </em></strong>    <strong><em> of</em></strong>  INDEX and without calling MY-INDEX recursively, in such a way that if N is any integer       <strong><em>greater than</em></strong> 1 and L is any <strong><em>nonempty</em></strong> list then (MY-INDEX N L) is equal to (INDEX N L).




(defun my-index (N L)

(let ((X (index (- N 1) (cdr L))))

__ ))




[Note: You should not have to call any functions.]




<ol>

 <li>MIN-FIRST is a function that is already defined on euclid and venus; if L <em>is any nonempty list of</em> <em>real numbers</em> then (MIN-FIRST L) is a list whose CAR is the minimum of the numbers in L and       whose CDR is the list obtained when the first occurrence of that value is removed from L.   (Thus       (MIN-FIRST L) is “L with the first occurrence of its minimum value moved to the front”.)  For       example,   (MIN-FIRST ‘(0 3 1 1 0 3 5)) =&gt; (0 3 1 1 0 3 5)</li>

</ol>

(MIN-FIRST ‘(4 3 1 1 0 3 5 0 3 0 2)) =&gt; (0 4 3 1 1 3 5 0 3 0 2).

Complete the following definition of a function MY-MIN-FIRST <strong><em>without making further calls of</em></strong>       MIN-FIRST and without calling MY-MIN-FIRST recursively, in such a way that if L is any list of       <strong><em>at</em> <em>least two</em></strong> real numbers then (MY-MIN-FIRST L) is equal to (MIN-FIRST L).




(defun my-min-first (L)

(let ((X (min-first (cdr L))))

___________________________________

___________________________________ ))




[There are two cases: (car L) may or may not be ≤ (car X).]







<strong>*</strong><strong>If you have difficulty with these problems, you are encouraged to see me during my office hours. Questions about these     problems that are e-mailed to me </strong><strong>will <em>not</em> be answered until after the due date</strong><strong>. </strong>

<ol>

 <li>SSORT is a function that is already defined on euclid and venus; if L <em>is any list of real numbers</em> then (SSORT L) is a list of those numbers in ascending order. Complete the following definition of a function MY-SSORT <strong><em>without making further calls of</em></strong>  SSORT and without calling       MY-SSORT recursively, in such a way that if L is any <strong><em>nonempty</em></strong> list of real numbers then       (MY-SSORT  L) is equal to (SSORT L).</li>

</ol>




(defun my-ssort (L)

(let* ((L1 (min-first L))

(X  (ssort (cdr L1))))

__________________________________ ))







<strong>SECTION 2 (Main Problems)</strong>




<strong>Your solutions to the following 16 problems will count a total of 2% towards your grade if the grade is computed using rule A––the 10 problems in Part I will count 1%, and the 6 problems in Part II will also count 1%.  It is expected that your solutions to problems 1 – 3 will be based on your solutions to A – C above.   [On euclid and venus, when you load in your function definitions for problems 1 – 3, you will replace the predefined functions with the same names with your versions of those functions.] </strong>

<strong>         Program in a functional style, <em>without using SETF or iterative constructs such as DO</em>.   Follow the indentation and spacing rules at:</strong>

<strong>   </strong><a href="https://euclid.cs.qc.cuny.edu/316/indentation-and-spacing-guidelines-for-Lisp-Assignments.pdf">https://euclid.cs.qc.cuny.edu/316/indentation-and-spacing-guidelines-for-Lisp-Assignments.pdf</a> <strong>Use LET / LET* or appropriate helping functions to avoid evaluating computationally expensive expressions more than once.  Any helping functions you define for use in your solutions must be defined in the .lsp file that you submit for grading. </strong>




<strong>         When writing a function, decide what the <em>valid</em></strong> <strong>values for each argument will be. The statement of each problem specifies that certain argument values <em>must</em> be valid. For example, in problem 5 any list of real numbers <em>in ascending order</em> (including the empty list) <em>must</em> be a valid  value for each of the arguments; you can choose to make other argument values valid too. </strong>     <strong>If <em>f</em> computes (<em>f</em> <em>y</em> …) from (<em>f</em> (<em>smaller </em> <em>y</em>) …) for certain values of <em>y</em>, your <em>base case</em> code needs to ensure this <em><u>never</u></em> happens for any value of <em>y </em>that is valid (in the sense of the previous paragraph) for that argument but which satisfies one of the following conditions: </strong>

<strong>               BC-1:  (<em>smaller  y</em>)<em> is undefined. </em></strong>

<strong>               BC-2:  (<em>smaller  y</em>)<em> is defined but is </em>not<em> a valid value for that argument of  f. </em></strong>

<strong>      BC-3:  (<em>smaller  y</em>)<em> is a valid value for that argument of f but is no smaller in size than y </em>                          [e.g., the case <em>y</em> = NIL when (<em>smaller</em>  <em>y</em>) is (cdr <em>y</em>), if NIL is a valid value for <em>y</em>]. </strong>

<strong> </strong>

<strong>PART I  [Solutions to problems 1 – 10 will count 1% towards your grade if the grade is         computed using rule A.] </strong>

<strong> </strong>

<ol>

 <li>Define a recursive function INDEX with the properties stated in problem A. Note that the first argument of INDEX may be 1, and that the second argument may be NIL.</li>

</ol>




<ol start="2">

 <li>Define a recursive function MIN-FIRST with the properties stated in problem B. Note that the argument of MIN-FIRST may be a list of length 1.</li>

</ol>




<ol start="3">

 <li>Define a recursive function SSORT with the properties stated in problem C. In the definition of SSORT you may call SSORT itself, MIN-FIRST, CONS, CAR, CDR and ENDP, but you      should not call any other function.</li>

</ol>




<ol start="4">

 <li>Use the function PARTITION from Lisp Assignment 4 to complete the following definition of a recursive function QSORT such that if L <em>is a list of real numbers</em> then (QSORT L) is a list of      those numbers in ascending order.</li>

</ol>

(DEFUN QSORT (L)

(IF (ENDP L)

NIL

(LET ((PL (PARTITION (CDR L) (CAR L))))

…  )))




<ol start="5">

 <li>Define a Lisp function MERGE-LISTS such that if each of L1 and L2 is a list of real numbers in ascending order then (MERGE-LISTS L1 L2) returns the list of numbers in ascending order that is      obtained by merging L1 and L2. Your definition must <strong><em><u>not</u> </em></strong>call any sorting function.</li>

</ol>

<strong>Examples</strong>:       (MERGE-LISTS  ‘(2 4 5 5 7 8 9) ‘(3 4 6 9 9)) =&gt; (2 3 4 4 5 5 6 7 8 9 9 9)

(MERGE-LISTS  ‘(1 2 3)  ‘(4 5 6 7)) =&gt; (1 2 3 4 5 6 7)

(MERGE-LISTS  ‘(3 4 5 6 7)  ‘(0 1 2 3)) =&gt; (0 1 2 3 3 4 5 6 7)




<strong>Hint</strong>: Consider the 4 cases  L1 = ( ), L2 = ( ), (&lt; (car L1) (car L2)), and (&gt;= (car L1) (car L2)).







<ol start="6">

 <li>Use the function SPLIT-LIST from Lisp Assignment 4 and MERGE-LISTS to define a recursive Lisp function MSORT such that if L is a list of real numbers then (MSORT L) is a list consisting      of the elements of L in ascending order. In the definition of MSORT you may call SPLIT-LIST,       MSORT itself, MERGE-LISTS, CAR, CDR, CADR and ENDP, but you should not call any             other function. Be sure to use LET or LET*, so that MSORT only calls SPLIT-LIST once.</li>

</ol>

<strong>Hint</strong>: Does a list of length 1 satisfy condition <strong>BC-3</strong> (see page 2) for one of your function’s recursive calls?







<strong>In problems 7 – 10, assume the argument is a list.   </strong>




<ol start="7">

 <li>Do exercise 10.4(a) on page 418 of Sethi, but use Common Lisp instead of Scheme. Name your function REMOVE-ADJ-DUPL.</li>

</ol>

<strong> </strong>

<strong><u>Hint for problems 8 and 9</u></strong>   One way to do these two problems is to give definitions of the following form:




(defun <em>function-name</em> (L)

(cond  ((endp L)                                                                      …    )     ;  L is ( )

((or (endp (cdr L)) (not (equal (car L) (cadr L))))     …    )     ;  L is (x) or (x y … )

((or (endp (cddr L)) (not (equal (car L) (caddr L)))) …    )      ;  L is (x x)  or  (x x y … )

(t                                                                                …    ))) ;  L is (x x x … )




<ol start="8">

 <li>Do exercise 10.4(b) on the same page in Common Lisp. Name your function UNREPEATED-ELTS.</li>

</ol>










<ol start="9">

 <li>Do exercise 10.4(c) on the same page in Common Lisp. Name your function REPEATED-ELTS.</li>

</ol>










<ol start="10">

 <li>Do exercise 10.4(d) on the same page in Common Lisp. Name your function COUNT-REPETITIONS.</li>

</ol>










<strong>PART II  [Solutions to problems 11 – 16 will count 1% towards your grade if the grade is                      computed using rule A.] </strong>







11.<strong>[Exercise 8 on p. 141 of Wilensky]</strong>  Write a recursive function SUBSET that takes two arguments:         a function and a list. SUBSET should apply the function to each element of the list, and return a         list of all the elements of the argument list for which the function application returns a true (i.e.,         non-NIL) value.   <strong>Example</strong>:  (subset  #’numberp  ‘(a b 2 c d 3 e f)) =&gt; (2 3)




12.<strong>[Exercise 7 on p. 141 of Wilensky]</strong>  Write (i) a recursive function OUR-SOME and (ii) a recursive        function OUR-EVERY each of which takes two arguments: a function and a list.  OUR-SOME        should apply the function to successive elements of the list <em>until </em>the function returns a true (i.e.,        non-NIL) value, at which point it should return the rest of the list (including the element for which        the function just returned a true value).* If the function returns NIL when applied to each of the        arguments, OUR-SOME should return NIL. OUR-EVERY should apply the function to successive        elements of the list <em>until </em>the function returns NIL, at which point it should return NIL.  If the        function returns a true value when applied to each of the arguments, then OUR-EVERY should        return T.    <strong>Examples</strong>:

(our-some #’numberp ‘(A B 2 C D))  =&gt;  (2 C D)   (our-some #’numberp ‘(A B C D))  =&gt;  NIL

(our-every #’symbolp ‘(A B 2 C D))  =&gt;  NIL         (our-every #’symbolp ‘(A B C D))  =&gt;  T

*Note that the built-in Lisp function SOME behaves differently from OUR-SOME in this case: SOME returns the          non-NIL value that was just returned by the function.







<ol start="13">

 <li>Modify your solutions to problem 7 of Lisp Assignment 4 and problem 4 above to produce a solution to exercise 10.6<strong><em>b</em></strong> on p. 419 of Sethi. Your sorting function should take as arguments a        2-argument predicate p and a list L, and may assume the predicate p and list L are such that:

  <ol>

   <li>For all elements <em>x</em> and <em>y</em> of L, (p <em>x y</em>) is either true or false.</li>

   <li>Whenever <em>x</em> and <em>y</em> are unequal elements of L, if (p <em>x y</em>) is true then (p <em>y x</em>) is false.</li>

   <li>For all elements <em>x</em>,<em> y</em>, and <em>z</em> of L, if (p <em>x y</em>) is true and (p <em>y z</em>) is true then (p <em>x z</em>) is also true. The sorted list returned by your function should contain exactly the same elements as L, and must       satisfy the following condition: Writing <em>s<sub>i</sub></em> to denote the <em>i</em><sup>th</sup> element of the sorted list, whenever the       elements <em>s<sub>j</sub></em> and <em>s<sub>k</sub></em> are unequal and <em>j </em>&lt; <em>k</em> (i.e., <em>s<sub>k</sub></em> appears <em>after</em> <em>s<sub>j</sub></em> in the sorted list) we have that        (p <em>s<sub>k</sub></em> <em>s<sub>j</sub></em>) is false. (You can easily verify that the sorted lists in the three examples below satisfy this        ) Your sorting function and the partition function it uses should be named <strong>QSORT1</strong>        and <strong>PARTITION1.  </strong><strong>Examples</strong>:</li>

  </ol></li>

</ol>

(QSORT1  #’&gt;  ‘(2 8 5 1 5 7 3))  =&gt;  (8 7 5 5 3 2 1)

(QSORT1  #'&lt;  ‘(2 8 5 1 5 7 3))  =&gt;  (1 2 3 5 5 7 8)

(QSORT1  (LAMBDA (L1 L2) (&lt;  (LENGTH L1) (LENGTH L2)))

‘((X) (A D X E G) (1 2 Q R) NIL (S D F)))   =&gt;   (NIL (X) (S D F) (1 2 Q R) (A D X E G))







<ol start="14">

 <li>Do exercise 10.12a on p. 420 of Sethi in Common Lisp. <strong>Example</strong>:</li>

</ol>

(FOO #’–  ‘(1 2 3 4 5)) =&gt; ((–1 2 3 4 5) (1 –2 3 4 5) (1 2 –3 4 5) (1 2 3 –4 5) (1 2 3 4 –5))







<ol start="15">

 <li>First, re-read section 8.16 (Advantages of Tail Recursion) on pp. 279 – 81 of Touretzky. Then solve the following problems.</li>

</ol>




<ul>

 <li>Do exercise 10.5 on p. 419 of Sethi in Common Lisp. Name your functions TR-ADD, TR-MUL and TR-FAC.     <strong>Examples</strong>:</li>

</ul>

(TR-ADD ‘(1 2 3 4 5) 0) =&gt; 15     (TR-MUL ‘(1 2 3 4 5) 1) =&gt; 120     (TR-FAC 5 1) =&gt; 120             Note that your definitions of TR-ADD, TR-MUL, and TR-FAC must be <strong><em><u>tail recursive</u></em></strong>.







<ul>

 <li>Wilson’s Theorem in number theory states that an integer <em>n</em> &gt; 1 is prime if <em>and only if </em>(<em>n</em> – 1)! mod <em>n</em>  = <em>n</em> – 1.  Use<em> this theorem</em> and TR-FAC to write a predicate SLOW-PRIMEP                   such that if <em>n</em> &gt; 1 is an integer then (SLOW-PRIMEP <em>n</em>) returns T or NIL according to              whether or not <em>n</em> is prime.  (You may of course use the built-in function MOD.)  Test your              predicate SLOW-PRIMEP by using it to find the least prime number greater than 20,000.                <strong>Important</strong>: To prevent stack overflow, enter     (compile ‘tr-fac)     at clisp’s &gt; prompt              before calling SLOW-PRIMEP with large arguments.</li>

</ul>










Lisp Assignment 5: Page 4 of 5




16.<strong>[Based on exercise 8 on p. 111 of Wilensky]</strong>  A matrix can be represented as a nonempty list of        nonempty lists in which the i<sup>th</sup> element of the j<sup>th</sup> list is the element in the i<sup>th</sup> column and j<sup>th</sup> row of        the matrix.  For example, ((A B) (C D)) would represent a 2 × 2 matrix whose first row contains        the elements A and B, and whose second row contains the elements C and D. Write three functions        TRANSPOSE1, TRANSPOSE2, and TRANSPOSE3, each of which takes a single argument M; if        M is a nonempty list of nonempty lists which represents a matrix in the above-mentioned way,        then each of the three functions should return the list of lists which represents the transpose of that        matrix. The three functions should work as follows:




<ul>

 <li>(transpose1 M) computes its result from (transpose1 (cdr M)) and (car M) using mapcar #’cons.  [<strong>Hint</strong>: Take the set of valid values of M to be the set of lists of one or more                   nonempty lists that all have the same length.  Then the <strong>BC-2</strong> base case is (endp (cdr M)),                   when the result to be returned is  (mapcar #’list (car M)).]</li>

 <li>(transpose2 M) computes its result from (transpose2 (mapcar #’cdr M)) and (mapcar #’car M).</li>

</ul>

[<strong>Hint</strong>: Again, take the set of valid values of M to be the set of lists of one or more                   nonempty lists that all have the same length.  This time, the <strong>BC-2</strong> base case is

(endp (cdar M)), when the result is  (list (mapcar #’car M)).]

<ul>

 <li>(transpose3 M) obtains its result as follows: (apply #’mapcar (cons #’??? M)) or, equivalently, (apply #’mapcar #’??? M), where ??? is the name of an appropriate function.</li>

</ul>




<strong>Example</strong> (here <em>n</em> may be 1, 2 or 3):

(TRANSPOSE<em>n</em>   ‘((1 2 3 4) (5 6 7 8) (9 10 11 12))) =&gt; ((1 5 9) (2 6 10) (3 7 11)(4 8 12))





