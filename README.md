# CALAND (CALculator+ANDroid)
###Abstract  
In today's world, Android phones take a prominent place in the mobile industry. It has become popular because of it's user friendly interface and ease of development of various applications. Our application, named 'Caland'(CALculator+ANDroid), aims at allotting partial credits to a user's methodology of solving a given mathematical expression by comparing the two expression trees - model tree and the user tree.  

###Download and run this project:
__This method is used to import this project in Android Studio only__  

In Android Studio,  
1. Select VCS from menu bar and select 'Github' from 'checkout from version controll'.  
2. Provide your credentials, if it asks for it.  
3. Copy the 'HTTPS clone url' into 'VC's repository URL' and click on close.  
4. The project gets cloned into local system. Change the 'Android' widget to 'Project' widget.  
5. Wait for gradle to build and run this application either in emulator or your android device.  

###Prerequisites
1. The user should know how to work with calculator with memory functions (M+, M-, MR and MC).
2. The user should keep in mind the precedence and associativity rules which solving the expression.
3. Only one operator or operand can be entered at a time in a calculator (so that we can perform step by step evaluation).

###Design
![ui](https://cloud.githubusercontent.com/assets/12692738/15332563/bc5d8380-1c83-11e6-9518-2ddf823d6a4b.png)

1. 7 activity screens were designed.  
2. The flow marked with 1 between activity_main and activity_menu, MainActivity.java's onClick() method opens activity_menu.xml. 
3. The flow marked with 2, menu.java's onClick() method goes to easy.xml upon clicking on easy button or med.xml upon clicking on medium button or hard.xml upon clicking on hard button. 
4. The flow marked with 3, either easy.java's or med.java's or hard.java's onClick() method opens activity_easy1.xml.
5. The flow marked with 5, uses CalculatorBrains's performOperation() and performWaitingOperation() methods to implement working calculator. 
6. The flow marked with 4, when the end button ('X' in the calculator) gets clicked, easy1's onClick() method opens activity_final.xml. 
  easy1.java's onClick method pass the key presses of the user and the model question to activity_final. 
7. The flow marked with 6 in the activity_final.xml, FinalActivity.java implements InfixToPostfix class to convert model tree's infix expression to postfix expression using InfixToPostfix.translate() and to convert user's keypresses to infix expression using InfixToPostfix.toInfix() and then to postfix expression using InfixToPostfix.translate().   
8. Both the postfix expressions will be passed to Tree class's insert() and evaluate() methods, so that, the model tree's and user tree's evaluated expression tree can be passed for comparision.   
  The root nodes of both the trees are passed to Tree.java's compare method.   
  If the structure of both the tree's are same, compare() method gets executed, else, it throws EmptyStackException.   
  When this exception is caught, excmp() method is called. It is called when the structure of the two tree's are not same.   
  If the evaluated values of both the trees are same, excmp1() method gets called.   
  If the length of both postfix expressions are same or user's postfix expression length is greater than the model postfix expression length, it is evaluated for hundred, else, it is evaluated for fifty.   
  Finally, what the model question was, what the user tries to solve and the credits he could earn for his efforts are shown in activity_final.xml's Model expr, User expr, and Earned text boxes.  
  
###Algorithm

1. Let x be given mathematical expression (model infix expression).
2. Let y be keypresses of the user on the calculator (stored in an array)
3. Convert y to infix expression using InfixToPostfix class's toInfix() method (user infix expression).
4. Convert model and user infix expression to model and user postfix expression respectively.
5. Construct binary expression trees for both user tree and model tree.
6. Using cmp() method of Tree class, compare both the expression trees, to which exent it is correct. This works if structure of trees are similar (ie, same nodes and edges with same or different values).
7. If structure is not similar, throw exception, catch exception and call excmp() method.
8. Using cmp() or excmp() compare method, evaluate the partial credits the user earned.

###Keypresses to Infix

![intopo](https://cloud.githubusercontent.com/assets/12692738/15333466/6558a926-1c87-11e6-8bf1-b24a17998e7d.png)

### Tree Comparison
![trcmp](https://cloud.githubusercontent.com/assets/12692738/15333572/d374c958-1c87-11e6-9c49-b9d07d271605.png)

- Each node has three nodes:
  1. Left most node represent operator or operand in the expression
  2. Middle node, evaluates the result of subtree from bottom to up.
  3. Right most node is applicable only in the user tree, it is used for compasison.Initially, variable denom = 0
     1. Taking a subtree formed by binary operator (+,-,*,/) from user and model expression tree, if all three nodes contain same value in both user and model expression tree, 3 is put in the last node, 3 is added to 'denom'.
     2. Taking a subtree formed by binary operator (+,-,*,/) from user and model expression tree, if all two out of three nodes contain same value in both user and model expression tree, 2 is put in the last node,  3 is added to 'denom'.
     3. Taking a subtree formed by binary operator (+,-,*,/) from user and model expression tree, if all one out of three nodes contain same value in both user and model expression tree, 1 is put in the last node,  3 is added to 'denom'.
     4. Taking a subtree formed by binary operator (+,-,*,/) from user and model expression tree, if none nodes contain same value in both user and model expression tree, 0 is put in the last node,  3 is added to 'denom'.
     4. Taking a subtree formed by unary operator (1/x, x^2, √) from user and model expression tree, if both the nodes contain same value in both user and model expression tree, 2 is put in the last node, 2 is added to 'denom'.
     5. Taking a subtree formed by unary operator (1/x, x^2, √) from user and model expression tree, if one out of two the nodes contain same value in both user and model expression tree,1 is put in the last node, 2 is added to 'denom'.
     6. Taking a subtree formed by unary operator (1/x, x^2, √) from user and model expression tree, if none of the nodes contain same value in both user and model expression tree, 0 is put in the last node, 2 is added to 'denom'.
    
    Finally, the values stored in rightmost nodes are added and stored in variable called 'mark'.
    Accuracy is calculated by, mark/denom*100
     
     

### Comparison when Tree structures are dissimilar
#### Initial state
![init](https://cloud.githubusercontent.com/assets/12692738/15334124/7356eec2-1c8a-11e6-97b1-deb16015a69d.png)

####Final state
![fin](https://cloud.githubusercontent.com/assets/12692738/15333800/c6a016a0-1c88-11e6-9bbc-bbc943faf00e.png)

###Problems
- This project is a research oriented project and it has lots of bugs to be detected and corrected. 
- The users will get to know as and when they use this application.

On the positive side, this project has scope in many applications. 
- It can be developed further for various other applications and can be implemented in evaluation in online examinations, where, user gets credits based on what he tried to solve rather than just looking into his final answer.
- It can be used for self evaluation.
- It can be extended to include man more operators like logical, relational, bit wise, etc. 

