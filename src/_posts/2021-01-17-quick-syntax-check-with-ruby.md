---
title: "Quick Syntax Check with Ruby"
permalink: /quick-syntax-check-with-ruby
---

If you've been working in a ruby file for a while and then tried to execute the file and encountered a syntax error it can be a bit frustrating.

Especially if the file is in a rails application. You have to notate the error line from the browser log, exit the browser and fix the line in the file and then rerun your program and hope that there isn't another error further down the file.

Well, ruby has you covered!

The ruby interpreter allows you to pass a few flags along with the name of the file whose syntax you wish to check and it will report back the status of the syntax for the file.

To run this check simply type `ruby -cw <filename>` and hit enter.

You can also pass any .rb files from your rails application to check the syntax. Just run the same command and pass the path to the file and run it.

-Happy Rubying!!!