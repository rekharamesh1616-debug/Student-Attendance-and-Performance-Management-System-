# Student-Attendance-and-Performance-Management-System-students = {}

def add_student():
    roll = int(input("Enter roll number: "))
    name = input("Enter name: ")
    students[roll] = {
        "name": name,
        "attendance": [],
        "marks": None
    }
    print("Student added successfully!\n")

def mark_attendance():
    roll = int(input("Enter roll number: "))
    if roll in students:
        status = input("Enter attendance (P/A): ").upper()
        if status in ["P", "A"]:
            students[roll]["attendance"].append(status)
            print("Attendance marked!\n")
        else:
            print("Invalid attendance input!\n")
    else:
        print("Student not found!\n")

def enter_marks():
    roll = int(input("Enter roll number: "))
    if roll in students:
        marks = int(input("Enter marks (out of 100): "))
        students[roll]["marks"] = marks
        print("Marks entered successfully!\n")
    else:
        print("Student not found!\n")

def calculate_attendance_percentage(att_list):
    if len(att_list) == 0:
        return 0
    present = att_list.count("P")
    return (present / len(att_list)) * 100

def warning_list():
    print("\nLOW ATTENDANCE WARNING LIST")
    for roll, data in students.items():
        percent = calculate_attendance_percentage(data["attendance"])
        if percent < 75:
            print(f"Roll: {roll}, Name: {data['name']}, Attendance: {percent:.2f}%")

def class_statistics():
    total_attendance = 0
    total_marks = 0
    count = len(students)

    for data in students.values():
        total_attendance += calculate_attendance_percentage(data["attendance"])
        if data["marks"] is not None:
            total_marks += data["marks"]

    if count > 0:
        print("\nCLASS STATISTICS")
        print(f"Average Attendance: {total_attendance / count:.2f}%")
        print(f"Average Marks: {total_marks / count:.2f}")
    else:
        print("No students available!")

def display_students():
    print("\nSTUDENT DETAILS")
    for roll, data in students.items():
        attendance_percent = calculate_attendance_percentage(data["attendance"])
        print(f"Roll: {roll}")
        print(f"Name: {data['name']}")
        print(f"Attendance: {attendance_percent:.2f}%")
        print(f"Marks: {data['marks']}")
        print("-" * 20)

# Main Menu
while True:
    print("\n===== STUDENT ATTENDANCE SYSTEM =====")
    print("1. Add student")
    print("2. Mark attendance")
    print("3. Enter marks")
    print("4. Display students")
    print("5. Low attendance warning")
    print("6. Class statistics")
    print("7. Exit")

    choice = int(input("Enter your choice: "))

    if choice == 1:
        add_student()
    elif choice == 2:
        mark_attendance()
    elif choice == 3:
        enter_marks()
    elif choice == 4:
        display_students()
    elif choice == 5:
        warning_list()
    elif choice == 6:
        class_statistics()
    elif choice == 7:
        print("Exiting program...")
        break
    else:
        print("Invalid choice!")
