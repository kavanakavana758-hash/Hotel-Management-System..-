# Hotel-Management-System..-
#include <iostream>
#include <fstream>
#include <vector>
#include <string>
#include <iomanip>

using namespace std;

// ================= ROOM CLASS =================
class Room
{
private:
    int roomNumber;
    string roomType;
    double price;
    bool booked;

public:
    Room()
    {
        roomNumber = 0;
        roomType = "";
        price = 0;
        booked = false;
    }

    Room(int number, string type, double p)
    {
        roomNumber = number;
        roomType = type;
        price = p;
        booked = false;
    }

    int getRoomNumber() const
    {
        return roomNumber;
    }

    string getRoomType() const
    {
        return roomType;
    }

    double getPrice() const
    {
        return price;
    }

    bool isBooked() const
    {
        return booked;
    }

    void setBooked(bool status)
    {
        booked = status;
    }

    void displayRoom() const
    {
        cout << left
             << setw(12) << roomNumber
             << setw(15) << roomType
             << setw(12) << price
             << setw(12) << (booked ? "Booked" : "Available")
             << endl;
    }
};

// ================= CUSTOMER CLASS =================
class Customer
{
private:
    int customerId;
    string name;
    string phone;
    string email;
    int roomNumber;

public:
    Customer()
    {
        customerId = 0;
        name = "";
        phone = "";
        email = "";
        roomNumber = 0;
    }

    Customer(int id, string n, string p, string e, int room)
    {
        customerId = id;
        name = n;
        phone = p;
        email = e;
        roomNumber = room;
    }

    int getCustomerId() const
    {
        return customerId;
    }

    string getName() const
    {
        return name;
    }

    string getPhone() const
    {
        return phone;
    }

    string getEmail() const
    {
        return email;
    }

    int getRoomNumber() const
    {
        return roomNumber;
    }

    void displayCustomer() const
    {
        cout << "\nCustomer ID : " << customerId;
        cout << "\nName        : " << name;
        cout << "\nPhone       : " << phone;
        cout << "\nEmail       : " << email;
        cout << "\nRoom Number : " << roomNumber << endl;
    }
};

// ================= HOTEL CLASS =================
class Hotel
{
private:
    vector<Room> rooms;
    vector<Customer> customers;

    const string roomFile = "rooms.txt";
    const string customerFile = "customers.txt";

public:

    // Constructor
    Hotel()
    {
        loadRooms();
        loadCustomers();

        // Create default rooms if no room file exists
        if (rooms.empty())
        {
            createDefaultRooms();
            saveRooms();
        }
    }

    // ================= CREATE ROOMS =================
    void createDefaultRooms()
    {
        rooms.push_back(Room(101, "Single", 1500));
        rooms.push_back(Room(102, "Single", 1500));
        rooms.push_back(Room(103, "Single", 1500));

        rooms.push_back(Room(201, "Double", 2500));
        rooms.push_back(Room(202, "Double", 2500));
        rooms.push_back(Room(203, "Double", 2500));

        rooms.push_back(Room