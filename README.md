# railway-reservation-system
import random

# Total seats
TOTAL_SEATS = 50
available_seats = list(range(1, TOTAL_SEATS + 1))
bookings = {}

def check_availability():
    print(f"\nAvailable Seats: {len(available_seats)}")

def book_ticket():
    if not available_seats:
        print("\n❌ No seats available!")
        return

    name = input("Enter Name: ")
    age = input("Enter Age: ")

    seat = available_seats.pop(0)
    booking_id = random.randint(1000, 9999)

    bookings[booking_id] = {
        "name": name,
        "age": age,
        "seat": seat
    }

    print(f"\n✅ Ticket Booked Successfully!")
    print(f"Booking ID: {booking_id}")
    print(f"Seat Number: {seat}")

def view_ticket():
    booking_id = int(input("Enter Booking ID: "))

    if booking_id in bookings:
        data = bookings[booking_id]
        print("\n🎟 Ticket Details")
        print(f"Name: {data['name']}")
        print(f"Age: {data['age']}")
        print(f"Seat: {data['seat']}")
    else:
        print("❌ Booking not found!")

def cancel_ticket():
    booking_id = int(input("Enter Booking ID to cancel: "))

    if booking_id in bookings:
        seat = bookings[booking_id]["seat"]
        available_seats.append(seat)
        available_seats.sort()
        del bookings[booking_id]

        print("✅ Ticket Cancelled Successfully!")
    else:
        print("❌ Invalid Booking ID!")

def menu():
    while True:
        print("\n--- Railway Reservation System ---")
        print("1. Check Availability")
        print("2. Book Ticket")
        print("3. View Ticket")
        print("4. Cancel Ticket")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == '1':
            check_availability()
        elif choice == '2':
            book_ticket()
        elif choice == '3':
            view_ticket()
        elif choice == '4':
            cancel_ticket()
        elif choice == '5':
            print("Thank you!")
            break
        else:
            print("Invalid choice!")

menu()
