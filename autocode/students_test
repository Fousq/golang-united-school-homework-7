package coverage

import (
	"os"
	"testing"
	"time"

	"github.com/stretchr/testify/assert"
)

const (
	SIMPLE_MATRIX = "1 2\n 3 4"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestLenShouldBeZero_whenPeopleInit(t *testing.T) {
	var people People
	peopleLen := people.Len()

	assert.Equal(t, 0, peopleLen)
}

func TestLenShouldBeNonZero_whenAddToPeople(t *testing.T) {
	people := People{Person{}}
	peopleLen := people.Len()

	assert.NotEqual(t, 0, peopleLen)
}

func TestLessBirthdayDiff(t *testing.T) {
	now := time.Now()
	people := People{Person{birthDay: now}, Person{birthDay: now.Add(-time.Hour * 1)}}

	isSecondLessFirst := people.Less(0, 1)
	isFirstLessSecond := people.Less(1, 0)

	assert.True(t, isSecondLessFirst)
	assert.False(t, isFirstLessSecond)
}

func TestLessFirstNameDiff(t *testing.T) {
	now := time.Now()
	people := People{Person{birthDay: now, firstName: "A"}, Person{birthDay: now, firstName: "B"}}

	isSecondLessFirst := people.Less(0, 1)
	isFirstLessSecond := people.Less(1, 0)

	assert.True(t, isSecondLessFirst)
	assert.False(t, isFirstLessSecond)
}

func TestLessLastNameDiff(t *testing.T) {
	now := time.Now()
	people := People{Person{birthDay: now, firstName: "T", lastName: "A"},
		Person{birthDay: now, firstName: "T", lastName: "B"}}

	isSecondLessFirst := people.Less(0, 1)
	isFirstLessSecond := people.Less(1, 0)

	assert.True(t, isSecondLessFirst)
	assert.False(t, isFirstLessSecond)
}

func TestLessBothEqual(t *testing.T) {
	now := time.Now()
	people := People{Person{birthDay: now, firstName: "T", lastName: "T"},
		Person{birthDay: now, firstName: "T", lastName: "T"}}

	isSecondLessFirst := people.Less(0, 1)
	isFirstLessSecond := people.Less(1, 0)

	assert.False(t, isSecondLessFirst)
	assert.False(t, isFirstLessSecond)
}

func TestSwap(t *testing.T) {
	person1 := Person{firstName: "T"}
	person2 := Person{firstName: "D"}
	people := People{person1, person2}

	assert.Equal(t, people[0], person1)
	assert.Equal(t, people[1], person2)

	people.Swap(0, 1)

	assert.Equal(t, people[1], person1)
	assert.Equal(t, people[0], person2)
}

func TestErrOnMismatchColsLenOnMatrix(t *testing.T) {
	strMatrix := "1 2\n 3"
	matrix, err := New(strMatrix)
	if assert.Error(t, err) {
		assert.Equal(t, err.Error(), "Rows need to be the same length")
		assert.Nil(t, matrix)
	}
}

func TestErrOnInvalidData(t *testing.T) {
	strMatrix := "1 2\n 3 a"
	matrix, err := New(strMatrix)
	if assert.Error(t, err) {
		assert.NotEqual(t, err.Error(), "Rows need to be the same length")
		assert.Nil(t, matrix)
	}
}

func TestMatrixNew(t *testing.T) {
	matrix, err := New(SIMPLE_MATRIX)

	assert.Nil(t, err)
	assert.NotNil(t, matrix)
}

func TestRows(t *testing.T) {
	strMatrix := "1 2\n 3 4\n 5 6"
	matrix, _ := New(strMatrix)

	rows := matrix.Rows()

	assert.Equal(t, 1, rows[0][0])
	assert.Equal(t, 2, rows[0][1])

	assert.Equal(t, 3, rows[1][0])
	assert.Equal(t, 4, rows[1][1])

	assert.Equal(t, 5, rows[2][0])
	assert.Equal(t, 6, rows[2][1])
}

func TestCols(t *testing.T) {
	strMatrix := "1 2\n 3 4\n 5 6"
	matrix, _ := New(strMatrix)

	rows := matrix.Cols()

	assert.Equal(t, 1, rows[0][0])
	assert.Equal(t, 3, rows[0][1])
	assert.Equal(t, 5, rows[0][2])

	assert.Equal(t, 2, rows[1][0])
	assert.Equal(t, 4, rows[1][1])
	assert.Equal(t, 6, rows[1][2])
}

func TestSetOnRowNegative(t *testing.T) {
	matrix, _ := New(SIMPLE_MATRIX)

	isSet := matrix.Set(-1, 0, 10)

	assert.False(t, isSet)
}

func TestSetOnRowExceedsMatrix(t *testing.T) {
	matrix, _ := New(SIMPLE_MATRIX)

	isSet := matrix.Set(10, 0, 10)

	assert.False(t, isSet)
}

func TestSetOnColNegative(t *testing.T) {
	matrix, _ := New(SIMPLE_MATRIX)

	isSet := matrix.Set(0, -1, 10)

	assert.False(t, isSet)
}

func TestSetOnColExceedsMatrix(t *testing.T) {
	matrix, _ := New(SIMPLE_MATRIX)

	isSet := matrix.Set(0, 10, 10)

	assert.False(t, isSet)
}

func TestSet(t *testing.T) {
	matrix, _ := New(SIMPLE_MATRIX)

	isSet := matrix.Set(0, 0, 10)

	assert.True(t, isSet)
	assert.Equal(t, 10, matrix.data[0])
}
