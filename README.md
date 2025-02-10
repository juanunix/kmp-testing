📐 ComprehensiveCalculatorTest

This repository contains the ComprehensiveCalculatorTest class, which is designed to thoroughly test the functionality of the ComprehensiveCalculator class.

The tests ensure that various mathematical operations and state management are functioning correctly.

📋 Table of Contents
About the Code

Dependencies

Setup

Tests

📖 About the Code
The ComprehensiveCalculatorTest class includes several unit tests that verify different operations of the ComprehensiveCalculator. These operations include addition of integers and floats, state management, and async operations.

Key Features
Uses Experimental Coroutines API: Annotated with @OptIn(ExperimentalCoroutinesApi::class).

Custom Test Dispatcher: Utilizes StandardTestDispatcher for coroutine-related tests.

State Flow Testing: Ensures correct state flow updates and async result fetching.

📦 Dependencies
To run these tests, you'll need the following dependencies:

Kotlin Coroutines

Kotlin Test

kotlinx.coroutines.test

Add these dependencies to your build.gradle.kts:

kotlin
```
dependencies {
    testImplementation("org.jetbrains.kotlinx:kotlinx-coroutines-test:1.5.2")
    testImplementation("org.jetbrains.kotlin:kotlin-test:1.5.31")
}
```
⚙️ Setup
Before running the tests, set up the main dispatcher and reset it after each test:

kotlin
```
@BeforeTest
fun setUp() {
    Dispatchers.setMain(testDispatcher)
}

@AfterTest
fun tearDown() {
    Dispatchers.resetMain()
}
```
🧪 Tests
The following tests are included in the ComprehensiveCalculatorTest:

Addition of Integers: Verifies that 2 + 2 equals 4.

kotlin

```
@Test
fun `add integers two plus two returns four`() {
    // Arrange
    val a = 2
    val b = 2
    val expected = 4

    // Act
    val actual = calculator.addIntegers(a, b)

    // Assert
    assertEquals(expected, actual, "Sum should be 4")
}
```

Addition of Floats: Verifies that 2.5 + 3.5 equals 6.0.

kotlin

```
@Test
fun `add floats two point five plus three point five returns six`() {
    // Arrange
    val a = 2.5f
    val b = 3.5f
    val expected = 6.0f

    // Act
    val actual = calculator.addFloats(a, b)

    // Assert
    assertEquals(expected, actual, 0.0001f, "Sum should be 6.0")
}
```

State Increment: Verifies that incrementing the state once sets it to 1.

kotlin
```

@Test
fun `increment state once increments by one`() {
    // Arrange
    calculator.incrementState()
    val expected = 1

    // Act
    val actual = calculator.getState()

    // Assert
    assertEquals(expected, actual, "State should be incremented by 1")
}
```

Fetch Result Asynchronously: Verifies that async fetching returns 42.

kotlin

```
@Test
fun `fetch result async returns expected result`() = runBlocking {
    // Arrange
    val expected = 42

    // Act
    val actual = calculator.fetchResultAsync()

    // Assert
    assertEquals(expected, actual, "Result should be 42")
}
```

Fetch Result Flow: Verifies that the flow emits 1, 2, 3.

kotlin
```

@Test
fun `fetch result flow returns expected flow`() = runBlocking {
    // Arrange
    val expected = listOf(1, 2, 3)

    // Act
    val actual = calculator.fetchResultFlow().toList()

    // Assert
    assertContentEquals(expected, actual, "Flow should emit 1, 2, 3")
}
```

Update State Flow: Verifies state flow updates to 5.

kotlin
```
@Test
fun `update state flow updates state flow value`() = testScope.runTest {
    // Arrange
    val newValue = 5
    val expected = 5

    // Act
    val deferredResult = async { calculator.updateStateFlow(newValue) }
    advanceTimeBy(500L)
    deferredResult.await()
    val actual = calculator.stateFlow.value
}
```
