# Kardinalitas

![soal (2)](https://github.com/user-attachments/assets/81682793-fb63-41b1-a131-ba04363cddce)
peg)

***1. Class ```Customer```***
Fungsi:
Mewakili informasi tentang pelanggan yang membuat pesanan.

Atribut:

```name```: Nama pelanggan (tipe data ```String```).

```address```: Alamat pelanggan (tipe data ```String```).
***Penjelasan:***

Class ini memiliki dua atribut yang menyimpan informasi pelanggan.

Class ini biasanya digunakan untuk menghubungkan pesanan dengan siapa yang memesannya.
```
public class Customer {
    private String name;
    private String address;
    // Constructor, Getter, Setter
}
```
***2. Class ```Order```***
Fungsi:
Mewakili sebuah pesanan yang dibuat oleh pelanggan.

Atribut:

```date```: Tanggal pesanan dibuat (tipe data ```Date```).

```status```: Status pesanan, misalnya "Pending", "Completed" (tipe data ```String```).

```customer```: Objek ```Customer``` yang merepresentasikan siapa yang memesan.

```orderDetails```: Daftar item yang dipesan (```List<OrderDetail>```).

***Metode:***

```calcSubTotal()```: Menghitung subtotal dari semua item yang dipesan.

```calcTax()```: Menghitung total pajak berdasarkan item.

```calcTotal()```: Menghitung total biaya pesanan (subtotal + pajak).

```calcTotalWeight()```: Menghitung total berat semua item yang dipesan.

```
public class Order {
    private Date date;
    private String status;
    private Customer customer;
    private List<OrderDetail> orderDetails;

    public double calcSubTotal() { /* Menghitung subtotal */ }
}
```
***3. Class ```OrderDetail```***
Fungsi:
Mewakili detail dari setiap item yang dipesan dalam sebuah pesanan.

Atribut:

```quantity```: Jumlah item yang dipesan (tipe data ```int```).

```taxStatus```: Status pajak, apakah item dikenakan pajak atau tidak (tipe data ```String```).

```item```: Objek ```Item``` yang berisi informasi barang.

***Metode:***

```calcSubTotal()```: Menghitung subtotal dari item berdasarkan jumlah.

```calcWeight()```: Menghitung berat total dari item berdasarkan jumlah.

```calcTax()```: Menghitung total pajak untuk item.
```
public class OrderDetail {
    private int quantity;
    private String taxStatus;
    private Item item;

    public double calcSubTotal() { /* Menghitung subtotal dari item */ }
}
```
***4. Class ```Item```***
Fungsi:
Mewakili item atau barang yang dipesan dalam pesanan.

Atribut:

```shippingWeight```: Berat pengiriman barang (tipe data ```double```).

```description```: Deskripsi atau nama barang (tipe data ```String```).

***Metode:***

```getPriceForQuantity()```: Menghitung harga berdasarkan jumlah item.

```getTax()```: Mengembalikan nilai pajak dari item.

```inStock()```: Mengecek apakah barang tersedia dalam stok.
```
public class Item {
    private double shippingWeight;
    private String description;

    public double getPriceForQuantity(int quantity) { /* Menghitung harga */ }
}
```
***5. Abstract Class ```Payment```***

Fungsi:

Kelas abstrak yang mewakili pembayaran dalam pesanan. Kelas ini tidak dapat diinstansiasi dan digunakan sebagai dasar untuk metode pembayaran lain.

Atribut:

```amount```: Jumlah yang harus dibayarkan (tipe data ```float```).

***Metode:***

```authorized()```: Metode abstrak yang harus diimplementasikan oleh kelas turunannya untuk mengecek apakah pembayaran berhasil.
```
public abstract class Payment {
    protected float amount;

    public abstract boolean authorized();
}
```
***6. Class ```Cash``` (Turunan ```Payment```)***
Fungsi:
Mewakili pembayaran menggunakan uang tunai.

Atribut:

```cashTendered```: Jumlah uang tunai yang diberikan (tipe data ```float```).

***Metode:***

```authorized()```: Mengecek apakah uang tunai yang diberikan cukup untuk membayar pesanan.
```
public class Cash extends Payment {
    private float cashTendered;

    @Override
    public boolean authorized() { /* Mengecek apakah uang tunai cukup */ }
}
```
***7. Class ```Check``` (Turunan ```Payment```)***
Fungsi:
Mewakili pembayaran menggunakan cek.

Atribut:

```name```: Nama pemilik rekening (tipe data ```String```).

```bankID```: Identitas bank (tipe data ```String```).

***Metode:***

```authorized()```: Mengecek apakah cek dapat diterima (contoh validasi cek bisa ditambahkan).
```
public class Check extends Payment {
    private String name;
    private String bankID;

    @Override
    public boolean authorized() { /* Mengecek validasi cek */ }
}
```
***8. Class ```Credit``` (Turunan ```Payment```)***
Fungsi:
Mewakili pembayaran menggunakan kartu kredit.

Atribut:

```number```: Nomor kartu kredit (tipe data ```String```).

```type```: Jenis kartu kredit, misalnya Visa atau Mastercard (tipe data ```String```).

```expDate```: Tanggal kadaluarsa kartu kredit (tipe data ```String```).

***Metode:***

```authorized()```: Mengecek apakah pembayaran menggunakan kartu kredit disetujui.
```
public class Credit extends Payment {
    private String number;
    private String type;
    private String expDate;

    @Override
    public boolean authorized() { /* Mengecek validasi kartu kredit */ }
}
```
***Hubungan Antar Kelas:***
**Customer-Order:**
Satu pelanggan (```Customer```) dapat memiliki banyak pesanan (```Order```), tetapi satu pesanan hanya terkait dengan satu pelanggan.

**Order-OrderDetail:**
Satu pesanan (```Order```) dapat memiliki beberapa item detail (```OrderDetail```), yang merepresentasikan item yang dipesan.

**OrderDetail-Item:**
Satu detail pesanan (```OrderDetail```) terkait dengan satu barang (```Item```).

**Order-Payment:**
Satu pesanan (```Order```) bisa memiliki satu atau lebih pembayaran (```Payment```), dan pembayaran bisa menggunakan metode yang berbeda (tunai, cek, atau kartu kredit).
