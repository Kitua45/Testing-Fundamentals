Testing Fundamentals with Jest & TypeScript
 Overview

This project demonstrates Testing Fundamentals in JavaScript/TypeScript using the Jest framework.
It covers the complete lifecycle of writing, structuring, and organizing unit tests for utility functions — focusing on AAA (Arrange, Act, Assert) and the FIRST-U testing principles.

The tests are written for functions such as product, authenticateUser, and UserNameToLowerCase, showcasing:

Use of Jest matchers

Test grouping and isolation

Parameterized testing

Test hooks (beforeAll, afterAll, etc.)

Coverage reporting

Test reliability and reusability

 Learning Objectives

Understand and apply the AAA (Arrange → Act → Assert) testing structure.

Write clean, isolated, and repeatable unit tests.

Explore the FIRST-U principle for effective test design.

Use Jest matchers to validate a wide range of expectations.

Work with Jest lifecycle hooks for setup and teardown.

Implement parameterized tests for multiple data inputs.

Generate and interpret coverage reports.

 Technologies Used
Tool	Purpose
TypeScript	Strong typing for clean, maintainable test code
Jest	Testing framework
ts-jest	Enables Jest to run TypeScript test files
ts-node	Executes .ts Jest config files
@types/jest	Jest type definitions for TypeScript

 Project Setup

1️ Install dependencies
npm install --save-dev jest ts-jest ts-node typescript @types/jest

2 Initialize Jest for TypeScript
npx ts-jest config:init


This creates a preconfigured Jest setup for TypeScript projects.

 Example Jest Configuration (jest.config.ts)
import type { Config } from "jest";

const config: Config = {
  preset: "ts-jest",
  testEnvironment: "node",
  verbose: true,
  collectCoverage: true,
  coverageDirectory: "coverage",
};

export default config;

 Test Suites Breakdown

1️ BasicUtils Test Suite

Tests the product() and authenticateUser() utility functions.

Key highlights:

Demonstrates matchers such as toBe, toEqual, toBeCloseTo, toContain, toBeTruthy, etc.

Follows the AAA pattern (Arrange, Act, Assert).

Verifies both primitive and reference type comparisons.

Example:

test("should return the product of two positive numbers", () => {
  const actual = product(3, 4);
  const expected = 12;
  expect(actual).toBe(expected);
});

2️ FIRST-U Principle Suite

Applies the FIRST-U principle to testing design:

F – Fast

I – Isolated

R – Repeatable

S – Self-validating

T – Timely

U – Unique

Tests are organized logically to ensure each case tests only one behavior of the code.

Example:

it("should authenticate valid user", () => {
  const actual = authenticateUser("deveLOPER", "dev");
  expect(actual.isAuthenticated).toBeTruthy();
});

3 Jest Hooks Suite

Shows the use of Jest lifecycle hooks:

beforeAll / afterAll

beforeEach / afterEach

These simulate setup and teardown activities in a test lifecycle.

Example:

beforeEach(() => {
  username = "deveLOPER";
});
afterEach(() => {
  username = "";
});


Tests include edge cases such as error throwing:

expect(() => UserNameToLowerCase("")).toThrow("Username cannot be empty");


Note: The suite is marked with describe.skip to demonstrate how Jest can skip certain suites during testing.

4️ Parameterized Tests Suite

Demonstrates data-driven testing using test.each() and it.each().

This approach runs the same test logic with multiple input/output combinations — ideal for repetitive or formula-based logic.

Example:

test.each([
  [3, 4, 12],
  [5, 6, 30],
  [7, 8, 56],
  [2, 9, 18]
])("product(%i, %i) should return %i", (a, b, expected) => {
  expect(product(a, b)).toBe(expected);
});


Also includes parameterized tests for string functions:

it.each([
  ["deveLOPER", "developer"],
  ["KEMBOI", "kemboi"],
  ["JaneDoe", "janedoe"]
])("UserNameToLowerCase(%s) should return %s", (input, expected) => {
  expect(UserNameToLowerCase(input)).toBe(expected);
});

 Coverage Reports

To generate test coverage:

npx jest --coverage


This produces a /coverage folder with detailed metrics for:

Statements

Branches

Functions

Lines

Use /* istanbul ignore next */ to exclude specific lines from coverage reports.

 Key Concepts Practiced
Concept	Description
AAA Pattern	Structure tests into Arrange, Act, Assert
FIRST-U Principle	Qualities of well-written unit tests
Matchers	Assertions used to compare actual vs expected
Hooks	Setup/teardown logic around test execution
Parameterized Tests	Run one test logic with multiple datasets
Coverage Analysis	Measure how much code is tested
 How to Run Tests

Run all tests
pnpm run test

Run a specific suite or file
npx jest path/to/file.test.ts

Run with watch mode
npx jest --watch

Skip or focus specific tests
describe.skip("...") // skip this suite
test.only("...")     // run only this test

 Summary

This testing project demonstrates:

Professional-level unit testing discipline

Best practices using Jest and TypeScript

Proper test structure, isolation, and clarity

Readable, reusable, and maintainable tests

It lays a solid foundation for expanding into:

Integration testing

Mocking external services

End-to-end (E2E) testing
