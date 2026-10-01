#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

class DuAn {
private:
    string maDuAn;
    string tenDuAn;
    string tenKhachHang;
    string ngayBatDau;
    string ngayKetThucDuKien;
    double nganSach;
    double tyLeHoanThanh;

public:
    // Ham nhap thong tin du an
    void nhap() {
        cout << "Nhap ma du an: ";
        getline(cin, maDuAn);

        cout << "Nhap ten du an: ";
        getline(cin, tenDuAn);

        cout << "Nhap ten khach hang: ";
        getline(cin, tenKhachHang);

        cout << "Nhap ngay bat dau: ";
        getline(cin, ngayBatDau);

        cout << "Nhap ngay ket thuc du kien: ";
        getline(cin, ngayKetThucDuKien);

        cout << "Nhap ngan sach: ";
        cin >> nganSach;

        cout << "Nhap ty le hoan thanh (%): ";
        cin >> tyLeHoanThanh;

        cin.ignore();
    }

    // Ham xuat thong tin du an
    void xuat() {
        cout << left
             << setw(12) << maDuAn
             << setw(25) << tenDuAn
             << setw(20) << tenKhachHang
             << setw(15) << ngayBatDau
             << setw(20) << ngayKetThucDuKien
             << setw(15) << nganSach
             << setw(15) << tyLeHoanThanh
             << endl;
    }

    // Ham lay ma du an
    string getMaDuAn() {
        return maDuAn;
    }

    // Ham lay ten du an
    string getTenDuAn() {
        return tenDuAn;
    }

    // Ham lay ngan sach
    double getNganSach() {
        return nganSach;
    }
};

int main() {
    DuAn da;

    da.nhap();

    cout << "\nTHONG TIN DU AN\n";

    cout << left
         << setw(12) << "Ma DA"
         << setw(25) << "Ten du an"
         << setw(20) << "Khach hang"
         << setw(15) << "Ngay BD"
         << setw(20) << "Ngay KT"
         << setw(15) << "Ngan sach"
         << setw(15) << "Hoan thanh"
         << endl;

    da.xuat();

    return 0;
}
