# GeneticAlgorithms-CSE316
Implementation Overview
In this lab, I implemented a Genetic Algorithm (GA) to solve the N-Queens problem using a function-based (procedural) programming style in Python.

Although there are multiple approaches to designing genetic algorithms, such as object-oriented programming (OOP) with classes, my implementation correctly follows the essential genetic algorithm workflow:

Population Initialization: Randomly generating an initial population of possible board configurations.

Fitness Evaluation: Scoring each board based on the number of non-attacking queen pairs.

Selection: Selecting parent boards for reproduction based on their fitness scores.

Crossover: Combining parts of two parents to produce offspring.

Mutation: Randomly altering some parts of the offspring to maintain genetic diversity.

Iteration over Generations: Repeating the process for a fixed number of generations or until an optimal solution is found.

📌 Limitations
While the implementation is functional and achieves the problem-solving goal, it has some limitations:

No Chessboard Display: The program outputs the queen positions as a list, without a visual board representation.

Fixed Mutation Probability: The mutation chance is hardcoded and not easily adjustable without modifying the code.

Lacks Class-based Structure: The program is function-based and does not use a class-based, modular design, which limits code reusability, readability, and future scalability.

📌 Future Improvements
For future enhancements, the following improvements are recommended:

Implement a class-based (OOP) version for better structure and maintainability.

Add a visual chessboard display for better understanding of the results.

Make mutation rates and other parameters configurable without changing the source code.

How to Run Your Code (Using VS Code)
To run the Genetic Algorithm code for solving the N-Queens problem using Visual Studio Code (VS Code):

Open VS Code.

Create a new folder for your project (optional but recommended).

Inside the folder, create a new file and name it something like n_queens_ga.py.

Paste the Python code into that file.

Make sure you have Python installed and configured in VS Code. If not:

Install Python from python.org.

Install the Python extension in VS Code (from the Extensions tab).
write the code
press f5 to run or
Open a terminal in VS Code (Ctrl + ~ or go to Terminal > New Terminal).

Run the code using this command:

bash
Copy
Edit
python n_queens_ga.py
You will see the output printed in the terminal once a solution is found or the algorithm finishes trying.



Project Objectives
To understand the core concepts of Genetic Algorithms.

To apply GA methods to solve the N-Queens problem.

To evaluate the effectiveness of GA in finding solutions to combinatorial problems.

To explore how genetic operations (selection, crossover, and mutation) influence the search for optimal solutions.
## Code

<pre> ```python import random def create_board(size): return [random.randint(0, size - 1) for _ in range(size)] def score_board(board): score = 0 size = len(board) for i in range(size): for j in range(i + 1, size): if board[i] != board[j] and abs(board[i] - board[j]) != abs(i - j): score += 1 return score def pick_parents(boards, scores): best_score = max(scores) chances = [s / best_score for s in scores] return random.choices(boards, weights=chances, k=2) def mix_boards(a, b): cut = random.randint(0, len(a) - 1) return a[:cut] + b[cut:], b[:cut] + a[cut:] def tweak_board(board, chance=0.1): if random.random() < chance: spot = random.randint(0, len(board) - 1) board[spot] = random.randint(0, len(board) - 1) return board def solve_queens(size, group_size=100, tries=1000): boards = [create_board(size) for _ in range(group_size)] best_possible = (size * (size - 1)) // 2 for step in range(tries): scores = [score_board(b) for b in boards] if best_possible in scores: winner = boards[scores.index(best_possible)] print(f"Found solution at step {step}: {winner}") return winner next_gen = [] while len(next_gen) < group_size: parent1, parent2 = pick_parents(boards, scores) child1, child2 = mix_boards(parent1, parent2) next_gen.append(tweak_board(child1)) if len(next_gen) < group_size: next_gen.append(tweak_board(child2)) boards = next_gen print("No perfect solution found.") return None if __name__ == "__main__": final = solve_queens(8) print("Final result:", final) ``` </pre>

