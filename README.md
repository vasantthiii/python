# Railway Ticket Booking System
# Author: [Your Name]
# Date: [Date]
# Description: A simple program to simulate a railway ticket booking system.

class RailwayBookingSystem:
    def __init__(self):
        """
        Initializes the railway booking system with a list of trains and an empty list of bookings.
        """
        self.trains = {
            "101": {"name": "Express Train", "seats": 50, "fare": 150},
            "102": {"name": "Superfast Train", "seats": 40, "fare": 250},
            "103": {"name": "Passenger Train", "seats": 100, "fare": 100}
        }
        self.bookings = []

    def display_trains(self):
        """
        Displays the available trains with their details.
        """
        print("\nAvailable Trains:")
        print("Train No | Train Name       | Seats Available | Fare")
        print("-" * 50)
        for train_no, details in self.trains.items():
            print(f"{train_no:<8} | {details['name']:<15} | {details['seats']:<15} | {details['fare']:<5}")

    def book_ticket(self):
        """
        Allows the user to book a ticket for a selected train.
        """
        self.display_trains()
        train_no = input("\nEnter the Train Number you want to book: ")
        if train_no in self.trains:
            train = self.trains[train_no]
            if train["seats"] > 0:
                name = input("Enter your name: ")
                age = int(input("Enter your age: "))
                seats = int(input("Enter number of seats to book: "))
                if seats <= train["seats"]:
                    train["seats"] -= seats
                    total_fare = seats * train["fare"]
                    self.bookings.append({
                        "name": name,
                        "age": age,
                        "train_no": train_no,
                        "train_name": train["name"],
                        "seats": seats,
                        "total_fare": total_fare
                    })
                    print(f"\nBooking successful! Total Fare: {total_fare} INR")
                else:
                    print("Insufficient seats available.")
            else:
                print("Sorry, no seats available on this train.")
        else:
            print("Invalid Train Number.")

    def view_bookings(self):
        """
        Displays the user's bookings.
        """
        if not self.bookings:
            print("\nNo bookings found.")
        else:
            print("\nYour Bookings:")
            print("Name    | Age | Train No | Train Name       | Seats | Total Fare")
            print("-" * 60)
            for booking in self.bookings:
                print(f"{booking['name']:<7} | {booking['age']:<3} | {booking['train_no']:<8} | {booking['train_name']:<15} | {booking['seats']:<5} | {booking['total_fare']} INR")

    def menu(self):
        """
        Displays the main menu and handles user inputs.
        """
        while True:
            print("\nRailway Ticket Booking System")
            print("1. View Available Trains")
            print("2. Book a Ticket")
            print("3. View My Bookings")
            print("4. Exit")
            choice = input("Enter your choice: ")
            if choice == "1":
                self.display_trains()
            elif choice == "2":
                self.book_ticket()
            elif choice == "3":
                self.view_bookings()
            elif choice == "4":
                print("Thank you for using the Railway Ticket Booking System!")
                break
            else:
                print("Invalid choice. Please try again.")

# Main Program Entry Point
if __name__ == "__main__":
    system = RailwayBookingSystem()
    system.menu()