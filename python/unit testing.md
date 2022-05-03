# Unit Tests
Unit tests are written in the Test_Case_Module_Name.py.  
There is a test case for each function in the module.  Each test case name is in the 'test_function_name' form.

``` python

class Test_Case_Name(unittest.TestCase):

    def test_function_name(self):

        self.assertEqual(function_name(paramater), expected_result)

if __name__=='__main__':

    unittest.main()

```

## Unit test methods

``` python

class Test_case_Name(unittes.TestCase):

    def test_method_name(self):

        object_instance = class_name(paramaters)

        self.assertEqual(object_instance.method(), output)

if __name__='__main__':

    unittest.main()

```