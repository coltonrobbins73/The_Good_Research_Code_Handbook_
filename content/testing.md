+++
title = 'Testing'
date = 2024-04-12T12:57:24-07:00
draft = false
weight = 6
+++

Testing refers to verifying the code is doing what you want under a broad range of circumstances. You can manually check this but it is exponentially better to set up automatic tests that you can refer back to throughout development.

### Unit testing

Unit testing focuses on a single function and relies heavily on the assert statement which checks for true statements. To create a unit test, simply craft assert statements for several different argument variables.

    assert my_function(x) = y
    assert my_function(z) = w

When you develop more complicated tests, you should set up a test suite in a separate script as in this example of a Fibonacci function:

    from src.fib import fib
    import pytest
    def test_typical():
        assert fib(1) == 1
        assert fib(2) == 1
        assert fib(6) == 8
        assert fib(40) == 102334155
    def test_edge_case():
        assert fib(0) == 0
    def test_raises():
        with pytest.raises(NotImplementedError):
            fib( -1)
        with pytest.raises(NotImplementedError):
            fib(1.5)

`pytest.raises` has a special use case for ensuring specific errors are caught.

### How much coverage?

Typical coverage rates should be from 80% - 100% of the code. However, it is reasonable to start off small by setting up tests for major functions and then adding them as needed.
