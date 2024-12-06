class StudentGradeManager:
    def __init__(self):
        self.grades = []
        self.grade_history = []

    def input_grades(self):
        print("Enter grades for different subjects or assignments.")
        while True:
            try:
                grade = float(input("Enter grade (0-100) or type 'done' to finish: "))
                if 0 <= grade <= 100:
                    self.grades.append(grade)
                else:
                    print("Grade must be between 0 and 100. Try again.")
                continue_input = input("Do you want to enter another grade? (yes/no): ").lower()
                if continue_input != "yes":
                    break
            except ValueError:
                break

    def calculate_average(self):
        if self.grades:
            return sum(self.grades) / len(self.grades)
        else:
            return 0

    def calculate_letter_grade(self, average):
        if average >= 90:
            return 'A'
        elif average >= 80:
            return 'B'
        elif average >= 70:
            return 'C'
        elif average >= 60:
            return 'D'
        else:
            return 'F'

    def calculate_gpa(self, average):
        if average >= 90:
            return 4.0
        elif average >= 80:
            return 3.0
        elif average >= 70:
            return 2.0
        elif average >= 60:
            return 1.0
        else:
            return 0.0

    def display_results(self):
        average = self.calculate_average()
        letter_grade = self.calculate_letter_grade(average)
        gpa = self.calculate_gpa(average)
        print("\nSummary:")
        print(f"Grades: {self.grades}")
        print(f"Average Grade: {average:.2f}")
        print(f"Letter Grade: {letter_grade}")
        print(f"GPA: {gpa:.2f}")

    def add_grade_to_history(self):
        history_entry = {
            "grades": self.grades,
            "average": self.calculate_average(),
            "letter_grade": self.calculate_letter_grade(self.calculate_average()),
            "GPA": self.calculate_gpa(self.calculate_average())
        }
        self.grade_history.append(history_entry)

    def view_grade_history(self):
        if self.grade_history:
            print("\nGrade History:")
            for index, entry in enumerate(self.grade_history, start=1):
                print(f"Entry {index}: Grades: {entry['grades']}, Average: {entry['average']:.2f}, "
                      f"Letter Grade: {entry['letter_grade']}, GPA: {entry['GPA']:.2f}")
        else:
            print("No grade history available.")

    def main_menu(self):
        while True:
            print("\nStudent Grade Manager")
            print("1. Enter Grades")
            print("2. Display Results (Average, Letter Grade, GPA)")
            print("3. View Grade History")
            print("4. Exit")
            choice = input("Choose an option (1/2/3/4): ")

            if choice == '1':
                self.input_grades()
                self.add_grade_to_history()
            elif choice == '2':
                self.display_results()
            elif choice == '3':
                self.view_grade_history()
            elif choice == '4':
                print("Goodbye!")
                break
            else:
                print("Invalid choice. Please try again.")


# Running the program
if __name__ == "__main__":
    manager = StudentGradeManager()
    manager.main_menu()
