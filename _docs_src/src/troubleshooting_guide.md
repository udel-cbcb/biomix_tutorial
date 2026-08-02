# How to troubleshoot

Troubleshooting issues is one of the most important skills for anyone doing computational work, but can be daunting if you are new to the command line.  These guidelines and tips should help you to be more comfortable and successful in the process.

* **The computer is (almost) always right.**  The hardest thing to accept at the beginning of your computational journey is that if something isn't working, it's probably because you made a mistake.  Don't let that bother you; data scientists of all experience levels encounter issues all the time!

* **If you get an error, read it carefully.**. Good error messages are useful.  Take the time to try to understand what the error is telling you.  Look up any words you don't understand to help you interpret the message.

* **Carefully inspect your code or command.**. Make sure to check every character, down to the spaces and other whitespace characters.

* **Not every issue results in an error message.**  If you get no error message, but a command still does not result in the expected output, you still have an issue.  In this case, carefully examine your command.

* **Keep the manual handy.** Just like for bash, manuals and other documentation exist for any good software or programming language.  Use these to look up details of how a command/line of code can be used and refer to any included examples for extra tips.

* **Google is your best friend!**  Google is your greatest resource when troubleshooting errors.  Often, just copying and pasting your error into the search bar will result in the exact answer you've been looking for.  Always be sure to include information like your operating system and the name of software you are trying to run, if applicable.

* **[StackOverflow](https://stackoverflow.com/) is your other best friend.** StackOverflow is a question/answer website.  It is the most popular place for people to ask questions about computational (and other issues), so your top Google search hits will often be from StackOverflow.  Users are able to up- and downvote answers, so the top response is almost always reliable, especially on common questions.

* **ChatGPT and other AI tools should be used with care.**  AI tools can be incredibly helpful in troubleshooting.  However, they will not always be able to provide a good answer and it is harder for beginners to recognize when an answer is wrong.  There is a reason that these tools are currently banned from StackOverflow: they regularly produce answers that seem correct, but really are not.

* **Always check intermediate files.**  If you are running a pipeline or program with multiple steps, be sure to check whether intermediate files were generated and if they contain data.  When pipelines encounter issues, they will often keep chugging along, generating a series of empty files.  Checking each of the expected files for data will reveal where your error occurred.
