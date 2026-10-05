# YÊU CẦU: bấm vào bút để xem code và chỉnh sửa lại code của mình để thống nhất và làm slide






#include <iostream>
#include <string>
#include <iomanip>
#include <cctype>
#include <limits>
using namespace std;

// Lop Du An
class Duan {
private:
    string maduan;
    string tenduan;
    string tenkhachhang;
    string ngaybatdau;
    string ngayketthuc;
    double ngansach;
    double tylehoanthanh;

public:
    void nhap();
    void xuat();

    double getNgansach();
    string getMaduan();
    string getTenduan();
};

// Nhap Du An
void Duan::nhap() {
    cout << "Nhap ma du an: ";
    cin >> maduan;

    cin.ignore();

    cout << "Nhap ten du an: ";
    getline(cin, tenduan);

    cout << "Nhap ten khach hang: ";
    getline(cin, tenkhachhang);

    cout << "Nhap ngay bat dau (dd/mm/yyyy): ";
    cin >> ngaybatdau;

    cout << "Nhap ngay ket thuc (dd/mm/yyyy): ";
    cin >> ngayketthuc;

    cout << "Nhap ngan sach: ";
    cin >> ngansach;

    cout << "Nhap ty le hoan thanh (%): ";
    cin >> tylehoanthanh;

    cin.ignore();
}

// Xuat Du An 
void Duan::xuat() {
    cout << "\n----------------------------------\n";
    cout << "Ma du an: " << maduan << endl;
    cout << "Ten du an: " << tenduan << endl;
    cout << "Ten khach hang: " << tenkhachhang << endl;
    cout << "Ngay bat dau: " << ngaybatdau << endl;
    cout << "Ngay ket thuc: " << ngayketthuc << endl;

    cout << "Ngan sach: "
         << fixed << setprecision(0)
         << ngansach << " VND" << endl;

    cout << "Ty le hoan thanh: "
         << tylehoanthanh << "%" << endl;

    cout << "----------------------------------\n";
}

// Ham lay du lieu
double Duan::getNgansach() {
    return ngansach;
}

string Duan::getMaduan() {
    return maduan;
}

string Duan::getTenduan() {
    return tenduan;
}

// Chuyen chu hoa thanh chu thuong 
string tolowerstring(string s) {
    for (int i = 0; i < (int)s.length(); i++) {
        s[i] = (char)tolower((unsigned char)s[i]);
    }

    return s;
}

// Nhap Danh sach 
void nhapDanhSach(Duan ds[], int &n) {
    int soLuong;

    cout << "Nhap so luong du an (1-199): ";

    while (!(cin >> soLuong) || soLuong < 1 || soLuong >= 200) {
        cout << "So luong khong hop le. Nhap lai (1-199): ";

        cin.clear();
        cin.ignore();
    }

    cin.ignore();

    n = soLuong;

    for (int i = 0; i < n; i++) {
        cout << "\n===== DU AN THU " << i + 1 << " =====\n";
        ds[i].nhap();
    }

    cout << "\nDa nhap danh sach thanh cong!\n";
}

// In danh sach
void indanhsach(Duan ds[], int n) {
    if (n == 0) {
        cout << "Danh sach rong!\n";
        return;
    }

    cout << "\n========== DANH SACH DU AN ==========\n";

    for (int i = 0; i < n; i++) {
        cout << "\nDu an thu " << i + 1 << ":";
        ds[i].xuat();
    }
}

// Sap xep ngan sach giam dan 
void sapxepngansachgiamdan(Duan ds[], int n) {
    if (n == 0) {
        cout << "Danh sach rong! Khong the sap xep.\n";
        return;
    }

    Duan temp;

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            if (ds[i].getNgansach() < ds[j].getNgansach()) {
                temp = ds[i];
                ds[i] = ds[j];
                ds[j] = temp;
            }
        }
    }

    cout << "\nDa sap xep theo ngan sach giam dan!\n";

    indanhsach(ds, n);
}

// Tim kiem theo ma
void timkiemtheoma(Duan ds[], int n) {
    if (n == 0) {
        cout << "Danh sach rong! Khong the tim kiem.\n";
        return;
    }

    string macantim;

    cout << "Nhap ma du an can tim: ";
    getline(cin, macantim);

    bool timthay = false;

    for (int i = 0; i < n; i++) {

        if (tolowerstring(ds[i].getMaduan()) ==
            tolowerstring(macantim)) {

            cout << "\nTim thay du an:\n";
            ds[i].xuat();

            timthay = true;
            break;
        }
    }

    if (!timthay) {
        cout << "Khong tim thay du an co ma: "
             << macantim << endl;
    }
}

// Tim kiem theo ten 
void timkiemtheoten(Duan ds[], int n) {
    if (n == 0) {
        cout << "Danh sach rong! Khong the tim kiem.\n";
        return;
    }

    string tencantim;

    cout << "Nhap ten du an can tim: ";
    getline(cin, tencantim);

    bool timthay = false;

    for (int i = 0; i < n; i++) {

        if (tolowerstring(ds[i].getTenduan()).find(
                tolowerstring(tencantim)) != string::npos) {

            if (!timthay) {
                cout << "\nCAC DU AN TIM THAY:\n";
                timthay = true;
            }

            ds[i].xuat();
        }
    }

    if (!timthay) {
        cout << "Khong tim thay du an co ten: "
             << tencantim << endl;
    }
}

// Them du an vao vi tri k (tinh tu 0-n) 
void bosungduan(Duan ds[], int &n) {

    if (n >= 200) {
        cout << "Danh sach da day, khong the bo sung!\n";
        return;
    }

    int k;

    cout << "Nhap vi tri can bo sung (tu 0 den " << n << "): ";
    cin >> k;

    if (k < 0 || k > n) {
        cout << "Vi tri khong hop le!\n";
        return;
    }

    // Dich cac phan tu sang phai
    for (int i = n; i > k; i--) {
        ds[i] = ds[i - 1];
    }

     cout << "Nhap thong tin du an moi:\n";
    ds[k].nhap();
    n++; // Tang so luong phan tu
    cout << "\nBo sung thanh cong!";
    indanhsach(ds, n);
}

// Xoa du an tai vi tri k ( vi tri tu 0-n) 
void xoaduan(Duan ds[], int &n) {

    if (n <= 0) {
        cout << "Danh sach rong, khong co gi de xoa!\n";
        return;
    }

    int k;
    cout << "Nhap vi tri can xoa (tu 0 den " << n - 1 << "): ";
    cin >> k;

    if (k < 0 || k >= n) {
        cout << "Vi tri khong hop le!\n";
        return;
    }

    // Dich cac phan tu phia sau sang trai
    for (int i = k; i < n - 1; i++) {
        ds[i] = ds[i + 1];
    }

    n--; // Giam so luong phan tu
    cout << "\nXoa thanh cong!";
    indanhsach(ds, n);
}

// Menu 
void menu() {

    cout << "\n========== QUAN LY DU AN PHAN MEM ==========\n";
    cout << "1. Nhap danh sach du an\n";
    cout << "2. In danh sach du an\n";
    cout << "3. Sap xep theo ngan sach giam dan\n";
    cout << "4. Tim kiem theo ma du an\n";
    cout << "5. Tim kiem theo ten du an\n";
    cout << "6. Bo sung du an tai vi tri cho truoc\n";
    cout << "7. Xoa du an tai vi tri cho truoc\n";
    cout << "0. Thoat chuong trinh\n";
    cout << "============================================\n";
    cout << "Nhap lua chon cua ban: ";
}

// Ham Main
int main() {

    // De toi da 199 du an theo yeu cau n < 200
    Duan ds[200];

    int n = 0;
    int chon;

    do {

        menu();

        if (!(cin >> chon)) {

            cout << "Lua chon khong hop le!\n";

            cin.clear();
            cin.ignore();

            continue;
        }

        cin.ignore();

        switch (chon) {

            case 1:
                nhapDanhSach(ds, n);
                break;

            case 2:
                indanhsach(ds, n);
                break;

            case 3:
                sapxepngansachgiamdan(ds, n);
                break;

            case 4:
                timkiemtheoma(ds, n);
                break;

            case 5:
                timkiemtheoten(ds, n);
                break;

            case 6:
                bosungduan(ds, n);
                break;

            case 7:
                xoaduan(ds, n);
                break;

            case 0:
                cout << "Da thoat chuong trinh!\n";
                break;

            default:
                cout << "Lua chon khong hop le! Vui long chon lai.\n";
        }

    } while (chon != 0);

    return 0;
}
