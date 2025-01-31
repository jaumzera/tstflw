# TstFlw

**TstFlw** is a lightweight testing utility for Java that helps you write tests using a clean, readable _Given/When/Then-like_ structure, without requiring
complex BDD frameworks. It focuses on **simplicity**, **clarity**, and minimizing boilerplate in your test code.

---

## Advantages & Benefits of Adoption

- **Enhanced Readability**  
  Keeps your tests straightforward by clearly separating the **action** (`when()`) from the **assertions** (`then()`).

- **Reduced Boilerplate**  
  Eliminates the need for additional setup/teardown frameworks. Everything is encapsulated in a single class (`TstFlw`) plus an anonymous inner class (or
  subclass) that you create in your test.

- **BDD-Like Structure Without Overhead**  
  Encourages a **Given/When/Then** approach without introducing the complexity of external BDD tools.

- **Consistent Testing Style**  
  By applying the same pattern across your project, team members can quickly understand and maintain tests.

- **Optional Final Step**  
  Need to run extra checks or resource cleanup? Override the `end()` method.

- **Easy Integration With JUnit**  
  Works seamlessly with JUnit (and other test frameworks). Just call `TstFlw.given(...)` inside your test methods.

---

## Getting Started

### Maven Dependency

If TstFlw is published to a Maven repository (e.g., Maven Central or your own internal repo), add it to your `pom.xml`:

    <dependency>
        <groupId>com.yourorg</groupId>
        <artifactId>tstflw</artifactId>
        <version>1.0.0</version>
        <scope>test</scope>
    </dependency>

*(Replace `com.yourorg`, `tstflw`, and `1.0.0` with your actual coordinates.)*

#### If Not Published

1. **Clone** or **download** the repository:

       git clone https://github.com/yourusername/tstflw.git

2. **Install** it locally with Maven:

       cd tstflw
       mvn clean install

3. **Add** the same `<dependency>...</dependency>` snippet above to your project’s `pom.xml`. Maven will resolve TstFlw from your local repository.

---

## Usage Example

Below is a simple test illustrating how to use **TstFlw** in JUnit:

    import static org.junit.jupiter.api.Assertions.assertEquals;
    import org.junit.jupiter.api.Test;

    public class MyTest {

        @Test
        void exampleTest() {
            TstFlw.given(new TstFlw.Task() {

                private int valueUnderTest;

                @Override
                public void when() {
                    // Main action under test:
                    valueUnderTest = 1 + 1;
                }

                @Override
                public void then() {
                    // Verification step:
                    assertEquals(2, valueUnderTest);
                }

                @Override
                public void end() {
                    // Optional final step:
                    System.out.println("Test finished successfully.");
                }
            });
        }
    }

1. **`when()`** – Put the logic or code under test here.
2. **`then()`** – Use assertions to verify the outcome.
3. **`end()`** – An optional method for any final checks or cleanup.

---

## Complete Source Code

Here is the entire **TstFlw** class for quick reference:

    public class TstFlw {
        public static abstract class Task {

            private Task _when() {
                when();
                return this;
            }

            private Task _then() {
                then();
                return this;
            }

            public abstract void when();
            public abstract void then();

            public void end() {
                // Override if you need it.
            }
        }

        public static void given(Task given) {
            given._when()._then().end();
        }
    }

- **`TstFlw.Task`**: Extend this abstract class (via an anonymous class or named subclass).
- **`given(Task given)`**: Orchestrates the execution flow of `when()`, then `then()`, then `end()`.

---

## Contributing

We welcome contributions! Here’s how you can help:

1. **Report Issues**  
   If you spot a bug or have a feature request, please open an issue in the repository.

2. **Submit Pull Requests**  
   Fork this repository, implement your changes, and open a pull request with a clear description.

3. **Suggest Improvements**  
   Open an issue or start a discussion if you have ideas for new features, improvements, or additional examples.

### Building & Testing Locally

1. **Clone** the repository:

       git clone https://github.com/yourusername/tstflw.git

2. **Build** with Maven:

       mvn clean install

3. **Run tests**:

       mvn test

---

## License

**TstFlw** is an open-source project. Two popular and permissive licenses often used are:

- **[MIT License](https://opensource.org/licenses/MIT)**
- **[Apache License 2.0](https://opensource.org/licenses/Apache-2.0)**

Both allow commercial and private use, distribution, modification, and sublicensing.  
Here’s the full **MIT License** text for your convenience:

    MIT License

    Copyright (c) 20XX YOUR NAME

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in
    all copies or substantial portions of the Software.

    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
    IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
    FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
    AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
    LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
    OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
    THE SOFTWARE.

Thank you for using **TstFlw**! If you have any questions or suggestions, feel free to open an issue or a pull request.
