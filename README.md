#include <iostream>
using namespace std;
int main() {
  int jumlahBuah,hargaBarang, total, result;
  string diskon;

  cout << "Masukan jumlah barang \t: ";
  cin >> jumlahBuah;
  cout << "Masukan harga barang \t: Rp ";
  cin >> hargaBarang;

  total = jumlahBuah * hargaBarang;
  cout << "Total pembelian \t\t: Rp " << total << endl;

  if (total > 100000){
    diskon = "10%";
    result = total - (total * 0.1);
  } else if (total > 50000) {
    diskon = "5%";
    result = total - (total * 0.05);
  } else if (total <= 20000) {
    diskon = "2%";
    result = total - (total * 0.02);
  } else {
    result = total;
  }

  if ( diskon.length() > 0){
    cout << "Mendapatkan diskon \t\t: " << diskon << endl;
  }
  
  cout << "Total diskon \t\t\t: " << diskon << endl;
  cout << "Harga yang dibayar \t\t: Rp " << result;

} 
