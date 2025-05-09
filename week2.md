Week:2

[Shell]{.mark} : In computing, a **shell** is a user interface that
provides access to the services of an operating system

Command-Line Shells:

1.  **Bourne Shell (sh)**

2.  **Bash (Bourne Again Shell)**

3.  Zsh (Z Shell)

4.  **KornShell (ksh)**

5.  **Fish (Friendly Interactive Shell)**

[2. Shell Scripting]{.mark}

**Shell scripting** is the practice of writing scripts using a shell\'s
scripting language to automate tasks.

An expert shell script writer utilizes constructs such as:

- Loops (for, while)

- Conditional logic (if, case)

- Functions

- Stream redirection and pipelines

- Process substitution

------------------------------------------------------------------------

[1.Getting Started with Shell Scripting: Naming, Permissions, Variables,
Builtins.]{.mark}

[\# sharp]{.mark}

[! Bang]{.mark}

[#! Shebang]{.mark}

[Builtins]{.mark} :

Type echo

O/p: echo is a shell builtins

Commands:

[To check which shell is using in OS:]{.mark}

Echo \$SHELL

[How to create command bash script:]{.mark}

Cd desktop/

touch hello.sh

Nano hello.sh

[Script:]{.mark}

[#! /bin/bash]{.mark}

[Echo "hello world"]{.mark}

Chmod +x hello.sh

./hello.sh

O/p: Hello world

[Two types if variables]{.mark}:

1.  **Environment Variables**

2.  **User-defined**

**Environment Variables:**

**Echo \$bash**

**Echo \$bash_version**

**Echo \$pwd**

**Echo\$home**

**O/p: /bin/bash**

**4.0.12.4 version**

**Desktop**

**/home/text**

[How to use variables:]{.mark}

Name='vinitha'

Echo "my name is \$Name"

o/p: my name is vinitha

[Read User Input:]{.mark}

![](./media/image1.png){width="2.7752405949256342in"
height="1.3501170166229222in"}

![](./media/image2.png){width="3.3169542869641293in"
height="1.0834273840769904in"}

![](./media/image3.png){width="3.525305118110236in"
height="0.8417399387576553in"}

Append text to varaiable:

Name 'vinitha'

Echo "my name is \${Name}R"

0r

Word 'string'

Echo "this is \${word}ing"

[Combine two variable:]{.mark}

Echo "\${name}\${word}."

[Special Variables, Pseudocode, Command Substitution, if Statement,
Conditionals.]{.mark}

#display the userid and username of the executing user:

#display if the user is root user or not.

![](./media/image4.png){width="2.350203412073491in"
height="1.108429571303587in"}

![](./media/image5.png){width="3.4836351706036743in"
height="0.8000688976377953in"}

#display the uid:

Echo "your userid is \${uid}"

Uid is manual in bash

O/p: your userid is 1000

[General commands manual]{.mark}

Command: [man bash]{.mark}

Id -u

o/p: 1000

id -n

o/p: root

If statement:

![](./media/image6.png){width="3.516971784776903in"
height="2.850247156605424in"}

O/p:

![](./media/image7.png){width="3.7253226159230097in"
height="1.1834361329833771in"}

![](./media/image8.png){width="3.5836439195100613in"
height="3.025262467191601in"}

o/p:

![](./media/image9.png){width="2.7335706474190724in"
height="1.091761811023622in"}

[Exit Statuses, Return Codes, String Test Conditionals, More Special
Variables.]{.mark}

![](./media/image10.png){width="5.433804680664917in"
height="1.633474409448819in"}

***Goal:***

The goal of this exercise is to create a shell script that adds users to
the same Linux system as the script is executed on.

***Scenario:***

Imagine that you\'re working as a Linux System Administrator for a fast
growing company.  The latest company initiative requires you to build
and deploy dozens of servers.  You\'re falling behind schedule and are
going to miss your deadline for these new server deployments because you
are constantly being interrupted by the help desk calling you to create
new Linux accounts for all the people in the company who have been
recruited to test out the company\'s newest Linux-based application.

In order to meet your deadline and keep your sanity, you decide to write
a shell script that will create new user accounts.  Once you\'re done
with the shell script you can put the help desk in charge of creating
new accounts which will finally allow you to work uninterrupted and
complete your server deployments on time.

![](./media/image11.png){width="6.268055555555556in"
height="5.892361111111111in"}

![](./media/image12.png){width="2.091848206474191in"
height="1.591804461942257in"}

O/p:

![](./media/image13.png){width="4.058685476815398in"
height="2.666897419072616in"}

[Random Data, Cryptographic Hash Functions, Text and String
Manipulation.]{.mark}

[Random Data]{.mark}:

Echo \${RANDOM}

[Positional Parameters, Arguments, for Loops, Special Parameters]{.mark}

Arguments in Shell:

Static input:

![](./media/image14.png){width="3.525305118110236in"
height="1.1000951443569553in"}

o/p

![](./media/image15.png){width="2.850247156605424in"
height="0.35003062117235345in"}

[Positional Parameters]{.mark}

\${0} fisrt argument

\${1} second argument

\${2} third argument

.............................. \${#} -TOTAL NO.OF ARGUMENT

![](./media/image16.png){width="3.8753357392825896in"
height="1.8001563867016623in"}

o/p:

![](./media/image17.png){width="6.268055555555556in"
height="0.7895833333333333in"}

[Dynamic Input:]{.mark}

![](./media/image18.png){width="3.175275590551181in"
height="1.6501432633420823in"}

O/P:

![](./media/image19.png){width="3.791994750656168in"
height="0.8500732720909886in"}

[For loop]{.mark}:

![](./media/image20.png){width="2.891917104111986in"
height="1.6418088363954506in"}

o/p:

![](./media/image21.png){width="3.308619860017498in"
height="0.7167290026246719in"}

The while Loop, Infinite Loops, Shifting, Sleeping

While loop:

![](./media/image23.png){width="3.816996937882765in"
height="2.183522528433946in"}

![](./media/image24.png){width="2.650229658792651in"
height="0.4167027559055118in"}

[True]{.mark}:

Do nothing return the exit comment as 0

[Sleep:]{.mark}

![](./media/image25.png){width="4.233699693788276in"
height="2.9419214785651793in"}

SHIFT:

![](./media/image26.png){width="4.292038495188102in"
height="3.025262467191601in"}

o/p:

![](./media/image27.png){width="5.18378280839895in"
height="2.933587051618548in"}
