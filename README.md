#include <iostream>
#include <string>
#include <iomanip>
using namespace std;

class Duan {
private:
    string maduan;
    string tenduan;
    string tenkhachhang;
    string ngaybatdau;
    string ngayketthucdukien;
    double ngansach;
    double tylehoanthanh;

public:
    void nhap();
	void xuat(); 
};


int main() {
    Duan da;

    da.nhap();

    da.xuat();

    return 0;
}

void Duan::nhap() {
    cout<<"Nhap ma du an: ";	cin>>maduan;	cin.ignore();
    cout<<"Nhap ten du an: ";	getline(cin,tenduan);
    cout<<"Nhap ten khach hang : ";		getline(cin, tenkhachhang);
    cout<<"Nhap ngay bat dau : ";	cin>>ngaybatdau;
    cout<<"Nhap ngay ket thuc : ";	cin>>ngayketthucdukien;
    cout<<"Nhap ngan sach : ";		cin>>ngansach;
    cout<<"Nhap ty le hoan thanh : ";	cin>>tylehoanthanh;
}
void Duan::xuat() {
	cout << "\nTHONG TIN DU AN\n";
    cout<<"Ma du an : "<<maduan <<endl;
    cout<< "Ten du an : "<<tenduan <<endl;
    cout<<"Ten khach hang : "<<tenkhachhang <<endl;
    cout<<"Ngay bat dau : "<<ngaybatdau <<endl;
    cout<< "Ngay ket thuc : " << ngayketthucdukien <<endl;
    cout<<"Ngan sach : "<<ngansach <<".000"<<endl;
    cout<<"Ty le hoan thanh : "<<tylehoanthanh<<"%"<<endl;
}
