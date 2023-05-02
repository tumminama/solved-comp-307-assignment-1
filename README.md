Download Link: https://assignmentchef.com/product/solved-comp-307-assignment-1
<br>



<em>Introduction to </em>AI

<strong>Basic Machine Learning Algorithms</strong>

<em>15% of Final Mark </em>

<h1>1       Objectives</h1>

The goal of this assignment is to help you understand the basic concepts and algorithms of machine learning, write computer programs to implement these algorithms, use these algorithms to perform classification tasks, and analyse the results to draw some conclusions. In particular, the following topics should be reviewed:

<ul>

 <li>Machine learning concepts,</li>

 <li>Machine learning common tasks, paradigms and methods/algorithms,</li>

 <li>Nearest neighbour method for classification,</li>

 <li>Decision tree learning method for classification,</li>

 <li>Perceptron/linear threshold unit for classification, and</li>

 <li>k-means method for clustering and k-fold cross validation for experiments.</li>

</ul>

These topics are (to be) covered in lectures 04–07. The textbook and online materials can also be checked.

<h1>2       Question Description</h1>

<h2>Part 1: Nearest Neighbour Method [30 Marks for COMP307, and 37 Marks for COMP420]</h2>

This part is to implement the k-Nearest Neighbour algorithm, and evaluate the method on the <em>wine </em>data set described below. Additional questions on k-means and k-fold cross validation need to be answered and discussed.

<h3>Problem Description</h3>

The <em>wine </em>data set is taken from the UCI Machine Learning Repository (http://mlearn.ics.uci.edu/MLRepository.html). The data set contains 178 instances in 3 classes, having 59, 71 and 48 instances, respectively. Each instance has 13 attributes: <em>Alcohol, Malic</em><em>acid, Ash, Alcalinity of ash, Magnesium, Total</em><em>phenols, Flavanoids, Nonflavanoid</em><em>phenols, Proanthocyanins, Color</em><em>intensity, Hue, OD280%2FOD315 of diluted wines</em>, and <em>Proline</em>. The data set is split into two subsets, one for training and the other for testing.

<h3>Requirements</h3>

Your programshould classify each instance in the test set wine-testaccording to the training set wine-training. Note that the final columns in these files list the class label for each instance.

Your program should take two file names as command line arguments, and classify each instance in the test set (the second file name) according to the training set (the first file name).

You may write the program code in Java, C/C++, Python, or any other programming language.

You should submit the following files electronically and also a report in hard copy.

<ul>

 <li>(15 marks) Program code for your k-Nearest Neighbour Classifier (both the source code and the executable program that is runnable on ECS School machines).</li>

 <li>txt describing how to run your program, and</li>

 <li>(15 marks) A report in PDF, text or DOC format. The report should include:

  <ol>

   <li>Report the class labels of each instance in the test set predicted by the basic nearest neighbour method (where k=1), and the classification accuracy on the test set of the basic nearest neighbour method.</li>

   <li>Report the classification accuracy on the test set of the k-nearest neighbour method where k=3,and compare and comment on the performance of the two classifiers (k=1 and k=3).</li>

   <li>Discuss the main advantages and disadvantages of k-Nearest Neighbour method.</li>

   <li>Assuming that you are asked to apply the k-fold cross validation method for the above problemwith <em>k=5</em>, what would you do? State the major steps.</li>

   <li>In the above problem, assuming that the class labels are not available in the training set and thetest set, and that there are three clusters, which method would you use to group the examples in the data set? State the major steps.</li>

  </ol></li>

 <li>(7 marks, this question is for COMP420 students. It is optional for COMP307 students (bonus 5 marks))</li>

</ul>

Implement the clustering method, run it on the <em>wine </em>data set using the number of clusters of 3 and 5. Submit the program code, report the number of instances in each cluster, and provide an analysis on your results (you can just provide simple comments by comparing your results with the classes).

<h2>Part 2: Decision Tree Learning Method [35 Marks for COMP307, and 38 Marks for COMP420]</h2>

This part involves writing a program that implements a simple version of the Decision Tree (DT) learning algorithm, reporting the results, and discussing your findings.

<h3>Problem Description</h3>

The main data set for the DT program is in the files hepatitis, hepatitis-training,and hepatitis-test. It describes 137 cases of patients with hepatitis, along with the outcome. Each case is specified by 16 Boolean attributes describing the patient and the results of various tests. The goal is to be able to predict the outcome based on the attributes. The first file contains all the 137 cases; the training file contains 112 of the cases (chosen at random) and the testing file contains the remaining 25 cases. The first columns of the files show the class label (“live” or “die”) of each instance. The data files are formatted as tab-separated text files, containing one header line, followed by a line for each instance.

<ul>

 <li>The first line contains the names of the attributes.</li>

 <li>Each instance line contains the class name followed by the values of the attributes (“true” or “false”).</li>

</ul>

This data set is taken from the UCI Machine Learning Repository http://mlearn.ics.uci.edu/MLRepository.html. It consists of data about the prognosis of patients with hepatitis. This version has been simplified by removing some of the numerical attributes, and converting others to booleans.

The file golf.data is a smaller data set in the same format that may be useful for testing your programs while you are getting them going. Each instance describes the weather conditions that made a golf player decide to play golf or to stay at home. This data set is not large enough to do any useful evaluation.

<h3>Decision Tree Learning Algorithm</h3>

The basic algorithm for building decision trees from examples is relatively easy. Complications arise in handling multiple kinds of attributes, doing the statistical significance testing, pruning the tree, etc., but your program don’t have to deal with any of the complications.

For the simplest case of building a decision tree for a set of instances with boolean attributes (yes/no decisions), with no pruning, the algorithm is shown below.

<table width="566">

 <tbody>

  <tr>

   <td width="566">instances: the set of training instances that have been provided to the node being constructed; attributes: the list of attributes that were not used on the path from the root to this node.BuildTree (Set instances, List attributes) <strong>if </strong>instances is empty <strong>return </strong>a leaf node containing the name and probability of the most probable class across the whole dataset(i.e., the ‘‘baseline’’ predictor)<strong>if </strong>instances are pure (i.e., all in the same class) <strong>return </strong>a leaf node containing the name of the class of the instances in the node and probability 1<strong>if </strong>attributes is empty <strong>return </strong>a leaf node containing the name and probability of the majority class of the instances in the node (choose randomly if classes are equal)<strong>else </strong>find best attribute:<strong>for each </strong>attribute separate instances into two sets:1)      instances for which the attribute is true, and2)      instances for which the attribute is false compute purity of each set.<strong>if </strong>weighted average purity of these sets is best so far bestAtt = this attributebestInstsTrue = set of true instances bestInstsFalse = set of false instances build subtrees using the remaining attributes:left = BuildTree(bestInstsTrue, attributes – bestAtt) right = BuildTree(bestInstsFalse, attributes – bestAttr) <strong>return </strong>Node containing (bestAtt, left, right)</td>

  </tr>

 </tbody>

</table>

To apply a constructed decision tree to a test instance, the program will work down the decision tree, choosing the branch based on the value of the relevant attribute in the instance, until it gets to a leaf. It then returns the class name in that leaf.

<h3>Requirements</h3>

Your program should take two file names as command line arguments, construct a classifier from the training data in the first file, and then evaluate the classifier on the test data in the second file.

You can write your program in Java, C/C++, Python, or any other programming language.

You should submit the following files electronically and also a report in hard copy.

<ul>

 <li>(20 marks) Program code for your decision tree classifier (both source code and executable program running on the ECS School machines). The program should print out the tree in a human readable form (text form is fine).</li>

</ul>

You should use the (im)purity measures presented in the lectures unless you want to use another measure from the textbook (i.e. information gain), which is more complex and not recommended. The file helper-code.java contains java code that may be useful for reading instance data from the data files. You may use it if you wish, but you may also write your own code.

<ul>

 <li>txt describing how to run your program, and</li>

 <li>(15 marks) A report in PDF, text or DOC format. The report should include:

  <ol>

   <li>You should first apply your program to the hepatitis-training and hepatitis-test files and report the classification accuracy in terms of the fraction of the test instances that it classified correctly. Report the learned decision tree classifier printed by your program. Compare the accuracy of your Decision Tree program to the baseline classifier which always predicts the most frequent class in the dataset, and comment on any difference.</li>

   <li>You could then construct 10 other pairs of training/test files, train and test your classifiers on eachpair, and calculate the average accuracy of the classifiers over the 10 trials. The files of 10 split 10 training and test sets are provided. The files are named as hepatitis-training-run-*, and hepatitis-test-run-*. Each training set has 107 instances and each test set has the remaining 30 instances. Show you working.</li>

   <li>“Pruning” (removing) some of leaves of the decision tree will always make the decision tree lessaccurate on the training set. Explain (a) How you could prune leaves from the decision tree; (b) Why it would reduce accuracy on the training set, and (c)Why it might improve accuracy on the test set.</li>

   <li>Explain why the impurity measure is not a good measure if there are three or more classes that the decision tree must distinguish.</li>

  </ol></li>

 <li>(3 marks, only for COMP420 students) What three conditions are needed if a function (such as P(A)*P(B)) is used as an impurity measure in building a decision tree?</li>

</ul>

<h3>Note: A Simple Way of Outputting a Learned Decision Tree</h3>

The easiest way of outputting the tree is to do a traversal of the tree. For each non-leaf node, print out the name of the attribute, then print the left tree, then print the right tree. For each leaf node, print out the class name in the leaf node and the fraction. By increasing the indentation on each recursive call, it becomes somewhat readable.

Here is a sample tree (not a correct tree for the golf dataset). Note that the final leaf node which is impure can only occur on a path which has used all the attributes so there is no attribute left to split the instances any further. This should not happen for the data set above, but might happen for some datasets.

<table width="377">

 <tbody>

  <tr>

   <td width="377">cloudy = True:raining = True:Class StayHome, prob = 1.0 raining = False:Class PlayGolf, prob = 1.0 cloudy = False:hot = true:Class PlayGolf, prob = 1.0 hot = False:windy = True:Class StayHome, prob = 1.0 windy = False:Class PlayGolf, prob = 0.75</td>

  </tr>

 </tbody>

</table>

Here is some sample (Java) code for outputting a tree.

In class Node (a non-leaf node of a tree):

public void report(String indent){ System.out.format(“%s%s = True:
”, indent, attName);

left.report(indent+” “); System.out.format(“%s%s = False:
”,

indent, attName);

right.report(indent+”  “);

}

In class Leaf (a leaf node of a tree):

public void report(String indent){

if (count==0)

System.out.format(“%sUnknown
”, indent); else

System.out.format(“%sClass %s, prob=$4.2f
”, indent, className, probability); }

<h2>Part 3: Perceptron [35 Marks for COMP307, and 45 Marks for COMP420]</h2>

This part of the assignment involves writing a program that implement a perceptron with “random” features that learns to distinguish between two classes of black and white images (X’s and O’s).

<h3>Data Set</h3>

The file image.data consists of 100 image files, concatenated together. Each image file is in PBM format, with exactly one comment line.

<ul>

 <li>The first line contains P1,</li>

 <li>The second line contains a comment (starting with #) that contains the class of the image (such as X and O),</li>

 <li>The third line contains the image width and height (number of columns and rows),</li>

 <li>The remaining lines contain 1’s and 0’s representing the pixels in the image, with ’1’ representing black, and ’0’ representing white. The line breaks are ignored.</li>

</ul>

<h3>Features</h3>

The program should construct a perceptron that uses at least 50 “random” features. Each feature should be connected to 3 randomly chosen pixels. Each connection should be randomly marked as <em>true </em>or <em>false</em>, and the feature should return 1 if at least two of the connections match the image pixel, and return 0 otherwise.

For example, if the Feature class has fields:

class feature {

int[] row; int[] col;

boolean[] sgn;

then a feature with positive connections to pixels (5,2), and (2,9), and negative connections to (6,5) could be represented using three arrays of length 3:

f.row = { 5, 2, 6};

f.col = { 2, 9, 5};

f.sgn = { true, true, false}; and the value of the feature for the given image (represented by a 2D boolean array) could be computed by:

int sum=0; for(int i=0; i &lt; 3; i++) if (image[f.row[i], f.col[i]]==f.sgn[i]) sum++;

return (sum&gt;=2)?1:0;

You may find it convenient to calculate the values of the features on each image as a preprocessing step, before you start learning the perceptron weights. This means that each image can be represented by an array of feature values. Don’t forget to include the “dummy” feature whose value is always 1.

If you are using Java, new Java.util.Random() will create a random number generator with a nextInt(int n) method that returns an int between 0 and n−1, and a nextBoolean(int n) method that returns a random boolean. To get the same sequence of random numbers every time, you can call the constructor with an integer (or long) argument that sets the seed of the random number generator to start at the same state each time.

<h3>Simple Perceptron Algorithm</h3>

A perceptron with <em>n </em>features is represented by a set of real valued weights, {<em>w</em><sub>0</sub><em>,w</em><sub>1</sub><em>,…,w<sub>n</sub></em>}, one weight for the threshold, and one for each feature. Given an instance with features <em>f</em><sub>1</sub><em>,…,f<sub>n</sub></em>, the perceptron will classify the instance as a positive instance (a member of the class) only if

<em>n</em>

X<em>w<sub>i</sub>f<sub>i </sub>&gt; </em>0

<em>i</em>=0

where <em>f</em><sub>0 </sub>is a “dummy” feature that is always 1.

The algorithm for learning the weights of the perceptron was given in lectures:

<table width="415">

 <tbody>

  <tr>

   <td width="415">Until the perceptron is always right (or some limit):Present an example (+ve or -ve)If perceptron is correct, do nothingIf -ve example and wrong(ie, weights on active features are too high) Subtract feature vector from weight vectorIf +ve example and wrong(ie, weights on active features are too low)Add feature vector to weight vector</td>

  </tr>

 </tbody>

</table>

Your program should implement this algorithm, using the feature vectors calculated from the images based on the previous description. It should present the whole sequence of training examples, several times over, until either the perceptron is correct on all the training examples, or it stops converging (e.g., it has presented all the examples 100 times). It should then use the perceptron to classify all the examples.

<h3>Useful File</h3>

The file MakeImage.java would let you construct your own image files if you wish (the data file image.data has been created using this program). More useful is the load method in that file that will read a pbm file (as long as it has exactly the one comment and no spaces between the pixels). You may modify this to load the data from image.data.

<h3>Requirements</h3>

The program should take one file name (the image data file) as a command line argument, and then:

<ul>

 <li>load the set of images from the data file,</li>

 <li>construct a set of random features,</li>

 <li>construct a perceptron that uses the features as inputs,</li>

 <li>train the perceptron on the images until either it has presented the whole set of images at least 100 times or the perceptron weights have converged (ie, the perceptron is correct on all the images),</li>

 <li>report on the number of training cycles to convergence, or the number of images that are still classified wrongly, and</li>

 <li>print out the “random” features that it created, and the final set of weights the perceptron acquired.</li>

</ul>

You can write your program in Java, C/C++, Python, or any other programming language.

In this part of the assignment, you should submit:

<ul>

 <li>(25 marks) Program code for your perceptron classifier (both source code and executable program runnable on the ECS School machines).</li>

 <li>txt describing how to run your program, and</li>

 <li>(10 Marks) A report in PDF, text or DOC format. The report should:

  <ol>

   <li>Report on the accuracy of your perceptron. For example, did it find a correct set of weights?</li>

   <li>Explain why evaluating the perceptron’s performance on the training data is not a good measureof its effectiveness. You may wish to create additional data to get a better measure. If you do, report on the perceptron’s performance on this additional data.</li>

  </ol></li>

 <li>(10 marks, for COMP420 students) Given the classification problem (Table 1): eight instances with three features in two classes (class 0 and class 1). Use the perceptron to solve this problem. Submit the program code and answer the following two questions in the report.

  <ol>

   <li>Run the program code of perceptron to solve this problem five times and report the averagedaccuracy.</li>

   <li>Analyse the results and make your conclusions in the report.</li>

  </ol></li>

</ul>

Table 1: Dataset (for COMP420 students)

<table width="405">

 <tbody>

  <tr>

   <td width="99">Instance No.</td>

   <td width="78">Feature 1</td>

   <td width="78">Feature 2</td>

   <td width="78">Feature 3</td>

   <td width="71">Class</td>

  </tr>

  <tr>

   <td width="99">1</td>

   <td width="78">0</td>

   <td width="78">0</td>

   <td width="78">1</td>

   <td width="71">0</td>

  </tr>

  <tr>

   <td width="99">2</td>

   <td width="78">0</td>

   <td width="78">1</td>

   <td width="78">0</td>

   <td width="71">1</td>

  </tr>

  <tr>

   <td width="99">3</td>

   <td width="78">1</td>

   <td width="78">0</td>

   <td width="78">1</td>

   <td width="71">1</td>

  </tr>

  <tr>

   <td width="99">4</td>

   <td width="78">1</td>

   <td width="78">1</td>

   <td width="78">0</td>

   <td width="71">0</td>

  </tr>

  <tr>

   <td width="99">5</td>

   <td width="78">1</td>

   <td width="78">1</td>

   <td width="78">1</td>

   <td width="71">0</td>

  </tr>

  <tr>

   <td width="99">6</td>

   <td width="78">1</td>

   <td width="78">0</td>

   <td width="78">0</td>

   <td width="71">1</td>

  </tr>

  <tr>

   <td width="99">7</td>

   <td width="78">0</td>

   <td width="78">1</td>

   <td width="78">1</td>

   <td width="71">1</td>

  </tr>

  <tr>

   <td width="99">8</td>

   <td width="78">0</td>

   <td width="78">0</td>

   <td width="78">0</td>

   <td width="71">0</td>

  </tr>

 </tbody>

</table>

<h1>3          Relevant Data Files and Program Files</h1>

The relevant data files, information files about the data sets, and some utility program files can be found in the following directory:

/vol/comp307/assignment1-new/

Under this directory, there are three subdirectories part1, part2, and part3 corresponding to the three parts of the assignment, respectively.


