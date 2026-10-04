# YÊU CẦU: bấm vào bút để xem code và chỉnh sửa lại code của mình để thống nhất và làm slide







#include <iostream>
#include <string>
#include <iomanip>
#include <cctype>
using namespace std;

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

void Duan::nhap() {
    cout << "Nhap ma du an: ";			cin >> maduan;	cin.ignore();
    cout << "Nhap ten du an: ";			getline(cin, tenduan);
	cout << "Nhap ten khach hang: ";	getline(cin, tenkhachhang);
	cout << "Nhap ngay bat dau: ";	cin >> ngaybatdau;
    cout << "Nhap ngay ket thuc: ";	cin >> ngayketthuc;
	cout << "Nhap ngan sach: ";		cin >> ngansach;
    cout << "Nhap ty le hoan thanh: ";  cin >> tylehoanthanh;
}

void Duan::xuat() {
    cout << "\nTHONG TIN DU AN\n";
    cout << "Ma du an: " << maduan << endl;
    cout << "Ten du an: " << tenduan << endl;
    cout << "Ten khach hang: " << tenkhachhang << endl;
    cout << "Ngay bat dau: " << ngaybatdau << endl;
    cout << "Ngay ket thuc: " << ngayketthuc << endl;
    cout << "Ngan sach: " << ngansach << endl;
    cout << "Ty le hoan thanh: " << tylehoanthanh << "%" << endl;
}

double Duan::getNgansach() {
    return ngansach;
}

string Duan::getMaduan() {
    return maduan;
}

string Duan::getTenduan() {
    return tenduan;
}
// ================= CHUYEN CHU HOA/THUONG =================

string tolowerstring(string s) {
    for (int i = 0; i < s.length(); i++) {
        s[i] = tolower(s[i]);
    }
    return s;
}

// ================= SAP XEP =================

void sapxepngansachgiamdan(Duan ds[], int n) {
    int i, j;
    Duan temp;
    if (n <= 0) {
        cout << "Danh sach rong! Khong the sap xep";
        return;
    }
    for (i=0; i< n-1; i++) {
        for (j=i+1; j<n; j++) {
            if (ds[i].getNgansach() < ds[j].getNgansach()) {
                temp = ds[i];
                ds[i] = ds[j];
                ds[j] = temp;
            }
        }
    }
    cout << "Danh sach da sap xep theo ngan sach giam dan:\n";
    for (int i = 0; i < n; i++) {
        ds[i].xuat();
    }
}

void timkiemtheoma(Duan ds[], int n) {
    int i;
    if (n <= 0) {
        cout << "Danh sach rong! Khong the tim kiem ma du an";
        return;
    }
    string macantim;
    cout << "Nhap ma du an can tim: ";	getline(cin >> ws, macantim);
    bool timthay = false;
    string malower = tolowerstring(macantim);
    for (i = 0; i < n; i++) {
        if (tolowerstring(ds[i].getMaduan()) == malower) {
            cout << "\nTHONG TIN DU AN TIM THAY THEO MA\n";
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

void timkiemtheoten(Duan ds[], int n) {

    int i;

    if (n<=0) {
        cout << "Danh sach rong! Khong the tim kiem ten du an";
        return;
    }
    string tencantim;
    cout << "Nhap ten du an can tim: ";	getline(cin >> ws, tencantim);
    bool timthay = false;
    string tenlower = tolowerstring(tencantim);
    for (i=0; i<n; i++) {
        if (tolowerstring(ds[i].getTenduan()).find(tenlower)!= string::npos) {
            if (!timthay) {
                cout << "\nTHONG TIN DU AN TIM THAY THEO TEN:\n";
                timthay = true;
            }
            ds[i].xuat();
        }
    }
    if (!timthay) {
        cout << "Khong tim thay du an co ten: "<< tencantim << endl;
    }
}

// Them du an vao vi tri k (tinh tu 0-n) 
void bosungduan(duan ds[], int &n) {
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
    
    // Dich cac phan tu dung sau sang phai
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
void xoaduan(duan ds[], int &n) {
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
    
    // Dich cac phan tu dung sau sang trai
    for (int i = k; i < n - 1; i++) {
        ds[i] = ds[i - 1 + 1];
    }
    
    n--; // Giam so luong phan tu
    cout << "\nXoa thanh cong!";
    indanhsach(ds, n);
}
int main() {
    Duan ds[100];
    int n;
    cout << "Nhap so luong du an: ";
    cin >> n;
    for (int i = 0; i < n; i++) {
        cout << "\n===== DU AN THU " << i + 1 << " =====\n";
        ds[i].nhap();
    }
    cout << "\n\n===== DANH SACH DU AN =====\n";
    for (int i = 0; i < n; i++) {
        ds[i].xuat();
    }
    cout << "\n\n===== SAP XEP =====\n";
    sapxepngansachgiamdan(ds, n);
    return 0;
}
