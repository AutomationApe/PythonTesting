# PythonTesting

Why do we test in Python?

    Testing is incredibly important, especially in large codebases as new changes can create crippling bugs/errors that can cause an application
    to fail in its purpose or even fail to run at all. Testing our code ensures that it will run how we expect, interact well with code that may
    have been written by another programmer, and is quality code.
    
How do we test in Python?

    One method of testing in Python is through the creation of a Python file dedicated solely to testing our code. We can use a built-in module
    called unittest to create unit tests that test our code.
    
    Let's have this hypothetical main.py file containing the following function:
    
    def do_stuff(num):
        return num + 5
    
    Now let's say we are creating a test.py file, this may look like this:
    
    import unittest
    import main
    
    class TestMain(unittest.TestCase):
        def test_do_stuff(self):
            test_param = 10
            result = main.do_stuff(test_param)
            self.assertEqual(result, 15)
            
    unittest.main()
    
    This code imports the necessary modules (in this scenario) and created a test class to execute our test. It includes a test function which 
    replicates the functionality of the function we have in our main.py file, and the last line "self.assertEqual(result, 15)" tells the test
    class to check if the results of the test function and the function in our main.py file match. This ensures that our function is working
    as intended, thus passing the test.
    
    Testing can also tell us how we can improve our code further, making it safer. For example, let's say we created a new test function that
    tests for string values. It will always error out, even if the string is a number since the data types will not match. So we may want to 
    improve our function via try-except statements:
    
    def do_stuff(num):
        try:
            return int(num) + 5
        except ValueError as err:
            return err
            
    Then we can improve our testing code further to give us more information about our function in main.py:
    
    def test_do_stuff2(self):
        test_param = "shkshks"
        result = main.do_stuff(test_param)
        self.assertTrue(isinstance(result, TypeError))
        
    This will test if our code is erroring out due to a type error and will return true if that is the case.
    
    The point of writing test code to break your functions in main.py is to make your function in main.py stronger, more efficient, and safer.
    Knowing how your code can break can help you bolster your code and make it stronger and more capable of error handling.
    
    Here is another example of code breaking in testing:
    
    def test_do_stuff3(self):
        test_param = None
        result = main.do_stuff(test_param)
        self.asserEqual(result, ValueError)
        
    This will check if the argument in the do_stuff function in main.py returns None. This is not our desired result, so now that we know our 
    code can break due to this, let's strengthen it!
    
    def do_stuff(num=0):
        try:
            if num:
                return int(num) + 5
            else:
                return "please enter number"
        except ValueError as err:
            return err
            
    Now our function has the ability to error handle for the following situations:
    * if no number has been entered, prompt the user to enter a number
    * if the value entered does not match the expected value, return an error
    
    We should also add the following line of code: 
    if __name__ == "__main__":
        unittest.main()
        
    This ensures that our file running our unit test is the main file.
