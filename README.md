Download Link :https://programming.engineering/product/csci-3155-lab-assignment-3/


# CSCI-3155-Lab-Assignment-3
CSCI 3155: Lab Assignment 3
Learning Goals. The primary learning goals of this lab are to understand the following:

how to read a formal specification of a language semantics;

how dynamic scoping arises;

the distinction between a big-step and a small-step operational semantics;

evaluation order; and

substitution and program transformation;

PL Ideas Semantics: evaluation order. Operational semantics. Substitution and program trans-formation.

FP Skills Iteration. Introduction to higher-order functions.

Concretely, we will extend JAVASCRIPTY with recursive functions and implement two inter-preters. The first will be a big-step interpreter that is an extension of Lab 2 but implements dynamic scoping “by accident.” The second will be a small-step interpreter that exposes evalu-ation order by iterating a single-step transition relation and implements static scoping by sub-stitution.

Peer Teaching and Pair Programming. To be able to have someone to work closely with on the assignment, the instructor will randomly assign partners for the lab assignment; you will get a different partner for every lab assignment. You can pair program or work as closely as you like with your partner. However, note that each student needs to submit on Canvas, and you are individually responsible for your learning from the entirety of the assignment so that you can do well in your interview.

General Guidelines. You are welcome to talk about these questions beyond your teams. How-ever, we ask that you code in pairs. See the collaboration policy for details, including the follow-ing:

Bottom line, feel free to use resources that are available to you as long as the use is rea-sonable and you cite them in your submission. However, copying answers directly or indirectly from solution manuals, web pages, or your peers is certainly unreasonable.


Also, recall the evaluation guideline from the course syllabus.

Both your ideas and also the clarity with which they are expressed matter—both in your English prose and your code!

We will consider the following criteria in our grading:

How well does your submission answer the questions? For example, a common mistake is to give an example when a question asks for an explanation. An example may be useful in your explanation, but it should not take the place of the explanation.

How clear is your submission? If we cannot understand what you are trying to say, then we cannot give you points for it. Try reading your answer aloud to yourself or a friend; this technique is often a great way to identify holes in your reasoning. For code, not every program that “works” deserves full credit. We must be able to read and understand your intent. Make sure you state any pre-conditions or invariants for your functions (either in comments, as assertions, or as require clauses as appropriate).

Try to make your code as concise and clear as possible. Challenge yourself to find the most crisp, concise way of expressing the intended computation. This may mean using ways of ex-pression computation currently unfamiliar to you.

Finally, make sure that your file compiles (e.g., with sbt compile). A program that does not compile will not be graded—no interview will be conducted.

Submission Instructions. We are using GitHub for assignment distribution and some auto-grading. You need to have a GitHub identity and must have your full name in your GitHub profile so that we can associate you with your submissions.

You will be editing/creating and submitting the the following files:

src/main/scala/jsy/student/Lab3.scala with your solution to the coding exercises;

lab3-writeup.pdf or lab3-writeup.md for a pdf or a Markdown document that should be pushed to the root directory of your repository with your response to the written ques-tions (scanned, clearly legible handwritten write-ups are acceptable). You will not get credit for write-ups in any other file format.

src/test/resources/lab3/mytest_somedescription.jsy with a challenging test case for your JAVASCRIPTY interpreter.

You are also likely to edit

src/test/scala/jsy/student/Lab3Spec.scala with your additional tests;

src/main/scala/jsy/student/Lab3.worksheet.sc for any scratch work; and

src/main/scala/jsy/student/Lab3.worksheet.js for JavaScript experimentation. You can also add JAVASCRIPTY tests in


src/test/resources/lab3/ as a pair of a *.jsy and a *.ans for a JAVASCRIPTY expres-sion and the expected value of that expression, respectively.

Following good git practice, please make commits in small bits corresponding to completing small conceptual parts and push often so that your progress is evident. We expect that you have some familiarity with git from prior courses. If not, please discuss with your classmates and the course staff (e.g., via Piazza).

At any point, you may push your updated files to your GitHub repository for auto-grading. You need to push to your GitHub repository for the auto-testing part of your score, as well as to continue to the interview.

Sign-up for an interview slot for an evaluator. To fairly accommodate everyone, the inter-view times are strict and will not be rescheduled. Missing an interview slot means missing the interview evaluation component of your lab score. Please take advantage of your interview time to maximize the feedback that you are able to receive. Arrive at your interview ready with a working development environment to show your implementation and your written responses. Implementations that do not compile and run will not be evaluated.

Finally, upload the zip file of your repo to Canvas by clicking the Code button and then Download ZIP. The generated file should be named your-lab-repo-name-main.zip.

Getting Started. First, form a team of two and pick a team name. For our bookkeeping, please prefix your team name with the lab number and your CU IdentiKeys (i.e., your team should look something like L3_your-identikey1_your-identikey2_anatomists).

You must work in teams of two, and you will form teams in lab section. If you cannot connect with your partner, then please contact the course staff (via Piazza).

Then, log into Canvas and follow the GitHub Classroom link for setting up your Lab 3 repos-itory with your team name. The first person will create the team, and the second person will select the team name from the existing team names. If you need to move teams after you have already created or joined a repository, you will need to contact the Course Manager (via Piazza) or work with a course staff member to move you manually.

If you would like to look at the code before getting your own copy from GitHub Classroom, you may go to https://github.com/csci3155/pppl-lab3.

Correctness and Testing. While some test cases are provided to you, the correctness of your implementations is defined by the specification in this handout. In addition to the test cases provided to you directly in your GitHub repository, the auto-grading may run additional tests to which you do not have direct access. The auto-grading runs when you push changes to your GitHub repository, which offers you some quick, iterative, and repeatable feedback, while guid-ing you to think deeply about your code. While you do not have direct access to the actual input itself, each failing test is named, and you can use that information to get a sense of is-sues in your code to come up with your own test cases for testing those scenarios. The point here is that you won’t always have every possible test case provided to you — both in a literal sense for this lab and in industry in general — so getting practice in developing test cases to drive your coding is crucially important. A starting point is to look at the test cases provided to you directly and think about what isn’t already being tested. Then, add some tests relating to these. It’s impossible to test exhaustively, so try to find “edge” cases that test tricky aspects


of your implementation. As the course progresses, you are gradually given fewer tests with the expectation that you are gradually better at creating your own test suites.

Checkpoint. The checkpoint is to encourage you to start the assignment early and it requires you to submit (i.e., push) your partial solution on GitHub a week before the assignment is due. You do not need to attempt everything a week early, but we want you to start working on it and make note in this handout any required questions in the checkpoint. This means that submit-ting the empty template that fails all tests is not sufficient. Failing to submit to the checkpoint will prevent you from proceeding to the interview.

Feedback. Complete the survey on Canvas after completing this assignment. Any non-empty answer will receive full credit.

JavaScripty Interpreter: Tag Testing, Recursive Functions, and Dynamic Scoping. We now have the formal tools to specify exactly how a JAVASCRIPTY program should behave. Unless otherwise specified, we will continue to try to match JavaScript semantics as imple-mented by Node.js. Thus, it is still useful to write little test JavaScript programs and run it through Node.js to see how the test should behave. Finding bugs in the JAVASCRIPTY speci-fication with respect to JavaScript is certainly deserving of extra credit.

In this lab, we extend JAVASCRIPTY with recursive functions. This language is very similar to the LETREC language in Section 3.4 of Friedman and Wand.

For this question, we try to implement functions as an extension of Lab 2 in the most straightforward way. What we will discover is that we have made a historical mistake and have ended up with a form of dynamic scoping.

The syntax of JAVASCRIPTY for this lab is given in Figure 1. Note that the grammar specifies the abstract syntax using notation borrowed from the concrete syntax. The new constructs are highlighted. We have function expressions p(x) => e1 and function calls e1(e2).

In a function expression, the function name p can either be an identifier or empty. When the identifier for the function name is present, it can be used for recursion. For simplicity,

expressions

e ::= x | n | b | str | undefined | uop e1 | e1 bop e2

| e1 ? e2 : e3 | const x = e1; e2 | console.log(e1)

| p(x) => e1 | e1(e2) | typeerror

values

v ::= n | b | undefined | str | p(x) => e1 | typeerror

unary operators

uop ::= – | !

binary operators

bop ::= , | + | – | * | / | === | !== | < | <= | > | >= | && | ||

variables

x

numbers (doubles)

n

booleans

b ::= true | false

strings

str

function names

p ::= x | ε

value environments

E ::= · | E[ x v]

Figure 1: Abstract Syntax of JAVASCRIPTY.

statements

s ::= const x = e | e | { s1 } | ; | s1 s2

expressions

e ::= ··· | (e1)

| const x = e1; e2

| p(x) => e1 | x => e1 | x => blk | (x) => e1 | (x) => blk

| function p(x) blk

function body blocks

blk ::= { s return e1 }

Figure 2: Concrete Syntax of JAVASCRIPTY.

case class Function(p: Option[String], x: String, e1: Expr) extends Expr Function(p, x, e1) p(x) => e1

case class Call(e1: Expr, e2: Expr) extends Expr Call(e1, e2) e1(e2)

Figure 3: Representing in Scala the abstract syntax of JAVASCRIPTY. After each case class or case object, we show the correspondence between the representation and the syntax shown in Figure 1.

all functions are one argument functions. Since functions are first-class values, we can get multi-argument functions via currying.

We have also added a “marker” typeerror to the expression language. This marker is not part of the source language but is used in our definition of the evaluation judgment form. We discuss this in more detail further below.

As before, the concrete syntax accepted by the parser is slightly less flexible than the ab-stract syntax in order to match the syntactic structure of JavaScript. For function expres-sions, only the anonymous version is allowed using the arrow syntax (=>), which may op-tionally have parentheses around the parameter and whose body may be an expression e or a block blk. A function body block is surrounded by curly braces (i.e., { }) and consists of a statement s for const bindings followed by a return with an expression e1.

The function keyword syntax may have a function name but whose body must be a block.

An abstract syntax tree representation is provided for you in ast.scala. We also provide a parser and main driver for testing. The correspondence between the Scala representation and the syntax definition from Figure 1 is shown in Figure 3.

In this lab, we start to see specifications of programming language semantics. A big-step operational semantics of JAVASCRIPTY is given in Figure 4. This figure may be one of the first times that you are reading a formal semantics of a programming language. It may seem daunting at first, but it will be become easier with practice. This lab is such an opportunity to practice.

A formal semantics enables us to describe the semantics of a programming language clearly and concisely. The initial barrier is getting used to the meta-language of judgment forms and inference rules. However, once you cross that barrier, you will see that we are telling you exactly how to implement the interpreter—it will almost feel like cheating!

In Figure 4, we define the judgment form E ⊢ e ⇓ v, which says informally, “In value en-


E ⊢ e ⇓ v

EVALVAR

EVALVAL

EVALNEG

n′ = −toNumber(v1)

EVALNOT

b′ = ¬toBoolean(v1)

E ⊢ e1 ⇓ v1

E ⊢ e1 ⇓ v1

E ⊢ x ⇓ E(x)

E ⊢ v ⇓ v

E ⊢ −e1 ⇓ n′

E ⊢ ! e1 ⇓ b′

EVALSEQ

EVALPLUSNUMBER

′

toNumber(v

)

toNumber(v

)

E

⊢

e

1 ⇓

v

1

E

⊢

e

2 ⇓

v

2

E

⊢

e

1 ⇓

v

1

E

⊢

e

2 ⇓

v

2

n

=

1

+

2

v

1

str

v

2

str

2

̸= 1

̸=

E ⊢ e1 , e2 ⇓ v2

E ⊢ e1 + e2 ⇓ n′

EVALPLUSSTRING1

str′ = str1 +toString(v2)

EVALPLUSSTRING2

str′=toString(v1)+str2

E ⊢ e1 ⇓ str1

E ⊢ e2 ⇓ v2

E ⊢ e1 ⇓ v1

E ⊢ e2 ⇓ str2

E ⊢ e1 + e2 ⇓ str′

E ⊢ e1 + e2 ⇓ str′

EVALARITH

E ⊢ e2 ⇓ v2

n′ = toNumber(v1) bop toNumber(v2)

bop ∈ {−, ∗, /}

E ⊢ e1 ⇓ v1

E ⊢ e1 bop e2 ⇓ n′

EVALINEQUALITYNUMBER1

v1 ̸=str1

EVALINEQUALITYNUMBER2

v2 ̸=str2

E ⊢ e1 ⇓ v1

E ⊢ e2 ⇓ v2

E ⊢ e1 ⇓ v1

E ⊢ e2 ⇓ v2

b′ = toNumber(v1) bop toNumber(v2)

bop ∈ {<, <=, >, >=}

b′ = toNumber(v1) bop toNumber(v2)

bop ∈ {<, <=, >, >=}

E ⊢ e1 bop e2 ⇓ b′

E ⊢ e1 bop e2 ⇓ b′

EVALINEQUALITYSTRING

E ⊢ e1 ⇓ str1

E ⊢ e2 ⇓ str2

b′ = str1 bop str2

bop ∈ {<, <=, >, >=}

E ⊢ e1 bop e2 ⇓ b′

EVALEQUALITY

EVALANDTRUE

E ⊢ e1 ⇓ v1

E ⊢ e2 ⇓ v2

v

1

p

(x

)

=>

e

1

v

2

p

(x

)

=>

e

2

b

′

=

(v

1

bop v

2

)

bop

∈

{

===

, !

}

E

⊢

e

1

⇓

v

1

true

=

toBoolean(v

1

)

E

⊢

e

2

⇓

v

2

̸= 1

1

̸= 1

2

==

E ⊢ e1 bop e2 ⇓ b′

E ⊢ e1 && e2 ⇓ v2

EVALANDFALSE

EVALORTRUE

EVALORFALSE

E ⊢ e2 ⇓ v2

E ⊢ e1 ⇓ v1

false = toBoolean(v1)

E ⊢ e1 ⇓ v1

true = toBoolean(v1)

E ⊢ e1 ⇓ v1false = toBoolean(v1)

E ⊢ e1 && e2 ⇓ v1

E ⊢ e1 || e2 ⇓ v1

E ⊢ e1 || e2 ⇓ v2

EVALPRINT

EVALIFTRUE

E ⊢ e2 ⇓ v2

E ⊢ e1 ⇓ v1

v1 printed

E ⊢ e1 ⇓ v1

true = toBoolean(v1)

E ⊢ console.log(e1) ⇓ undefined

E ⊢ e1 ? e2 : e3 ⇓ v2

EVALIFFALSE

E ⊢ e3 ⇓ v3

EVALCONST

v1] ⊢ e2 ⇓ v2

E ⊢ e1 ⇓ v1

false = toBoolean(v1)

E ⊢ e1 ⇓ v1

E[ x

E ⊢ e1 ? e2 : e3 ⇓ v3

E ⊢ const x = e1; e2 ⇓ v2

EVALCALL

v1 = (x) => e′

E ⊢ e2 ⇓ v2

E[ x v2] ⊢ e′ ⇓ v′

E ⊢ e1 ⇓ v1

E ⊢ e1(e2) ⇓ v′

EVALCALLREC

E ⊢ e2 ⇓ v2

v2] ⊢ e′ ⇓ v′

E ⊢ e1 ⇓ v1

v1 = x1(x2) => e′

E[ x1

v1][ x2

E ⊢ e1(e2) ⇓ v′

Figure 4: Big-step operational semantics of JAVASCRIPTY (with dynamic scoping).


vironment E, expression e evaluates to value v.” This relation has three parameters: E, e, and v. You can think of the other parts of the judgment as just punctuation. This judg-ment form corresponds directly to the eval function that we are asked to implement (not a coincidence). It similarly has three parts:

def eval(env: Env, e: Expr): Expr

It takes as input a value environment env (corresponding to E) and an expression e (corre-sponding e) returns a value v.

It is very informative to compare your Scala code from Lab 2 with the inference rules that define E ⊢ e ⇓ v. One thing you should observe is that all of the rules are implemented, except for EVALCALL, EVALCALLREC, and part of EVALEQUALITY. In essence, implementing those rules is your task for this question.

In Lab 2, all expressions could be evaluated to something (because of conversions). With functions, we encounter one of the very few run-time errors in JavaScript: trying to call something that is not a function. In JavaScript and in JAVASCRIPTY, calling a non-function raises a run-time error. In the formal semantics, we model this with evaluating to the “marker” typeerror.

Such a run-time error is known as a dynamic type error. Languages are called dynamically typed when they allow all syntactically valid programs to run and check for type errors dur-ing execution.

In our Scala implementation, we will not clutter our Expr type with a typeerror marker.

Instead, we will use a Scala exception DynamicTypeError:

case class DynamicTypeError(e: Expr) extends Exception

to signal this case. In other words, when your interpreter discovers a dynamic type error, it should throw this exception using the following Scala code:

throw DynamicTypeError(e)

The argument should be the input expression to eval where the type error was detected. One advantage of using a Scala exception for typeerror is that the marker does not need to be propagated explicitly as in the inference rules in Figure 6. In particular, your interpreter will implement the EVALTYPEERROR rules explicitly, but the EVALPROPAGATE rules are imple-mented implicitly with Scala’s exception propagation semantics.

Note in rule EVALEQUALITY, we disallow equality and disequality checks (i.e., === and ! ==) on function values. If either argument to a equality or disequality check is a function value, then we consider this a dynamic type error. This choice is a departure from JavaScript se-mantics.

First, write some JAVASCRIPTY programs and execute them as JavaScript programs. This step will inform how you will implement your interpreter and will serve as tests for your interpreter.

Submit at least one of your tests as src/test/resources/lab3/mytest_somedescription.jsy


for the checkpoint. Focus on tricky edge cases to get better feedback.

Write-up: In your write up, give one test case that behaves differently under dy-namic scoping versus static scoping (and does not crash). Explain the test case and how they behave differently in your write-up.

Then, implement

def eval(env: Env, e: Expr): Expr

that evaluates a JAVASCRIPTY expression e in a value environment env to a value ac-cording to the evaluation judgment E ⊢ e ⇓ v.

You will again want the following helper functions for converting values to numbers, booleans, and strings:

def toNumber(v: Expr): Double

def toBoolean(v: Expr): Boolean

def toStr(v: Expr): String

We suggest the following step-by-step process:

Bring your Lab 2 implementation into Lab 3 and make sure your previous test cases work as expected.

Extend your implementation with non-recursive functions. On function calls, you need to extend the environment for the formal parameter but not for the function itself. Do not worry yet about dynamic type errors.

Add support for checking for dynamic type errors.

Check that your interpreter, unfortunately, implements dynamic scoping instead of static scoping.

Modify your implementation to support recursive functions.

While not strictly required, an important milestone to reach is have completed this question (i.e., finished implementing this eval function), except perhaps with a few remaining bugs to iron out, by the end of the first week.

JavaScripty Interpreter: Substitution and Evaluation Order. In this question, we will do two things. First, we will remove environments and instead use a language semantics based on substitution. This change will “fix” the scoping issue, and we will end up with static, lexical scoping.

As an aside, substitution is not the only way to “fix” the scoping issue. Another way is to represent function values as closures, which is a pair of the function with the environment when it is defined. Substitution is a fairly simple way to get lexical scoping, but in practice, it is rarely used because it is not the most efficient implementation.

The second thing that we do is move to implementing a small-step interpreter. A small-step interpreter makes explicit the evaluation order of expressions. These two changes are or-thogonal, that is, one could implement a big-step interpreter using substitution or a small-step interpreter using environments.

Implement


def iterate(e0: Expr)(next: (Expr, Int) => Option[Expr]): Expr

that iterates calling the callback next until next returns None. The callback next takes an Expr to transform and the iteration number, which is initially (e0, 0).

This function is used by the interface method iterateStep to repeatedly call step to reduce a JAVASCRIPTY expression to a value.

(b) Implement

def substitute(e: Expr, v: Expr, x: String): Expr

that substitutes value v for all free occurrences of variable x in expression e. We advise defining substitute by recursion on e. The cases to be careful about are ConstDecl and Function because these are the variable binding constructs. In particular, calling substitute on expression

a; (const a = 4; a)

with value 3 for variable “a” should return

3; (const a = 4; a)

not

3; (const a = 4; 3)

This function is a helper for the step function, but you might want to implement all of the cases of step that do not require substitute first.

(c) Implement

def step(e: Expr): Expr

that performs one-step of evaluation by rewriting the input expression e into a “one-step reduced” expression. This one-step reduction should be implemented according to the judgment form e −→ e′ defined in Figures 7, 8, and 9. We write e[v/x] for sub-stituting value v for all free occurrences of the variable x in expression e (i.e., a call to substitute).

Write-up: Explain whether the evaluation order is deterministic as specified by the judgment form e −→ e′.

It is informative to compare the small-step semantics used in this question and the big-step semantics from the previous one. In particular, for all programs where dynamic scoping is not an issue, your interpreters in this question and the previous should behave the same. We have provided the functions evaluate and iterateStep that evaluate “top-level” ex-pressions to a value using your interpreter implementations.

Evaluation Order. Write-up: Consider the small-step operational semantics for JAVASCRIPTY shown in Figures 7, 8, and 9. What is the evaluation order for e1 + e2? Explain. How do we change the rules to obtain the opposite evaluation order?


Short-Circuit Evaluation. In this question, we will discuss some issues with short-circuit evaluation.

Concept. Write-up: Give an example that illustrates the usefulness of short-circuit evaluation. Explain your example.

JAVASCRIPTY. Write-up: Consider the small-step operational semantics for JAVASCRIPTY shown in Figures 7, 8,and 9. Does e1 && e2 short circuit? Explain.


−→ e′


e −→ e′

SEARCHUNARY

SEARCHBINARY1

SEARCHBINARYARITH2

e1 −→ e1′

e1 −→ e1′

e2 −→ e2′bop ∈ {+, −, ∗, /, <, <=, >, >=}

uop e1 −→ uop e1′

e1 bop e2 −→ e1′ bop e2

v1 bop e2 −→ v1 bop e2′

SEARCHEQUALITY2

e

bop

{

, !

}

SEARCHPRINT

e′

e

−→

e′

v

p(x)

=>

∈

==

e

−→

2

2

1

̸=

1

===

1

1

v1 bop e2 −→ v1 bop e2′

console.log(e1) −→ console.log(e1′)

SEARCHIF

SEARCHCONST

SEARCHCALL1

e1 −→ e1′

e1 −→ e1′

e1 −→ e1′

e1 ? e2 : e3 −→ e1′ ? e2 : e3

const x = e1; e2 −→ const x = e1′; e2

e1(e2) −→ e1′(e2)

SEARCHCALL2

2 −→ e2′

p(x) => e1 (e2) −→ p(x) => e1 (e2′)

Figure 8: Small-step operational semantics of JAVASCRIPTY: SEARCH rules.

e −→ e′

TYPEERROREQUALITY1

TYPEERROREQUALITY1

TYPEERRORCALL

bop ∈ {===, ! ==}

bop ∈ {===, ! ==}

v1 ̸=p(x) => e1

(p(x) => e1) bop e2 −→ typeerror

v1 bop (p(x) => e2) −→ typeerror

v1(e2) −→ typeerror

PROPAGATEUNARY

PROPAGATEBINARY

PROPAGATEBINARY

uop typeerror −→ typeerror

typeerror bop e2 −→ typeerror

v1 bop typeerror −→ typeerror

PROPAGATEPRINT

PROPAGATEIF

console.log(typeerror) −→ typeerror

typeerror ? e2 : e3 −→ typeerror

PROPAGATECONST

PROPAGATECALL1

PROPAGATECALL2

const x = typeerror; e2 −→ typeerror

typeerror(e2) −→ typeerror

v1(typeerror) −→ typeerror

Figure 9: Small-step operational semantics of JAVASCRIPTY: Dynamic type error rules.

