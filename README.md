# Project3
# Import necessary modules
import calendar
from datetime import datetime

class Caregiver:
    def __init__(self, name, phone, email, pay_rate):
        self.name = name
        self.phone = phone
        self.email = email
        self.pay_rate = pay_rate
        self.availability = {}  # Example: {'Monday AM': 'preferred', 'Monday PM': 'available'}

    def set_availability(self, day, shift, status):
        self.availability[f"{day} {shift}"] = status

class Schedule:
    def __init__(self, year, month):
        self.year = year
        self.month = month
        self.schedule = {}  # Example: {'2024-11-22 AM': 'Caregiver Name'}

    def assign_shift(self, date, shift, caregiver):
        self.schedule[f"{date} {shift}"] = caregiver

    def display_calendar(self):
        cal = calendar.HTMLCalendar().formatmonth(self.year, self.month)
        print(cal)  # You can save this HTML to a file and view it in a browser

class Payroll:
    def __init__(self):
        self.records = {}

    def calculate_weekly_pay(self, caregiver, hours_worked):
        pay = caregiver.pay_rate * hours_worked
        self.records[caregiver.name] = pay
        return pay

    def generate_report(self):
        total = sum(self.records.values())
        for name, pay in self.records.items():
            print(f"Caregiver: {name}, Weekly Pay: ${pay:.2f}")
        print(f"Total Payroll: ${total:.2f}")

# Example
# Create caregivers
caregiver1 = Caregiver("Alice", "555-1234", "alice@example.com", 20)
caregiver2 = Caregiver("Bob", "555-5678", "bob@example.com", 20)

# Set availability
caregiver1.set_availability("Monday", "AM", "preferred")
caregiver2.set_availability("Monday", "PM", "available")

# Create a schedule
schedule = Schedule(2024, 11)
schedule.assign_shift("2024-11-22", "AM", "Alice")
schedule.assign_shift("2024-11-22", "PM", "Bob")
schedule.display_calendar()

# Calculate payroll
payroll = Payroll()
payroll.calculate_weekly_pay(caregiver1, 30)
payroll.calculate_weekly_pay(caregiver2, 25)
payroll.generate_report()

 
