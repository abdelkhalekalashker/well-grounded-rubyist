# well-grounded-rubyist
## Chapter 6

### 6.2. Repeating actions with loops
#### 6.2.1. Unconditional looping with the loop method (infinite loop)
  ```
  loop { puts "Looping forever!" }
  loop do
    puts "Looping forever!"
  end
  ```
#### 6.2.2. Conditional looping with the while and until keywords
  ```
  n = 1
  while n < 11
    puts n
    n = n + 1
  end
  puts "Done!"
  ```

  ```
  n = 1
  until n > 10
    puts n
    n = n + 1
  end
  ```





### 6.4
  ```
  if tourney_roster2.players&.first&.position == "Forward"
    puts "Forward: #{tourney_roster1.players.first.name}"
   end
   ```
  the "&" in the previuose code is called safe navigation operator, we can use the safe navigation operator to avoid the NoMethodError The safe navigation operator tells Ruby to only call the next method if the receiver isn’t nil. Otherwise, the expression returns nil
#### 6.4.8. Creating your own exception classes
  it`s preferred to use unique errors instead system errors like NoMethodError
  ```
  class MyNewException < Exception
  end
  raise MyNewException, "some new kind of error has occurred!"
  ```
  This technique offers two primary benefits. 
  First, by letting you give new names to exception classes, it performs a self-documenting function: when a MyNewException gets raised, it’s distinct from, say, a ZeroDivisionError or a plain-vanilla RuntimeError.

  Second, this approach lets you pinpoint your rescue operations. Once you’ve created MyNewException, you can rescue it by name:
  ```
  class MyNewException < Exception
  end
  begin
    puts "About to raise exception..."
    raise MyNewException
  rescue MyNewException => e
    puts "Just raised an exception: #{e}"
  end
  ```
InvalidLineError provides a meaningful exception name and refines the semantics of the rescue operation.

