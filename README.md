Lab 4: TempConverter; irb; loops, Conditionals, Strings
=

Objectives:
=

- Learn the basics of Ruby programming
- Learn how to use coditional structures and loops in Ruby
- Learn how to work with Strings and Arrays in Ruby
- Learn to use irb command prompt
- Improve familiarity with basic git commands
- Learn how to work with Time class in Ruby

Due Date:
= 
**February, 3rd 2022** by the end of the lab session.

Important Note
= 
 In this lab, you have a total of **5 checkpoints** to validate with one of the teaching team members. 
 
Checkpoints will be graded as follows:

* Checkpoint 1: 20 points
* Checkpoint 2: 20 points
* Checkpoint 3: 20 points
* Checkpoint 4: 20 points
* Checkpoint 5: 20 points

All your work should be staged and committed in a dedicated git repository.

Part 1: Ruby Introduction and Conditionals
===========

This part of the lab will get everyone familiar with some Ruby basics and provides a review of other key concepts. 

1. We are going to begin by writing a simple program for Ruby to convert temperatures and then modify it several times. 

	a. First, open Visual Studio Code and connect to your CMUQ dedicated server via `ssh-remote`. Please review the steps provided in this [tutorial](https://canvas.cmu.edu/courses/26286/modules/items/5060523), if needed.
	
	b. In the terminal, create a new folder named `lab4` (`mkdir lab4` then`cd lab4`), where you will save all your ruby files for this lab. 
		
	
	b. Now create a new file called `temp_conversions.rb`. In VS Code, just use `File --> new File`. Then save the file as a Ruby file. Do not forget to indicate the `.rb` extension.
	
	c. In this file, create a method called `convert` that takes `temp` as a parameter (temperature in Fahrenheit) and converts it to its equivalent in Celsius. Check this [link] to get the Fahrenheit to Celsius formula.
	
	d. Create some simple tests for this method with the code below:
	
	```ruby
	  puts convert(32)          
	  puts convert(50)          
	  puts convert(212)
	```
	 
    e. Run this code from the command line using the following command:
    
    	ruby temp_conversions.rb
    
    f. Once this is running, set up a git repository and add this file to it 	(Please do not spend much time on this, make sure you ask a teaching member if you don't remember how to do this from the previous labs).


2. Add the test `puts convert("zero")` to the tests and rerun the code normally.  Why did you get an error?  

	a. To correct this, we will limit all temperatures to integers by adding a line before the calculation in our method: 

  ```ruby
  return "Temperature must be an integer" unless temp.class == Integer
  ``` 

 	Rerun these tests after adding this line.  If the tests pass, add the revision to the git repository.

   The Ruby `unless` statement xecutes code **if the condition is false**. If the condition is true, the code specified in the else clause is executed.
	`unless` is the logical opposite of `if`.

 b. Ruby offers also conditional structures that are pretty common to modern languages. Let's check how we could solve the same using an `if` statement.
 
  ```ruby
  	return "Temperature must be an integer" if temp.class != Integer
  ``` 

**Note:** Notice that if we want to return before the end of method, we need to use the return keyword, but if the method runs its course, the last value is automatically returned by the method.  Finally, notice the use of the inline If (where the the condition is placed at the end of the line).

3. Add the test `puts convert(-500)` to the tests and rerun.  Of course, remembering your basic physics leaves you distressed at this point because you know this answer is in error – Absolute Zero is at –474 degrees Fahrenheit or -270 degrees Celsius, making this result impossible.  To make sure our program doesn't give silly answers, we will add another line after the last correction (and before the calculation): 

  ```ruby
  return "Temperature below Absolute Zero" if temp < -474 
  ```
 
 Rerun the tests; assuming they pass, save the revision to the git repository.
  We call this an **inline if**. It is usually used in this format `<code if condition>` and used when only one condition is to be tested. It executes code if the condition is true.

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

7. More on Conditionals:

- Create a new Ruby file named `conditionals.rb`

- When only one condition is to be tested, we use the `if` modifier as in the following example. Copy this code and paste it in conditionals.rb. Then run it using `ruby conditionals.rb`.

```ruby
age=35
if age < 105
	puts "don't worry, you are still young!"
end
```

**Note**: The conditional testing happens within a block that starts with `if` and finishes with `end`. The `end` is mandatory.

- The `if/elsif/else/end` conditional structure: copy the code below and run it.

	```ruby
	x = 1
	if x > 2
	   puts "x is greater than 2"
	elsif x <= 2 and x!=0
	   puts "x is 1"
	else
	   puts "I can't guess the number"
	end
	``` 
 Notice that Ruby uses `elsif`, not `else if` nor `elif`.

- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 1**. Show a CA that you have completed the first part by testing the convert and below_absolute_zero? and showing her/him that they work fine. Also, make sure you show her/him the history of your git activity.

- - -

Part 2: Ruby Loops 
===========
Looping in programming languages is a feature which clears the way for the execution of a set of instructions or functions repeatedly  when some of the condition evaluates to true or false.  Ruby provides the different types of loop to handle the condition based situation in the program to make the programmers task simpler. 

1. Create a new Ruby file named `loops.rb` and add to it all the Ruby codes given in the next questions of this part (2 to 9).

2. Looping with `for`

		for variable_name in expression  
		
		     # # code to be executed
		end
		
	In a for loop, the expression could be a range, an array, keys in a hash.
	
	a. Using an array: 
	
	Add the following lines in loops.rb and test it.

			array = [10, 91, 2, 333, 4, 5]
			for elem in array
			     puts elem
			end
			
			array2 = ["hi", "you", "ruby", "programming"]
			for elem in array2
				puts elem
			end

	b. Using Range
		- In Ruby, `1..5` is an object of type **Range**
		- Ruby creates sequences using the ".."" range operator.
		- A Sequence has a start point, an end point and way to produce successive values.
		- `1..5` generates the sequence `1, 2, 3, 4, 5`

			for i in 1..5 
			     puts "Value of local variable is #{i}"
			     puts array[i]
			end

3. Looping with while

The syntax of While loops is similar to Python with a small difference: the `end` at the end of the loop is mandatory

		index=0
		while index<array.length
		     puts "Value of current element is #{array[index]}"
		     index+=1
		end
		
Another example

		n = 0
		while n < 4
		  puts n
		  n += 1
		end
		
4. Looping with the `times` method in Ruby

 This is the easiest loop you can work with.
 
 a. Try the following Ruby code:
 
		30.times {puts "I will not throw paper airplanes"} \
 
 This code prints the message "I will not throw paper airplanes" 30 times.

b. But what if we want the iterator (iterative index)? We can do this using the iterator offered in times. 

	75.times { |i| puts "hello #{i}" }


`times` is a Ruby built-in method that takes a **block** (a block of code with a set of instructions as an 'argument'). We will discuss blocks more in details in the next lecture.


5. Lopping with the `each` Ruby method

The `each`  Ruby method allows you to go over a list of items,  without having to keep track of the number of iterations, or having to increase some kind of counter. We tell the `each` method what to do with every item by using a **block**.

The general syntax of each is as follows:

		(expression).each do |element| 
		     your instructions here 
		end

6. We can use the each method to iterate over the individual items in an range (a sequence). Read the code below and test it.

		(1..4).each do |element|
		     puts "The Value of the local variable element is #{element}"
		     element=element/20
		     puts element
		     if element%2==0
		          puts "the element is even!"
		     end
		end
		
And this is equivalent to 
		
		range= 1..4
		range.each do |element|
		    puts "The Value of the local variable element is #{element}"
		end

7. We can use each to iterate over the elements of an array

		# Array of integers
		[1, 2, 3, 4].each do |element|
		     puts "The Value of the local variable i is #{element*65}"
		end
		
		# Array of strings
		string_array=["a", "b","c", "d"]
		string_array.each do |item|
		     puts "The value of i is #{item.upcase}"
		end

8. When one instuction is included in the block, we can write it as follows

		string_array.each {|item| puts "The current array item is #{item}"}

9. We can also manipulate items inside of an each block, unless we reassign the new value to the item in the array,  the following code will leave the original array unchanged

		array = [100, 11, 25, 36, 47, 5]
		array.each do |item|
		  item = item + 2
		  puts "The current item + 2 is #{item}."
		end
		

**Note**: More on loops: https://www.rubyguides.com/ruby-tutorial/loops/

- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 2**. Show a CA/TA that you completed this part successfully!
- - -

Part 3: Ruby Strings 
===========
Whether written in Ruby or another language almost every software needs to work with text. A series of characters is a String. **Strings in Ruby are Objects**. Working with Strings in Ruby is very easy.  Ruby provides over 170 methods you can call on strings: methods that do things like: splitting them into pieces, capitalizating them, and more.

1. In Ruby strings are represented Single quotes

		puts 'I am a string'

	Or double quotes

		puts "Me too!"

2. **String methods in Ruby**

Let's explore some of the methods we can call on strings

		phrase="i AM arthur, king of the britons"
		puts phrase.class  # ==> String
		puts phrase.length # ==> 32

	a. `capitalize`: Returns a new string by converting its first character uppercase and the remaining to lowercase.
	
		puts phrase.capitalize # ==> I am arthur, king of the britons

	b. `upcase`: Returns a new string with all lowercase letters replaced with their uppercase counterparts.

		puts phrase.upcase # ==> I AM ARTHUR, KING OF THE BRITONS

	c. `downcase`: Returns a new string with all uppercase letters replaced with their lowercase counterparts. 
	
		puts phrase.downcase # ==> i am arthur, king of the britons

	d. reverse: Returns a new string with the characters from the given string in reverse order.
	
		puts phrase.reverse # ==> snotirb eht fo gnik ,ruhtra MA i
		
	We can also combine different String methods:
	
		puts phrase.upcase.reverse # ==> SNOTIRB EHT FO GNIK ,RUHTRA MA I

		puts phrase # ==> i AM arthur, king of the britons

	e. `split`: a method which is used to split the given string into an array of substrings  based on a pattern specified. str is divided where the pattern matches. the default pattern is a 'space'.

		p phrase.split #==> ["i", "AM", "arthur,", "king", "of", "the", "britons"]
		p phrase.split('a') # ==> ["i AM ", "rthur, king of the britons"]
		p phrase.split(',')  #==> ["i AM arthur", " king of the britons"]

	f. `index`: am method which is used to return the index of the first occurrence of the given substring or pattern in the given string.  It specifies the position in the string to begin the search if the second parameter is present.  It will return **nil** if not found. Please note that indexing a string starts at 0.

		puts phrase.index('a') # ==> 5
		puts phrase.index('i') # ==>0
		puts phrase.index('i', 2) # ==>14
		puts phrase.index('z') # ==>  nothing is printed
		p phrase.index('z') # ==> nil

3. **String slicing**

Similarly to Python, we use the [] to slice a String. The main difference is that the start index and end index are both included
		
		puts phrase[5..10] #==>  arthur (the character at position 10 is included)
		puts phrase.nil? # checks if phrase is  nil
		puts !phrase.nil? # checks if phrase is not nil
	
4. **String concatenation**

We can use different operators and methods to concatenate strings in Ruby.

	puts "hello "+"world" # using +   ==> hello world
	puts "hello "<<"world" # using the push operation ==> hello world
	puts "hello ".concat "world" # using concat  ==> hello world

5. **String repetition/multiplication**

We use the '*' operator to repete a string.

		puts "hello"*3 # ==> hellohellohello
		puts "7"*3 # ==> 777 and not 21

6. **String comparison in Ruby**: Please explore the code below. Run it and make sure the results you obtain matches the ones mentioned with comments

		s="zebra"
		puts s <"ant" # ==> false
		puts s >"ant" #  ==> true
		puts s =="ant" #  ==> false
		puts s =="zebra" #  ==> true
		puts s =="ZEBRA" #  ==> false
		puts s == "ant".length # ==> false

7. **String Interpolation in Ruby**

	As we already saw in Wednesday's lecture, Ruby provides a feature called string interpolation that lets you substitute the result of Ruby code into the middle of a string.
	
	Anywhere you want within the string, you can include an interpolation marker.A marker consists of a hash mark (also known as a pound sign), an opening curly brace, and a closing curly brace: `#{}`.
	
	You can include any Ruby code you want between the curly braces. The code will be evaluated, the result will be converted to a string, and the resulting string will be substituted for the interpolation marker within the containing string.
	
	String interpolation lets us:
		- concatenate values like numbers with strings.
		- embed simple math operations within a string
		- embed any code to be interpreted by Ruby in within a string
	
	a. Let's look at some examples:

		age=35
		puts "Your age is "+age 
	
	This code gives you an errors, as you are trying to concatenate a String and an Integer. A possible solution would be to use the to_s method

		puts "Your age is "+age.to_s
	
	Or use String Interpolation

		puts "Your age is #{age}" # ==> prints Your age is 35
		puts "Your age is #{age/47.0}"
	
	b. Interpolation works within double-quoted Ruby strings. No interpolation in single-quoted strings.

		puts 'Your age is #{age}' # ==> prints Your age is #{age}


 	c. We can include multiple interpolation markers into a single string.

		puts "is #{age+47} even? #{(age+47).even?}"

8. **String escape sequences in Ruby **

Below are some of the more common escape sequences that can appear inside of double quotes.

-\n: skips to a new line

-\t: indents text: adds a tabulation

-\": inserts double quotes

-\': inserts single quotes

-\\: inserts a backslash \

a. Try the following examples, to check how the esacape sequences work in practice

	puts "first line\nsecond line"
	puts "\tnewparagraph"
	puts "he said, \"Whoa\""


9. **Ruby destructive methods**

	All ruby methods that end with the exclamation mark, for example, `downcase!` or `capitalize!` are called **destructive methods **( also mutator methods, dangerous methods). 
	
	The usual methods perform an action on a copy of the object and then return copy, Destructive methods perform an action and change the object itself, returning the modified object as a result.
	
	Check the examples below.

	str="i AM arthur, king of the britons"
	puts str.capitalize # this will not change the value of the object str
	puts str #==> prints i AM arthur, king of the britons

	str.capitalize! # this will print the modified str object
	puts str # prints I am arthur, king of the britons

	`capitalize!` is Equivalent to:

		str=str.capitalize
	
- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 3**. Show a CA/TA that you completed this part successfully!
- - -

Part 4: Arrays in Ruby
==========

So far the basic types that we've learned about are strings and numbers. 
Let's say we would like to create a shopping list.  Within the shopping list our grocery items could be something like: milk, eggs, and bread.
We could store that list in a string, for example separated by commas. Or we could use an array as a data container.  Arrays can store any type of data that we have access to in Ruby. 

1. **Array Creation**

	a. Create an empty array
	
		
		grocery_list = Array.new #=> creates an empty Array []
		puts  grocery_list
		# Or
		p grocery_list
		
		
	`p` displays the raw version of the array while `puts` displays a human readable version (a string version of it)
	
	b. Everything in Ruby is an Object.  So, creating an array is about instantiating the class `Array` to create the object `grocery_list`.
	
	
		puts "grocery_list is a: #{grocery_list.class}"
		
		
	The `.class` method returns the class of the object. This should return Array.
	
	c. We can create an empty array using the following as well, they are both equivalent:
	
	
		grocery_list= []
		puts "grocery_list is a: #{grocery_list.class}"
	
	
	d. To check if an array is empty, we use the `empty?` Array built-in method
		
	
		puts "Is the grocery list empty?:  #{grocery_list.empty?}"

	
	e. Let's create an array with items
	
		
		grocery_list= ["milk", "eggs", "bread"]
		p grocery_list
		
		prices= ["10", "30", "5"]
		p prices
		
		a = Array.new([5,4,6])
		p a
		
	
	f. Another way to create an Array of strings in Ruby, where we do not have to surround the array items with quotes
	
		
		grocery_list=%w(milk eggs bread)
		p grocery_list # this prints ["milk", "eggs", "bread"]
		
	
	g. **Note**: Never create an array with different object types. The following array declaration is possible syntactically, but not recommended to do.
	
		
		array= ["hello", "67-272", "Ruby is amazing", 76, 98]
		p array
	
	
	h. We can use the `inspect` to return a printable version of the array in an array format.
	
	
		puts grocery_list.inspect
	

2. **Adding items in an array**

	a. We can add items at the end of an array using the append operator <<
	
	
		grocery_list<< "carrots" 
		p grocery_list
		

	b. We can add items at the end of an array using the `push` method
	
	```ruby
	grocery_list.push("potatoes")
	p grocery_list
	```
	c. We can add items at the end of an array using the `+=` operator
	
	```ruby
	grocery_list+=["ice cream", "pie"]
	# equivalent to 
	grocery_list= grocery_list+["ice cream", "pie"]
	
	grocery_list+=["tomatoes"]
	p grocery_list
	```
	d. We can add items at the beginning of an array using the `unshift` method
	
	```ruby
	grocery_list.unshift("strawberry")
	p grocery_list
	```
	e. We can add items in the middle of an array
	
	The following code is bad, becuase it erases the content of the array at that index
	
	```ruby
	# grocery_list[2]= "oatmeal" 
	# p grocery_list
	```
	A better way
	
	```ruby
	grocery_list.insert(2, "oatmeal")
	puts "The new content of my array: #{grocery_list}"
	```
	
3. **Accessing items in an array**

	a. To access the first item in an array, we can use the [], exactly like in Python
		
		
		p grocery_list[0] 
	
	  We can also use the `at` available Array instance method.
		
	
		p grocery_list.at(0)
	
	  We can use the `first` Array instance method
	 
		p grocery_list.first
	
	b. To access the last item in an array, we can use the [], exactly like in Python
	
	
		p grocery_list[-1] # last item in an array
	
	 We can use the `last` Array instance method
		 
		
		p grocery_list.last 

4. **Array slicing**

	a. Array Slicing in Ruby works exactly as for List slicing in Python using []
	
		p grocery_list[0,3]
	
	The syntax here is`array[start_index, stop_index]` where the the item at stop_index is not included
	
	b. we can also use the `slice` method that takes to parameters: (1) the start index and (2) how many items to consider.
	
		p grocery_list.slice(0,3) 
		
5. **Removing items from arrays in Ruby**
puts "Grocery list before: #{grocery_list}"
last_item= grocery_list.pop # the pop method deletes the last item in an array and returns it (the item)
p last_item
puts "Grocery list after removing the last item: #{grocery_list}"


first_item=grocery_list.shift # the shift method deletes the first item in an array and returns it (the item)
puts "Grocery list after removing the first item: #{grocery_list}"


6. **Other array methods in Ruby**

	a. to check if an array contains an item, we use either the `any?` or `include?` built-in predicate methods

		p grocery_list.any?("potatoes") # this prints true
		
		p grocery_list.any?("water") # this prints false
	 
		p grocery_list.include?("water") # false

	b. get the number of elements in an array
	
		p grocery_list.length
	or 
	
		p grocery_list.count 
	c. We can use the `count` method to count the number of occurrences of an element in an array
	
		p grocery_list.count("eggs") 


	d. To get the list of Array methods available for you, you can use the `methods` method 
	
		p grocery_list.methods
		
- - -
# <span class="mega-icon mega-icon-issue-opened"></span> Stop

**Checkpoint 4**. Show a CA/TA that you completed this part successfully!
- - -

Part 5: Interactive Ruby
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
  
 and see that result as well. As we noted earlier in the temp conversion method, Ruby is evaluating these statements as either true or false and returning the result.
  
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

**Checkpoint 5**. Show a CA/TA that you completed this part successfully! Take a screenshot of the console with all the commands you executed using irb.

<!--
Part 5: Ruby Blocks
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
-->