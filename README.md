Download Link: https://assignmentchef.com/product/solved-cs3103-operating-systems-programming-assignment-1
<br>
<h1>Goals</h1>

By completing this assignment, you will know how to develop a program in the Linux platform and to make system calls related to process management.




<h1>Introduction</h1>

You need to implement a C/C++ program called BP that allows user to run <strong>multiple processes (up to three <em>at the same time</em>)</strong> at the background. When three processes are currently running, further execution request will be pended (the process state is changed to “stopped”) and wait until <strong>another</strong> process is stopped or terminated. While processes are running at the background, the user can input command to display information of the background processes, stop or kill a background process.




<h1>Requirements</h1>

<ol>

 <li>Your BP needs to show a prompt for user input as follows.</li>

</ol>

$ ./BP

BP &gt;




<ol start="2">

 <li>BP accepts the following commands from the user and takes the corresponding action.</li>

</ol>




<table width="654">

 <tbody>

  <tr>

   <td width="654"> BP &gt;bg [name of executable file] [a list of arguments]Action: BP runs the executable file with a list of arguments at the background and continues to accept input from the user. If there are already 3 running processes, the process is stopped. Example: BP runs the executable file demo1 with a list of [arguments]: running 2 5 at the background and continues to accept input from the user.BP &gt;bg demo1 running 2 5BP &gt; </td>

  </tr>

  <tr>

   <td width="654"> BP &gt;bglistAction: Display the process id(s), name(s) and the state(s) of ALL background processes. Example:BP &gt;bglist16529: demo1(running)16605: demo2(stopped)16613: demo3(terminated) </td>

  </tr>

  <tr>

   <td width="654"> BP &gt;bgstop [pid]Action: Stop the process with process id pid and display a message. If there exists <em><u>another</u></em> stopped process <em>(e.g. stopped earlier because there’re already 4 running processes)</em>, the earliest process in stopped state <em>(creation order, not runtime order)</em> should be automatically restarted. Example:BP &gt;bgstop 1652916529 stopped16624 automatically restarted</td>

  </tr>

  <tr>

   <td width="654"> BP &gt;bgkill [pid]Action: Terminate the process with process id pid and display a message. Similar to bgstop, if there exists <em>another</em> stopped process, the earliest process <em>(creation order, not runtime order)</em> in stopped state should be automatically restarted. Example:BP &gt;bgkill 1652916529 killed </td>

  </tr>

  <tr>

   <td width="654"> BP &gt;exitAction: BP executes bgkill to terminate all background processes, if any, and exits.   Example:BP &gt;exit16605 killed16607 killed$ </td>

  </tr>

 </tbody>

</table>




<ol start="3">

 <li>BP should display a message after a background process has completed.</li>

</ol>

Example:

<ul>

 <li>completed</li>

</ul>




<ol start="4">

 <li>You may assume that the syntax of the input commands and pids are valid, but BP needs to handle redundant commands (e.g. bgkill a process which is already terminated) by displaying a message. Examples:

  <ul>

   <li>already stopped</li>

  </ul></li>

</ol>

16529 already terminated 16529 does not exist




<h1>Hints</h1>

<ul>

 <li>Use fork() and execvp() so that the parent process accepts user input and the child process executes the background process.</li>

 <li>When you use fork(), it is important that you do not create a <em>fork bomb</em>, which easily eats up all the resources allocated to you. If this happens, you can try to use the command “kill” to terminate your processes (<a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">http://cslab.cs.cityu.edu.hk/supports/unix</a><a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">–</a><a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">startup</a><a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">–</a><a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">guide</a><a href="http://cslab.cs.cityu.edu.hk/supports/unix-startup-guide">)</a>.  However, if you cannot log into your account any more, you need to ask CSLab for help to kill your processes.</li>

 <li>Use waitpid() with an option WNOHANG to check if a background process has completed.</li>

 <li>Use kill()to send a signal to a process, e.g., a SIGTERM signal to terminate a process. Do note that kill()can also be used to stop / resume a process, regardless of it’s name.</li>

 <li>Study the man pages of the system calls used in your program. For example, the following command displays the man pages of kill() in Section 2.</li>

</ul>

$ man 2 kill




<h1>Helper programs demo.cpp</h1>

<ul>

 <li>This demo program can be used to act as a background process for testing your BP as its execution can be visualized by displaying a word every few seconds a number of times.</li>

 <li>This program takes three arguments, word, interval and times.  The first argument word is a single word to be displayed repeatedly.  The second argument interval is the number of seconds between two consecutive displays of the word.</li>

 <li>The third argument times is the number of times the word to be displayed.</li>

 <li>For example, the following command displays the word “running” 5 times in 2-second interval.</li>

</ul>

$ demo running 2 5




args.cpp

<ul>

 <li>This example program shows how to read a line from terminal, as well as parsing (cutting) the string using the strtok()</li>

 <li>To compile the program, use the following command.</li>

</ul>

$ g++ args.cpp -lreadline -o args

<strong> </strong>




<ul>

 <li></li>

</ul>





