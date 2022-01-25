Lab 4: TempConverter; irb; loops and blocks
=

Objectives:
=

- Learn the basics of Ruby programming
- Learn how to work with Time class in Ruby
- Learn how to create blocks and use loops in Ruby
- Learn to use irb command prompt
- Improve familiarity with basic git commands

Due Date:
= 
**February, 3rd 2022** by the end of the lab session.

Important Note
= 
 In this lab, you have a total of **3 checkpoints** to validate with one of the teaching team members. 
 
Checkpoints will be graded as follows:

* Checkpoint 1: 25 points
* Checkpoint 2: 35 points
* Checkpoint 3: 40 points


Part 1: Ruby Introduction
===========

This part of the lab will get everyone familiar with some Ruby basics and provides a review of other key concepts. This is a short introduction, but there are some 'on your own' exercises at the very end that students are strongly encouraged to try to solidify their understanding of Ruby. 

1. We are going to begin by writing a simple program for Ruby to convert temperatures and then modify it several times. 

	a. First, open Visual Studio Code and connect to your CMUQ dedicated server via `ssh-remote`. Please review the steps provided in this [tutorial](https://canvas.cmu.edu/courses/26286/modules/items/5060523), if needed.
	
	b. In the terminal, create a new folder named `lab4` (`mkdir lab4` then`cd lab4`), where you will save all your ruby files for this lab. 
		
	
	b. Now create a new file called `temp_conversions.rb`. In VS Code, just use `File --> new File`. Then save the file as a Ruby file. Do not forget to indicate the `.rb` extension.
	
	c. In this file, create a method called `convert` that takes `temp` as a parameter (temperature in Fahrenheit) and converts it to its equivalent in Celsius. 
	
	d. Create some simple tests for this method with the code below:
	
	```ruby
	  puts convert(32)          
	  puts convert(50)          
	  puts convert(212)
	```
	 
    e. Run this code from the command line using the following command:
    
    	ruby temp_conversions.rb
    
    f. Once this is running, set up a git repository and add this file to it 	(Please do not spend much time on this, make sure you ask a teaching member if you don't remember how to do this from the previous labs).


2. Add the test `puts convert("zero")` to the tests and rerun the code normally.  Why did you get an error?  To correct this, we will limit all temperatures to integers by adding a line before the calculation in our method: 

  ```ruby
  return "Temperature must be an integer" unless temp.class == Integer
  ``` 

	Rerun these tests after adding this line.  If the tests pass, add the revision to the git repository.

	**Note:** Notice that if we want to return before the end of method, we need to use the return keyword, but if the method runs its course, the last value is automatically returned by the method.  Finally, notice the use of the inline If (where the the condition is placed at the end of the line).

3. Add the test `puts convert(-500)` to the tests and rerun.  Of course, remembering your basic physics leaves you distressed at this point because you know this answer is in error – Absolute Zero is at –474 degrees Fahrenheit or -270 degrees Celsius, making this result impossible.  To make sure our program doesn't give silly answers, we will add another line after the last correction (and before the calculation): 

  ```ruby
  return "Temperature below Absolute Zero" if temp < -474 
  ```
  Rerun the tests; assuming they pass, save the revision to the git repository.

4. Of course, we have only half the temperature conversion problem – converting Fahrenheit to Celsius – and have no capability to convert Celsius to Fahrenheit.  Create a new branch in git called `exp` and switch to it.  Now in your code, add another argument called `measure` and using an `if ... else ... end` construct, correct the code so that either a Fahrenheit or Celsius temperature is converted.  Set up the `measure` argument so its default value is "F".  Add the test below:

  ```ruby  
  puts convert(0, "C")
  puts convert(10, "C")
  puts convert(100, "C")
  puts convert(-280, "C")
  ```

	Rerun the code; if all tests pass, save to the repository.

5. Looking at the results, we see that the code is still problematic: we get a result for –280 oC even though we know that value is below Absolute Zero.  There are a number of ways to correct this, but for learning purposes here, we are going to create a new method called `below_absolute_zero?` which has two arguments: `temp` and `measure`.  This method will simply return a boolean of `true` if the temperature for the measurement system is below the critical value; this is why this method will end in a question mark. Create the basic structure for this method now.

  ```ruby
  def below_absolute_zero?(temp, measure)
		# your code goes here
  end
  ```
  
6. Back to the code: go to the convert method and change the if statement for the Absolute Zero condition so that it references this new method rather than the simple statement of `temp < -474`.  Rerun the code and make sure that everything is working properly.  If so, save this code to the git repository. Checkout the `master` branch, and then merge the `exp` branch onto the `master` branch.

- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 1**. Show a CA that you have completed the first part by testing the convert and below_absolute_zero? and showing her/him that they work fine. Also, make sure you show her/him the history of your git activity.

- - -



Part 2: Interactive Ruby
==========

Interactive Ruby or `irb` is an interactive programming environment that comes with Ruby.
Under `irb`, Ruby will show the results of any Ruby statements you feed it without the use of any printing command (puts, print). Playing with Ruby code in interactive sessions like this is a terrific way to learn the language.

1. We are going to switch gears now and start to interact with Ruby with `irb`.  The irb prompt is a useful command line tool that can allow you to try out simple ruby constructs and methods.

2. Once in irb, type 

  ```ruby 
  a = Time.now
  ``` 
  
  This gives us an object a with a Ruby timestamp.  Now type in 
  
  ```ruby
  require 'date'
  b = Date.today
  ``` 
  
  Compare this result with the results of the first command.  What is the difference between these two objects? Be sure you are clear on the difference before proceeding.
  
3. Now type `a.month` and note what is output is. Now type `a.strftime("%B")` and note the output. How would you find the year of `a`? (Guess ...)  Try your idea in irb now.

	`strftime` which basically means 'format time' is a method we use for time formatting. We use it to get almost any format we need.

4. Now type the command 

  ```ruby 
  a.month == b.month
  ```
  
  What was returned?  
  
  Type the command 
  
  ```ruby 
  a.day == b.day - 1
  ```
  
 	and see that result as well. As we noted earlier in the temp conversion 	method, Ruby is evaluating these statements as either true or false and 	returning the result.
  
5. Use the `strftime` method to format the object `a` in the format of 99/99/9999.  To see the options with `strftime`, please refer to [strfti.me](http://strfti.me/).

6. We are going to add three variables at once through multiple assignment (an option in Ruby). To do this, type into irb: 
  ```ruby
  m1, d1, y1 = 04, 01, 2014
  ```  
  Now we will use these values to create a new timestamp in Ruby with the command:
  
  ```ruby
  c = Time.mktime(y1, m1, d1)
  ```
  
  Now we have the timestamp for this year's April Fool's Day.  Let's change it a little bit by typing `d1 = 31` and rerunning the command: `c = Time.mktime(y1, m1, d1)`.  What did Ruby do with the date 04/31/2014?


- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 2**. Show a CA/TA that you completed this part successfully! Take a screenshot of the console with all the commands you executed using irb.


Part 3: Ruby Blocks
==========

In this part of the lab, you will work through block problems from a previous 67-272 exam. This section contains 4 problems, but you only need to complete the first 3 for full credit. However, you are encouraged to complete them all if time allows! They will be good practice for future exams and your projects.

In each problem, you will be given an expected output, and your task is to write a block that will generate this output. You can complete the problems in a separate file, and run it the same way as TempConverter.

Add the following dictionaries to the top of your file, as these will be used in the problems.

  ```ruby
  cast = {bob_parr: :incredibles, helen_parr: :incredibles, lucius: :incredibles, 
          edna: :incredibles, woody: :toy_story, buzz: :toy_story, bopeep: :toy_story, 
          andy: :toy_story, merida: :brave, marlin: :finding_nemo, dory: :finding_nemo, 
          nemo: :finding_nemo, sulley: :monsters_inc, mike: :monsters_inc, 
          randall: :monsters_inc, sally: :cars, mcqueen: :cars, doc: :cars, 
          mater: :cars, jessie: :toy_story_3, big_baby: :toy_story_3}

  toys = [:woody, :bopeep, :buzz, :jessie, :big_baby]

  females = [:helen_parr, :edna, :bopeep, :dory, :sally, :jessie, :merida]

  year_produced = {incredibles: 2004, toy_story: 1995, brave: 2012, finding_nemo: 2003, up: 2009, walle: 2008, monsters_inc: 2001, cars: 2006, bugs_life: 1998, toy_story_3: 2010}

  ```

1. Create a block that prints out all the female toys in alphabetical order.

  ```ruby
  # EXPECTED OUTPUT: 
    bopeep
    jessie
  ```

2. Create a block that will print out a list of all the movies produced in the past 10 years.

  ```ruby
  # EXPECTED OUTPUT: 
    [:brave, :toy_story_3]
  ```

3. Create a block that will print out a list of movies that have some cast members in the cast dictionary, arranged by year produced.

  ```ruby
  # EXPECTED OUTPUT: 
    Toy_story - 1995
    Monsters_inc - 2001
    Finding_nemo - 2003
    Incredibles - 2004
    Cars - 2006
    Toy_story_3 - 2010
    Brave - 2012
  ```

4. Create a block that will print out a list of all movies in the year_produced dictionary in a user-friendly format (spacing and capitalization). Make sure they are in alphabetical order.

  ```ruby
  # EXPECTED OUTPUT: 
    Brave
    Bugs Life
    Cars
    Finding Nemo
    Incredibles
    Monsters Inc
    Toy Story
    Toy Story 3
    Up
    Walle
  ```

- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 3**. Show a TA/CA that you finished solving 3 problems in this part.The TA/CA will check your git log for the history of your git activity.
- - -

On your Own
===========

This week for the "on your own" section, your job is to complete the following two parts: 

1. Write a method called `valid_date?` which takes year, month and day as arguments and returns true if the date is valid or false if not.  Below are some test cases.

  ```
   # Tests
  valid_date?(2013, 1, 29) # => true
  valid_date?(2013, 2, 28) # => true
  valid_date?(2013, 2, 29) # => false
  valid_date?(2014, 2, 29) # => false
  valid_date?(2014, 9, 29) # => true
  valid_date?(2014, 9, 31) # => false
  valid_date?(2013, 12, 31) # => true
  valid_date?(2013, 12, 32) # => false
  valid_date?(2013, 13, 31) # => false
  valid_date?("2014", "Jan", 31) # => false
  
  ```

2. Review HTML, CSS, and basic JavaScript. If you don't remember much from HTML & CSS, please refer to the following tutorials to brush up your skills:

	- [HTML Tutorial](https://www.w3schools.com/html/)
	- [CSS Tutorial](https://www.w3schools.com/css/)
