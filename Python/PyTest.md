
PyTest is a python based test framework that enables us to write automated test cases.

###  Library to import

```python
import pytest
```

- File names should start or end with “**test**”, as in `test_example.py` or `example_test.py`.
- If tests are defined as methods on a class, the **class name** should start with “**Test**”, as in`TestExample`. The class should not have an `__init__` method.
- Test **method names or function names** should start with “**test_**”, as in `test_example`. **Methods with names that don’t match this pattern won’t be executed as tests.**

###  Test Function:

```python
def test_sum():  
	assert sum(1, 2) == **4**
```

Test Function Parametrization
	The builtin [pytest.mark.parametrize](https://docs.pytest.org/en/latest/reference.html#pytest-mark-parametrize-ref) decorator enables parametrization of arguments for a test function. We have passed following parameters to it-
	- **argnames** — a comma-separated string denoting one or more argument names, or a list/tuple of argument strings. Here, we have passed `num1`, `num2` and `expected` as 1st input , 2nd input and expected sum respectively.
	- **argvalues** — The list of argvalues determines how often a test is invoked with different argument values. If only one argname was specified argvalues is a list of values. If N argnames were specified, argvalues must be a list of N-tuples, where each tuple-element specifies a value for its respective argname. Here, we have passed a tuple of `(3,5,8)` inside a list where `3` is `num1`,`5` is`num2` and `8`is `expected sum.`

```python
import pytest

@pytest.mark.parametrize('num1, num2, expected',[(3,5,8), (-2,-2,-4), (-1,5,4), (3,-5,-2), (0,5,5)])
def test_sum(num1, num2, expected):  
        assert sum(num1, num2) == expected
```


### Fixtures

Fixtures can be used to share test data between tests, execute setup and teardown methods before and after test executions respectively.

``` python
import pytest
@pytest.fixture
def get_sum_test_data():
        return [(3,5,8), (-2,-2,-4), (-1,5,4), (3,-5,-2), (0,5,5)]
def test_sum(get_sum_test_data):
        for data in get_sum_test_data:
                num1 = data[0]
                num2 = data[1]
                expected = data[2]
                assert sum(num1, num2) == expected
```



### **Test case Markings**

Pytest allows to mark tests and then selectively run them.

By using the `pytest.mark` helper you can easily set metadata on your test functions. There are some builtin markers, for example:

-   [skip](https://docs.pytest.org/en/latest/skipping.html#skip) — always skip a test function
-   [skipif](https://docs.pytest.org/en/latest/skipping.html#skipif) — skip a test function if a certain condition is met
-   [xfail](https://docs.pytest.org/en/latest/skipping.html#xfail) — produce an “expected failure” outcome if a certain condition is met
-   [parametrize](https://docs.pytest.org/en/latest/parametrize.html#parametrizemark) to perform multiple calls to the same test function. (_We already discussed this above._)

In the above examples, We can mark the 1st test function as slow and only run that function.

```python
@pytest.mark.slow
def test_sum():  
    assert sum(1, 2) == 3

def test_sum_output_type():  
    assert type(sum(1, 2)) is int
```


Now, to run only slow marked tests inside file test_example.py we will use-

```python
pytest test_example.py -m slow
```

## **Cheatsheet to run pytest with different options**

```python
# keyword expressions 
# Run all tests with some string ‘validate’ in the name
pytest -k “validate”
# Exclude tests with ‘db’ in name but include 'validate'
pytest -k “validate and not db” 
#Run all test files inside a folder demo_tests
pytest demo_tests/
# Run a single method test_method of a test class TestClassDemo 
pytest demo_tests/test_example.py::TestClassDemo::test_method
# Run a single test class named TestClassDemo 
pytest demo_tests/test_example.py::TestClassDemo
# Run a single test function named test_sum
pytest demo_tests/test_example.py::test_sum
# Run tests in verbose mode: 
pytest -v demo_tests/
# Run tests including print statements: 
pytest -s demo_tests/
# Only run tests that failed during the last run 
pytest — lf
```