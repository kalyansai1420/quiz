# Quiz Game in Go

This is a simple quiz game written in Go. The game reads questions and answers from a CSV file and quizzes the user.

## Getting Started

### Prerequisites

- Go (version 1.16 or later)

### Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/kalyansai/quiz.git
    cd quiz
    ```

2. Build the project:
    ```sh
    go build
    ```

### Usage

1. Prepare a CSV file with questions and answers in the format [`question,answer`](command:_github.copilot.openSymbolFromReferences?%5B%22question%2Canswer%22%2C%5B%7B%22uri%22%3A%7B%22%24mid%22%3A1%2C%22fsPath%22%3A%22%2Fhome%2Fkalyanmaram%2Fgo%2Fquiz%2Fmain.go%22%2C%22external%22%3A%22file%3A%2F%2F%2Fhome%2Fkalyanmaram%2Fgo%2Fquiz%2Fmain.go%22%2C%22path%22%3A%22%2Fhome%2Fkalyanmaram%2Fgo%2Fquiz%2Fmain.go%22%2C%22scheme%22%3A%22file%22%7D%2C%22pos%22%3A%7B%22line%22%3A11%2C%22character%22%3A79%7D%7D%5D%5D "Go to definition"). For example:
    ```
    5+5,10
    7-3,4
    12/4,3
    ```

2. Run the quiz game:
    ```sh
    ./quiz-game -csv=problems.csv
    ```

### Code Explanation

The main logic of the quiz game is in the [`main.go`](command:_github.copilot.openRelativePath?%5B%7B%22scheme%22%3A%22file%22%2C%22authority%22%3A%22%22%2C%22path%22%3A%22%2Fhome%2Fkalyanmaram%2Fgo%2Fquiz%2Fmain.go%22%2C%22query%22%3A%22%22%2C%22fragment%22%3A%22%22%7D%5D "/home/kalyanmaram/go/quiz/main.go") file. Here's a brief overview:

1. **Flag Definition and Parsing:**
    ```go
    csvFilename := flag.String("csv", "problems.csv", "a csv file in the format of 'question,answer'")
    flag.Parse()
    ```

2. **File Opening:**
    ```go
    file, err := os.Open(*csvFilename)
    if err != nil {
        exit(fmt.Sprintf("Failed to open the CSV file: %s\n", *csvFilename))
    }
    ```

3. **CSV Reading:**
    ```go
    r := csv.NewReader(file)
    lines, err := r.ReadAll()
    if err != nil {
        exit("Failed to parse the provided CSV file.")
    }
    ```

4. **Parsing Lines:**
    ```go
    problems := parseLines(lines)
    ```

5. **Quiz Logic:**
    ```go
    correct := 0
    for i, p := range problems {
        fmt.Printf("Problem #%d: %s = \n", i+1, p.q)
        var answer string
        fmt.Scanf("%s\n", &answer)
        if answer == p.a {
            correct++
        }
    }
    fmt.Printf("You scored %d out of %d. \n", correct, len(problems))
    ```

### Contributing

1. Fork the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Make your changes.
4. Commit your changes (`git commit -am 'Add new feature'`).
5. Push to the branch (`git push origin feature-branch`).
6. Create a new Pull Request.
