#include <iostream>
#include <string>
#include <vector>
#include <iomanip>
#include <limits>

using namespace std;


struct Seat {
    int number;
    bool isBooked;
};


struct Bus {
    string type;
    double price;
    vector<Seat> seats;
};


int getValidatedInput(int min, int max) {
    int input;
    while (true) {
        cin >> input;
        if (cin.fail() || input < min || input > max) {
            cout << "Input tidak valid, masukkan angka antara " << min << " dan " << max << ": ";
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
        } else {
            break;
        }
    }
    return input;
}

// Fungsi login
bool login() {
    string username, password;
    const string correctUsername = "admin";
    const string correctPassword = "123";

    for (int attempts = 3; attempts > 0; --attempts) {
        cout << "\nMasukkan username: ";
        cin >> username;
        cout << "Masukkan password: ";
        cin >> password;

        if (username == correctUsername && password == correctPassword) {
            cout << "Login berhasil!\n";
            return true;
        } else {
            cout << "Username atau password salah. Percobaan tersisa: " << attempts - 1 << "\n";
        }
    }

    cout << "Anda telah gagal login sebanyak 3 kali. Program keluar.\n";
    return false;
}


void printDestinations() {
    cout << "\nPilih jurusan perjalanan:\n";
    cout << "1. Jogja - Magelang\n";
    cout << "2. Jogja - Solo\n";
    cout << "3. Jogja - Semarang\n";
    cout << "4. Jogja - Surabaya\n";
    cout << "5. Jogja - Cirebon\n";
}


void printBusOptions(vector<Bus> &buses) {
    cout << "\nPilih jenis bus:\n";
    for (size_t i = 0; i < buses.size(); ++i) {
        cout << i + 1 << ". " << buses[i].type << " (Rp " << fixed << setprecision(0) << buses[i].price << ")\n";
    }
}


void bookingSystem() {
    
    vector<Bus> buses = {
        {"Ekonomi", 50000, vector<Seat>(20)},
        {"Patas", 80000, vector<Seat>(20)},
        {"Eksekutif", 120000, vector<Seat>(20)}
    };

    
    for (auto &bus : buses) {
        for (size_t i = 0; i < bus.seats.size(); ++i) {
            bus.seats[i] = {static_cast<int>(i + 1), false};
        }
    }

    string customerName;
    cout << "\nMasukkan nama Anda: ";
    cin.ignore();
    getline(cin, customerName);

    printDestinations();
    cout << "Masukkan pilihan jurusan (1-5): ";
    int destinationChoice = getValidatedInput(1, 5);

    printBusOptions(buses);
    cout << "Masukkan pilihan jenis bus (1-3): ";
    int busChoice = getValidatedInput(1, 3);

    Bus &selectedBus = buses[busChoice - 1];

    cout << "\nBerapa tiket yang ingin Anda pesan? (1-5): ";
    int ticketCount = getValidatedInput(1, 5);

    vector<int> bookedSeats;
    for (int i = 0; i < ticketCount; ++i) {
        cout << "\nKursi tersedia: ";
        for (const auto &seat : selectedBus.seats) {
            if (!seat.isBooked) {
                cout << seat.number << " ";
            }
        }

        cout << "\nPilih nomor kursi: ";
        int seatNumber = getValidatedInput(1, selectedBus.seats.size());

        if (!selectedBus.seats[seatNumber - 1].isBooked) {
            selectedBus.seats[seatNumber - 1].isBooked = true;
            bookedSeats.push_back(seatNumber);
        } else {
            cout << "Kursi " << seatNumber << " sudah dipesan. Pilih kursi lain.\n";
            --i;
        }
    }

    double totalPrice = selectedBus.price * ticketCount + 5000; 

   
    cout << "\n====================================================\n";
    cout << "Tiket Anda:\n";
    cout << "Nama: " << customerName << "\n";
    cout << "Jurusan: " << destinationChoice << "\n";
    cout << "Jenis Bus: " << selectedBus.type << "\n";
    cout << "Kursi: ";
    for (const auto &seat : bookedSeats) {
        cout << seat << " ";
    }
    cout << "\nJumlah Tiket: " << ticketCount << "\n";
    cout << "Total Harga: Rp " << fixed << setprecision(0) << totalPrice << "\n";
    cout << "====================================================\n";
}

int main() {
    cout << "Selamat datang di Sistem Pemesanan Tiket Bus\n";
    if (!login()) {
        return 0;
    }
    bookingSystem();
    return 0;
}
