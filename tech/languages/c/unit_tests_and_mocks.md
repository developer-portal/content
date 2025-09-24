---
title: Unit Tests and Mocks
subsection: c
order: 5
---

# Unit tests

Unit tests are an efficient way to improve software quality. They are especially well suited if you want to avoid code regressions due to code modifications.

A unit test is a snipet of code which exercises only a small portion of the whole software. It is usually made of three parts:
* prepare the inputs,
* call the function under test,
* check that something went well.

Each unit test can be viewed as a small constraint on the possible behaviours of the software. Run together several small unit tests can greatly increase your confidence in the code base. A test is also a form of executable documentation: if you break a test you can read its name and scenario to understand the intent of the code that was just modified.

AUM is a library that lets you easily write and execute unit tests in C. The latest releases, installation instructions and documentation are available [here](https://github.com/airbus-cyber/aum).
Here is an example that gives you a concrete exemple of AUM in action:

```c
AUM_TEST(malloc__should_return_a_non_null_pointer)
{
  char *result = malloc(10 * sizeof(char));
  AUM_ASSERT_PTR_NOT_NULL(result);
  free(result);
}
```

This test checks that calling function `malloc` returns a non-null pointer.

# Mocks

Sometimes, when writing tests, it is necessary to control the behavior of a function. It could be that the function can not be run automatically; for instance in the case of user interactions or network accesses. Or that you want to exercise corner cases; for instance when the program runs out of memory, or when file accesses fail. In these cases, you use function mocks.

Here is a test with a mock of `malloc` written with AUM:

```c
AUM_MOCK_CREATE(void *, malloc, size_t);

AUM_TEST(aum_mock_will_return__should_set_return_code)
{
  aum_mock_will_return("malloc", 0);

  char *result = malloc(10 * sizeof(char));
  AUM_ASSERT_PTR_NULL(result);
}
```

In this example, function `malloc` is replaced by a mock which is supposed to always return `NULL`.

# Some best practices

Here are some best practices related to unit tests:
* If you don't want to spend too much time on writing tests, a cost-effective approach consists in introducing at least one new test for each bug that is detected and fixed.
* Better, you can follow Test Driven Development (TDD): it roughly consists in writing each test before the corresponding code. If your project is starting from scratch, then you are in the ideal situation for TDD: you will be able to achieve 100% code coverage at a relatively low cost.
* At least, it is always profitable to set up a continuous integration server to build, analyse and test your code. In doing so, you know at all times whether everything still works or not.



