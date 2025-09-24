# ESEP Grade Calculator

This library is a simple utility to calculate your grades.

### Runtime requirements:
Golang 1.24+ (Download at https://go.dev/dl)

Run
```
go version
```
after downloading to ensure the correct version is being used.

### Grade Calculator Functions
```
func NewGradeCalculator() *GradeCalculator

ex usage.
gradeCalculator := NewGradeCalculator()
```
creates and returns a reference to the GradeCalculator containing array information on the assignments, exams, and essays.

```
func (gc *GradeCalculator) AddGrade(name string, grade int, gradeType GradeType)

ex usage.
gradeCalculator.AddGrade("AI Essay", 90, Essay)

```
adds a grade to the GradeCalculator arrays sorted by GradeType. It takes in the name of the grade, the grade integer, and the type of grade (Assignment, Exam, Essay). Returns nothing.

```
func (gc *GradeCalculator) calculateNumericalGrade() int

ex usage.
numericalGrade := gradeCalculator.calculateNumericalGrade()
This is used to get the letter grade in the GetFinalGrade function.

```
calculates the numerical grade of all grades in the arrays of Assignments, Exams, and Essays by averaging the results and calculating a weighted grade based on the weights for each category. Returns the numerical weighted grade.

```
func computeAverage(grades []Grade) int

ex usage.
numericalAvg := computAverage(gradeCalculator.assignments)
This is used to calculate in calculateNumericalGrade function.
```
calculates the average of the given grade array and returns the average as an integer.

```
func (gc *GradeCalculator) GetFinalGrade() string

ex usage.
letterGrade := gradeCalculator.GetFinalGrade()
```
translates a numerical weighted grade to a letter grade and returns it as a string.


### Creating a Unit Test
General format for a single test will be. In this example, we test for
the expected letter grade.
```
func TestName(t *testing.T) {
    // set the expected output variable information
    expected_value := "A"

    gradeCalculator := NewGradeCalculator()

    // add grade information so something like below
    gradeCalculator.AddGrade("Assignment 1", 100, Assignment)
    gradeCalculator.AddGrade("Exam 1", 100, Exam)
    gradeCalculator.AddGrade("AI Essay", 100, Essay)

    // get the actual value of what you are testing
    actual_value := gradeCalculator.GetFinalGrade()

    // compare the expected and actual values and return a PASS/FAIL
    if expected_value != actual_value {
		t.Errorf("Expected GetGrade to return '%s'; got '%s' instead", expected_value, actual_value)
	}
}
```

### Run unit tests:
Ensure the path is ../grade_calculator or you are in the grade_calculator folder and then run below to run all test files.
```
cd grade_calculator/
go test ./...
```

### Run unit tests with code coverage:
Ensure the path is like the unit tests above (in the grade_calculator folder), run the below to get a report of unit tests.
```
cd grade_calculator/
go test -coverprofile=coverage.txt ./...
```