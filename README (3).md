[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/aRvIU2lf)
| Name           | NRP        | Kelas     |
| ---            | ---        | ----------|
| Jorell Ramos Sinaga | 5025241202 | A |



## Put your topology config image here!

![](https://drive.google.com/uc?export=view&id=1XnCLw6EPNNr1_OCWszM0znz4XCqgYQft)

## Put your GNS3 Project file here!

[File Project Final Praktikum](https://github.com/Jorell-Ramos-Sinaga/test-final-praktikum/blob/X-Komp-1/Final%20Praktikum.gns3project)

<br>

## Soal 1

> Menggunakan metode VLSM, buatlah pembagian subnet untuk masing-masing gedung dengan cara yang seefisien mungkin!

> _Using the VLSM method, create subnets for each building as efficiently as possible!_

**Answer:**

- Screenshot

  Hasil Subnetting Akhir :
  
  ![](https://drive.google.com/uc?export=view&id=1l5Tv1TwlO9pb2E5qoYzt18_-fy-AOqQu)
  
- Explanation

  Membagi subnet sesuai topologi yang disediakan :

  ![](https://drive.google.com/uc?export=view&id=1Y0RkY1KZkPLWGuM7RpamV6mfWYcjaiGd)

  Menghitung jumlah host yang diperlukan oleh semua subnet

  `A1 + A2 + A3 + A4 + A5 + A6 + A7 + A8 + A9`
  <br>`= (50+1+1)  + (100 + 1) + (10 + 1 + 1) + (200 + 1)  + (1 + 250 + 1 + 1000) + (1 + 5000) + 3 + (2 + 1) + 2`
  <br>`= 8253`

  Jadi, pembagian IP dilakukan mulai dari netmask /18 (16382 usable IPs). Kemudian, lakukan pembagian IP dengan metode VLSM :

  ![](https://drive.google.com/uc?export=view&id=1WYIiYlz440oDjgyYxEwa1YEqSQsT-VQr)

  Konfigurasi IP, Netmask, dan Gateway statis (untuk sementara bagi node yang seharusnya lewat DHCP) di setiap node sesuai tabel pembagian IP. Node non-router :

  | Node | Subnet | IP Address | Netmask | Gateway | Keterangan Gateway |
  | :--- | :--- | :--- | :--- | :--- | :--- |
  | **RuyLopez** | A1 | 10.64.41.129 | 255.255.255.192 | 10.64.41.190 | via Lucena (eth0) |
  | **Ponziani** | A1 | 10.64.41.130 | 255.255.255.192 | 10.64.41.190 | via Lucena (eth0) |
  | **Sicilian** | A2 | 10.64.41.1 | 255.255.255.128 | 10.64.41.126 | via Zugzwang (eth1) |
  | **Caro-Kann** | A3 | 10.64.41.193 | 255.255.255.240 | 10.64.41.206 | via Zugzwang (eth2) |
  | **Alekhine** | A3 | 10.64.41.194 | 255.255.255.240 | 10.64.41.206 | via Zugzwang (eth2) |
  | **Slav** | A4 | 10.64.40.1 | 255.255.255.0 | 10.64.40.254 | via Zugzwang (eth3) |
  | **Stafford** | A5 | 10.64.32.1 | 255.255.248.0 | 10.64.39.254 | via Smith-Morra (eth2) |
  | **Budapest** | A5 | 10.64.32.2 | 255.255.248.0 | 10.64.39.254 | via Smith-Morra (eth2) |
  | **Blackmar-Diemer**| A6 | 10.64.0.1 | 255.255.224.0 | 10.64.31.254 | via Smith-Morra (eth3) |
  | **Petrov** | A8 | 10.64.41.217 | 255.255.255.248 | 10.64.41.218 | via Zwischenzug (eth1) |

  Lucena :

  | Interface | IP Address | Netmask | Keterangan Subnet |
  | :--- | :--- | :--- | :--- |
  | **eth0** | 10.64.41.190 | 255.255.255.192 | Kompleks A1 |
  | **eth1** | 10.64.41.209 | 255.255.255.248 | Kompleks A7 |

  Zugzwang :

  | Interface | IP Address | Netmask | Keterangan Subnet |
  | :--- | :--- | :--- | :--- |
  | **eth0** | 10.64.41.219 | 255.255.255.248 | Kompleks A8 |
  | **eth1** | 10.64.41.126 | 255.255.255.128 | Kompleks A2 |
  | **eth2** | 10.64.41.206 | 255.255.255.240 | Kompleks A3 |
  | **eth3** | 10.64.40.254 | 255.255.255.0 | Kompleks A4 |
  
  Smith-Morra :

  | Interface | IP Address | Netmask | Keterangan Subnet |
  | :--- | :--- | :--- | :--- |
  | **eth0** | DHCP / Public IP | - | **NAT** (Internet) |
  | **eth1** | 10.64.41.226 | 255.255.255.252 | Kompleks A9 |
  | **eth2** | 10.64.39.254 | 255.255.248.0 | Kompleks A5 |
  | **eth3** | 10.64.31.254 | 255.255.224.0 | Kompleks A6 |
  
  Zwischenzug :
  | Interface | IP Address | Netmask | Keterangan Subnet |
  | :--- | :--- | :--- | :--- |
  | **eth0** | 10.64.41.210 | 255.255.255.248 | Kompleks A7 |
  | **eth1** | 10.64.41.218 | 255.255.255.248 | Kompleks A8 |

  Fianchetto :
  | Interface | IP Address | Netmask | Keterangan Subnet |
  | :--- | :--- | :--- | :--- |
  | **eth0** | 10.64.41.211 | 255.255.255.248 | Kompleks A7 |
  | **eth1** | 10.64.41.225 | 255.255.255.252 | Kompleks A9 |

<br>

## Soal 2

> Konfigurasi semua router agar bisa terhubung ke semua jaringan. Gunakan static routing dan uji dengan melakukan ping dari **Budapest** ke **Alekhine** dan dari **Ponziani** ke **Sicilian**!

> _Configure all routers to connect to all networks. Use static routing and perform testing by pinging from **Budapest** to **Alekhine** and from **Ponziani** to **Sicilian**!_

**Answer:**

- Screenshot

  Hasil **Static Routing** dan koneksi antar node :
  
  ![](https://drive.google.com/uc?export=view&id=1O_CXOpzjbVk2d6MFdyTPFDdCVMAGh3S-)
  
- Explanation

  Aktifkan **IP Forwarding** di setiap router dengan perintah :

  ```
  up echo 1 > /proc/sys/net/ipv4/ip_forward
  ```

  Lakukan **Static Routing** di setiap router menuju setiap subnet yang tidak langsung terhubung.
  <br> Router Lucena :
  ```
  ip route add 10.64.32.0/21 via 10.64.41.211 # Menuju A5
  ip route add 10.64.0.0/19 via 10.64.41.211 # Menuju A6
  ip route add 10.64.41.224/30 via 10.64.41.211 # Menuju A9
  ip route add 10.64.41.216/29 via 10.64.41.210  # Menuju A8
  ip route add 10.64.41.0/25   via 10.64.41.210  # Menuju A2
  ip route add 10.64.41.192/28 via 10.64.41.210  # Menuju A3
  ip route add 10.64.40.0/24   via 10.64.41.210  # Menuju A4
  ```

  Router Zugzwang :

  ```
  ip route add 10.64.41.128/26   via 10.64.41.218  # Menuju A1
  ip route add 10.64.32.0/21 via 10.64.41.218 # Menuju A5
  ip route add 10.64.0.0/19 via 10.64.41.218 # Menuju A6
  ip route add 10.64.41.208/29 via 10.64.41.218  # Menuju A7
  ip route add 10.64.41.224/30 via 10.64.41.218  # Menuju A9
  ```

  Router Smith-Morra :
  ```
  ip route add 10.64.41.208/29 via 10.64.41.225  # Menuju A7
  ip route add 10.64.41.128/26 via 10.64.41.225  # Menuju A1
  ip route add 10.64.41.216/29 via 10.64.41.225  # Menuju A8
  ip route add 10.64.41.0/25   via 10.64.41.225  # Menuju A2
  ip route add 10.64.41.192/28 via 10.64.41.225  # Menuju A3
  ip route add 10.64.40.0/24   via 10.64.41.225  # Menuju A4
  ```

  Router Zwischenzug :
  ```
  ip route add 10.64.41.128/26   via 10.64.41.209  # Menuju A1
  ip route add 10.64.32.0/21 via 10.64.41.211 # Menuju A5
  ip route add 10.64.0.0/19 via 10.64.41.211 # Menuju A6
  ip route add 10.64.41.224/30 via 10.64.41.211 # Menuju A9
  ip route add 10.64.41.0/25   via 10.64.41.219  # Menuju A2
  ip route add 10.64.41.192/28 via 10.64.41.219  # Menuju A3
  ip route add 10.64.40.0/24   via 10.64.41.219  # Menuju A4
  ```

  Router Fianchetto :
  ```
  ip route add 10.64.41.128/26 via 10.64.41.209  # Menuju A1
  ip route add 10.64.32.0/21 via 10.64.41.226 # Menuju A5
  ip route add 10.64.0.0/19 via 10.64.41.226 # Menuju A6
  ip route add 10.64.41.216/29 via 10.64.41.210  # Menuju A8
  ip route add 10.64.41.0/25   via 10.64.41.210  # Menuju A2
  ip route add 10.64.41.192/28 via 10.64.41.210  # Menuju A3
  ip route add 10.64.40.0/24   via 10.64.41.210  # Menuju A4
  ```
<br>

## Soal 3

> Berikan seluruh client (**Blackmar-Diemer, Budapest,** dan **Stafford**) IP secara dinamis dari DHCP. Range IP dibebaskan, namun tunjukkan bahwa mereka mendapatkan IP secara dinamis!

> _Assign all clients (**Blackmar-Diemer, Budapest,** and **Stafford**) dynamic IP addresses via DHCP. You may use any IP range you would like, but prove that they receive IP addresses dynamically!_

**Answer:**

- Screenshot

  Hanya untuk pembuktian soal ini, bukti pembagian IP sesuai dengan range di file `/etc/dhcp/dhcpd.conf` :
  
  ![](https://drive.google.com/uc?export=view&id=1qUoBzw_Z4Pfdm963nhHhmFSmKFH4WjC-)

- Explanation

  1. Melakukan setup **DHCP Server** di node `Ponziani`.
     
     Install dhcp server :
     ```
     apt-get update
     apt-get install -y isc-dhcp-server
     ```

     Edit file `/etc/default/isc-dhcp-server` untuk menentukan interface yang menuju ke switch adalah `eth0` :

     ```
     INTERFACESv4="eth0"
     ```
     
     Konfigurasi file konfigurasi `isc-dhcp-server` pada `/etc/dhcp/dhcpd.conf` untuk mengirim IP dinamis ke subnet client (A5 dan A6) :

     ```
      option domain-name "jarkom.local";
      # Persiapan soal DNS
      option domain-name-servers 10.64.41.193, 10.64.41.194, 192.168.122.1, 8.8.8.8;
      default-lease-time 600;
      max-lease-time 7200;
      authoritative;
      
      # === Subnet Lokal ===
      subnet 10.64.41.128 netmask 255.255.255.192 {
      }
      
      # === Subnet A5 ===
      subnet 10.64.32.0 netmask 255.255.248.0 {
          range 10.64.32.1 10.64.39.253;
          option routers 10.64.39.254;
          option subnet-mask 255.255.248.0;
          option broadcast-address 10.64.39.255;
      }
      
      # Subnet A6
      subnet 10.64.0.0 netmask 255.255.224.0 {
          range 10.64.0.1 10.64.31.253;
          option routers 10.64.31.254;
          option subnet-mask 255.255.224.0;
          option broadcast-address 10.64.31.255;
      }
     ```

     Restart service dhcp server :

     ```
     service isc-dhcp-server restart
     ```

  2. Setup **DHCP Relay** di router `Smith-Morra` :

     Install dhcp relay :

     ```
     apt update
     apt install -y isc-dhcp-relay
     ```

     Lakukan konfigurasi pada `/etc/default/isc-dhcp-relay` untuk menentukan IP dhcp server dan interface dari dhcp relay :

     ```
     SERVERS="10.64.41.130"
     INTERFACES="eth1 eth2 eth3"
     OPTIONS=""
     ```

     Restart service dhcp relay :

     ```
     service isc-dhcp-relay restart
     ```

  3. Pada node client, hapus konfigurasi IP statis lama dan tambah konfigurasi dhcp :

     ```
     auto eth0
     iface eth0 inet dhcp
     ```

<br>

## Soal 4

> Berikan web server **Slav** dan **Sicilian** IP address yang tetap/fixed dari DHCP. 

> _Assign **Slav** and **Sicilian** web servers fixed IP addresses via DHCP._

**Answer:**

- Screenshot

  Hanya untuk pembuktian soal ini, bukti pembagian _fixed address_ dengan range di file `/etc/dhcp/dhcpd.conf` :
  
  ![](https://drive.google.com/uc?export=view&id=1ao6TPFRi7SGmGjAdUsPQo3GLTps_ZMwI) 

- Explanation

  1. Tambahkan konfigurasi di node `Ponziani`

     Lakukan konfigurasi untuk subnet A2 (`Sicilian`) dan A4 (`Slav`) pada `/etc/dhcp/dhcpd.conf`.

     ```
      # === SUBNET A2 ===
      subnet 10.64.41.0 netmask 255.255.255.128 {
          option routers 10.64.41.126;
          option subnet-mask 255.255.255.128;
          option broadcast-address 10.64.41.127;
      }
      
      # === SUBNET A4 ===
      subnet 10.64.40.0 netmask 255.255.255.0 {
          option routers 10.64.40.254;
          option subnet-mask 255.255.255.0;
          option broadcast-address 10.64.40.255;
      }
     ```

     Tambahkan juga konfigurasi untuk _fixed address_ pada `/etc/dhcp/dhcpd.conf` dengan men-spesifikasi nama node dan **hwaddress**. **hwaddress** didapatkan dengan melaksanakan perintah `ip a` di node yang diinginkan di bagian `link/ether`.

     ```
      # --- Sicilian ---
      host Sicilian {
          hardware ethernet 02:42:f0:ce:bf:00;
          fixed-address 10.64.41.1;
      }
      
      # --- Slav ---
      host Slav {
          hardware ethernet 02:42:f4:e5:89:00;
          fixed-address 10.64.40.1;
      }
     ```

     Restart service dhcp server :

     ```
     service isc-dhcp-server restart
     ```
 
  2. Setup **DHCP Relay** di node `Zugzwang`
 
     Install dhcp relay :

     ```
     apt update
     apt install -y isc-dhcp-relay
     ```

     Lakukan konfigurasi pada `/etc/default/isc-dhcp-relay` untuk menentukan IP dhcp server dan interface dari dhcp relay :

     ```
     SERVERS="10.64.41.130"
     INTERFACES="eth0 eth1 eth2 eth3"
     OPTIONS=""
     ```

     Restart service dhcp relay :

     ```
     service isc-dhcp-relay restart
     ```

  3. Pada node client, hapus konfigurasi IP statis lama dan tambah konfigurasi dhcp. Kemudian, tambahkan setting hwaddress agar tidak berubah saat project di-restart
 
     `Sicilian` :

     ```
     auto eth0
     iface eth0 inet dhcp
     hwaddress ether 02:42:f0:ce:bf:00
     ```

     `Slav` :

     ```
     auto eth0
     iface eth0 inet dhcp
     hwaddress ether 02:42:f4:e5:89:00
     ```


<br>

## Soal 5

> Buatlah konfigurasi untuk domain:  
**parkov.com** → IP Node **Slav**  
**paskarov.com** → IP Node **Sicilian** 
Pada **DNS Master Caro-Kann.** Tambahkan juga subdomain www untuk kedua domain tersebut.

> _Configure the domains:  
**parkov.com** → **Slav** Node IP  
**paskarov.com** → **Sicilian** Node IP  
On the **Caro-Kann DNS Master,** then add the www subdomain for both domains._

**Answer:**

- Screenshot

  Tes ping ke domain `pakarov.com` dan `paskarov.com` setelah DNS Server menyala :
  
  ![](https://drive.google.com/uc?export=view&id=1ENQjpxeQ1TFZcn41cmmRGz8ByTi8ipH3)

- Explanation

  Install service bind9 di `Caro-Kann` :

  ```
  apt-get update
  apt-get install bind9 -y
  ```

  Di `Caro-Kann`, konfigurasi zona domain pada `/etc/bind/named.conf.local` :

  ```
  zone "parkov.com" {
      type master;
      file "/etc/bind/jarkom/parkov.com";
  };
  
  zone "paskarov.com" {
      type master;
      file "/etc/bind/jarkom/paskarov.com";
  };
  ```

  Tambahkan database untuk masing-masing domain. <br> `/etc/bind/jarkom/parkov.com` :

  ```
  ; Config parkov.com
  $TTL    604800
  @       IN      SOA     parkov.com. root.parkov.com. (
                       2023101001         ; Serial
                           604800         ; Refresh
                            86400         ; Retry
                          2419200         ; Expire
                           604800 )       ; Negative Cache TTL
  ;
  @       IN      NS      parkov.com.
  @       IN      A       10.64.40.1
  www     IN      CNAME   parkov.com.
  ```
     
  `/etc/bind/jarkom/paskarov.com` :

  ```
  ; Config paskarov.com
  $TTL    604800
  @       IN      SOA     paskarov.com. root.paskarov.com. (
                       2023101001         ; Serial
                           604800         ; Refresh
                            86400         ; Retry
                          2419200         ; Expire
                           604800 )       ; Negative Cache TTL
  ;
  @       IN      NS      paskarov.com.
  @       IN      A       10.64.41.1
  www     IN      CNAME   paskarov.com.
  ```

  Restart service bind9 :

  ```
  service bind9 restart

  // ATAU

  named -g
  ```

  Di node-node client, tambahkan nameserver di `/etc/resolv.conf` yang menuju ke IP DNS Server :

  ```
  nameserver 10.64.41.193
  ```

<br>

## Soal 6

> Konfigurasikan juga **Alekhine** sebagai **DNS Slave** yang bekerja untuk membantu **Caro-Kann.** Lakukan pengujian dengan **mematikan Caro-Kann** lalu coba ping ke domain dan subdomain tersebut (pilih salah satu saja).

> _Configure **Alekhine** as a **DNS Slave** to assist **Caro-Kann**. Perform testing by **disabling Caro-Kann** and then pinging the domain and subdomain (choose only one)._

**Answer:**

- Screenshot

  Tes ping ke domain masih bisa walaupun hanya DNS Slave menyala :
  
  ![](https://drive.google.com/uc?export=view&id=1w6YE_WDwUs1axp7KzPpD8gy1ecJLdiBO)

- Explanation

  1. Edit konfigurasi zona domain di `Caro-Kann`.

     Tambahkan setting `allow-notify` dan `allow-transfer` :

     ```
      zone "parkov.com" {
          type master;
          file "/etc/bind/jarkom/parkov.com";
      };
      
      zone "paskarov.com" {
          type master;
          file "/etc/bind/jarkom/paskarov.com";
      };
      ```

      Restart service bind9 :

      ```
      service bind9 restart
    
      // ATAU
    
      named -g
      ```

   2. Setup DNS Slave di `Alekhine`

      Install service bind9 di `Caro-Kann` :

      ```
      apt-get update
      apt-get install bind9 -y
      ```

      Tambahkan zona domain tipe slave di `/etc/bind/named.conf.local` :

      ```
      zone "parkov.com" {
          type slave;
          masters { 10.64.41.193; };
          file "/var/lib/bind/parkov.com";
      };
      
      zone "paskarov.com" {
          type slave;
          masters { 10.64.41.193; };
          file "/var/lib/bind/paskarov.com";
      };
      ```

      Restart service bind9 :

      ```
      service bind9 restart
    
      // ATAU
    
      named -g
      ```

      Di node-node client, tambahkan nameserver DNS Slave di `/etc/resolv.conf` setelah nameserver ke DNS Server :

      ```
      nameserver 10.64.41.193
      nameserver 10.64.41.194
      ```

<br>

## Soal 7

> Konfigurasikan **Sicilian** agar berfungsi sebagai **web server nginx** yang akan menyajikan [halaman berikut](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Konfigurasikan juga agar **Sicilian** bisa menyimpan custom access log ke file **/tmp/access.log** dan error log ke file **/tmp/error.log.**

> _Configure **Sicilian** to function as an **nginx web server**that will serve [this page](https://drive.google.com/file/d/1eX0ZjRKprx8T34XFAssrpc7ZE1j6Jv0j/view). Also, configure **Sicilian** to save custom access logs to **/tmp/access.log** and error logs to **/tmp/error.log.**_

**Answer:**

- Screenshot

  Tes curl ke domain yang menuju ke web server Sicilian :
  
  ![](https://drive.google.com/uc?export=view&id=1ACKPxHJci1YTHWKBjVdPpaFktqbaVPXk)
  
- Explanation

  Install nginx :

  ```
  apt-get update
  apt-get install -y nginx
  ```

  Buatkan folder tempat untuk menyimpan file-file konfig web server :

  ```
  mkdir -p /myscripts/myweb
  mkdir -p /myscripts/myconfig
  mkdir -p /myscripts/tmp
  ```

  Buat file konfigurasi nginx di `/myscripts/myconfig/nginx.conf` dan spesifikasi tempat `access.log` dan `error.log` :

  ```
  user www-data;
  worker_processes auto;
  pid /myscripts/tmp/nginx.pid;
  events { worker_connections 768; }
  
  http {
  
      # LOG FILES
      access_log /myscripts/tmp/access.log jarkom_format;
      error_log /myscripts/tmp/error.log;
  
      server {
          listen 80;
          server_name paskarov.com;
          root /myscripts/myweb;
          index sicilian.html;
          location / {
              try_files $uri $uri/ =404;
          }
      }
  }
  ```

  Masukkan file `sicilian.html` yang diberikan soal di `/myscripts/myweb/sicilian.html` :

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Sicilian Defense Guide (Offline)</title>
      <style>
        /* General Reset and Base Styles */
        body {
          font-family: Arial, Helvetica, sans-serif;
          margin: 0;
          padding: 40px 20px;
          background-color: #f3f4f6; /* Light gray background */
          min-height: 100vh;
          display: flex;
          flex-direction: column;
          align-items: center;
        }
        .container {
          max-width: 900px;
          width: 100%;
        }
  
        /* Color Variables (Simplified Palette) */
        :root {
          --primary-blue: #1e40af;
          --primary-dark: #0f172a;
          --card-bg: #ffffff;
          --text-color: #374151;
          --heading-color: #111827;
        }
  
        /* Header Styling */
        header {
          text-align: center;
          margin-bottom: 40px;
        }
        header h1 {
          font-size: 32px;
          font-weight: 800;
          color: var(--primary-dark);
          letter-spacing: -1px;
          margin-bottom: 8px;
        }
        header p {
          font-size: 18px;
          color: #6b7280;
        }
  
        /* Card Styling */
        .card {
          background-color: var(--card-bg);
          padding: 30px;
          border-radius: 12px;
          box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
            0 4px 6px -2px rgba(0, 0, 0, 0.05);
          border-top: 4px solid var(--primary-blue);
        }
  
        .card-header {
          display: flex;
          align-items: center;
          margin-bottom: 16px;
        }
        .card-header span {
          font-size: 28px;
          margin-right: 12px;
        }
        .card-header h2 {
          font-size: 24px;
          font-weight: 700;
          color: var(--primary-blue);
        }
        .card h3 {
          font-size: 20px;
          font-weight: 600;
          color: var(--heading-color);
          margin-bottom: 20px;
        }
  
        /* Content Styles */
        .content p {
          color: var(--text-color);
          line-height: 1.6;
          margin-bottom: 20px;
        }
  
        /* Code Block/Key Lines */
        .key-sequence {
          background-color: #e5e7eb;
          padding: 15px;
          border-radius: 8px;
          margin-bottom: 20px;
        }
        .key-sequence h4 {
          font-size: 16px;
          font-weight: 700;
          margin-bottom: 8px;
          color: var(--primary-dark);
        }
        .key-sequence code {
          display: block;
          background-color: #d1d5db;
          font-family: monospace;
          padding: 10px;
          border-radius: 4px;
          font-size: 14px;
          color: var(--primary-dark);
          white-space: pre-wrap; /* Ensure wrapping on smaller screens */
        }
  
        /* List Styles */
        .variations-list {
          list-style: disc;
          margin-left: 20px;
          padding-left: 0;
          color: var(--text-color);
          line-height: 1.5;
        }
        .variations-list li {
          margin-bottom: 8px;
        }
        .variations-list strong {
          font-weight: 600;
        }
  
        /* Footer */
        footer {
          margin-top: 40px;
          padding-top: 20px;
          text-align: center;
          color: #6b7280;
          font-size: 14px;
          border-top: 1px solid #e5e7eb;
        }
  
        /* Responsive adjustments */
        @media (min-width: 768px) {
          header h1 {
            font-size: 44px;
          }
          .card {
            padding: 40px;
          }
        }
      </style>
    </head>
    <body>
      <div class="container">
        <header>
          <h1>The Sicilian Defense</h1>
          <p>
            Black's most popular, aggressive, and counter-attacking response to 1.
            e4.
          </p>
        </header>
  
        <main>
          <!-- SICILIAN DEFENSE CARD -->
          <div class="card">
            <div class="card-header">
              <span role="img" aria-label="Knight icon">♞</span>
              <h2>Key Strategies</h2>
            </div>
            <h3 class="opening-move">Start: 1. e4 c5</h3>
  
            <div class="content">
              <p>
                The Sicilian is a commitment to imbalance. Black immediately
                fights for the d4 square without directly occupying the center,
                inviting White to expand. This often leads to sharp battles,
                especially in the Open Sicilian variations where White plays d4.
                Black aims to undermine White's central control and use the
                half-open c-file. Favored by champions like Kasparov and Fischer,
                this opening requires high skill to play but can be deadly in the
                right hands.
              </p>
  
              <!-- Key Lines -->
              <div class="key-sequence">
                <h4>Key Move Sequence (Open Sicilian)</h4>
                <code title="1. e4 c5 2. Nf3 Nc6 3. d4 cxd4 4. Nxd4">
                  1. e4 c5 2. Nf3 Nc6 3. d4 cxd4 4. Nxd4
                </code>
              </div>
  
              <!-- Sub-Variations -->
              <div class="variations">
                <h3>Major Sub-Variations:</h3>
                <ul class="variations-list">
                  <li>
                    <strong class="font-medium">Najdorf:</strong> 4... a6.
                    Extremely flexible and deep. Black often prepares to challenge
                    the center with ...e5 or initiate queenside play with ...b5.
                  </li>
                  <li>
                    <strong class="font-medium">Dragon:</strong> 6... g6. Black
                    fianchettoes the dark-squared bishop, leading to sharp,
                    opposite-side castling positions, often involving an attack
                    down the h-file.
                  </li>
                  <li>
                    <strong class="font-medium">Scheveningen:</strong> Black
                    places pawns on e6 and d6, forming a solid central fortress,
                    but risking a Keres Attack if White is aggressive.
                  </li>
                  <li>
                    <strong class="font-medium">Taimanov/Kan:</strong> Solid and
                    positional setups, often involving ...e6 and ...a6,
                    prioritizing development and flexible pawn structures over
                    immediate conflict.
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </main>
  
        <footer>
          <p>
            This document is made for Computer Networks 2025.<br />
            -adieos
          </p>
        </footer>
      </div>
    </body>
  </html>
  ```

  Start service nginx :

  ```
  nginx -c /myscripts/myconfig/nginx.conf
  ```

<br>

## Soal 8

> Buatlah custom access log ke file **/tmp/access.log.** Untuk keperluan logging, gunakan format log seperti di bawah:
> - Tanggal dan waktu akses dalam format standar log.
> - Nama node yang sedang diakses.
> - Alamat IP klien yang mengakses website.
> - Metode HTTP dan URI yang diakses oleh klien.
> - Status respons HTTP yang diberikan oleh server.
> - Jumlah byte yang dikirimkan dalam respons.
> - Waktu yang dihabiskan oleh server untuk menangani permintaan.> 
> - Contoh format log yang sesuai:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds

> _Webserver: Create a custom access log to the file **/tmp/access.log.** For logging purposes, use the log format shown below:_
> - _The date and time of access in standard log format._
> - _The name of the node being accessed._
> - _The IP address of the client accessing the website._
> - _The HTTP method and URI accessed by the client._
> - _The HTTP response status returned by the server._
> - _The number of bytes sent in the response._
> - _The time spent by the server processing the request._
> - _Example of appropriate log format:  
[01/Oct/2024:11:30:45 +0000] Jarkom Node Sicilian Access from 192.168.1.15 using method "GET /resep/bayam HTTP/1.1" returned status 200 with 2567 bytes sent in 0.038 seconds_

**Answer:**

- Screenshot

  Isi `access.log` setelah beberapa pengujian dari node lain :
  
  ![](https://drive.google.com/uc?export=view&id=15V_wduu6TBH2F8V90Rbq2bhsbMtZ57Wt)

- Explanation

  Sesuaikan format `access.log` seperti soal di `/myscripts/myconfig/nginx.conf` :

  ```
  // ...
  # LOG FORMAT
      log_format jarkom_format "[$time_local] Jarkom Node Sicilian Access from $remote_addr using method \"$request\" returned status $status with $body_bytes_sent bytes sent in $request_time seconds";
  
      # LOG FILES
      access_log /myscripts/tmp/access.log jarkom_format;
      error_log /myscripts/tmp/error.log;
  // ...
  ```

  Start service nginx :

  ```
  nginx -c /myscripts/myconfig/nginx.conf
  ```

<br>

## Soal 9

> Konfigurasikan juga **Slav** agar berfungsi sebagai **web server nginx** yang menyajikan [halaman berikut](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view) dan **hanya** bisa diakses melalui port **8000** dan **8888.**

> _Configure **Slav** to function as an **nginx web server** that serves [this page](https://drive.google.com/file/d/1h8ik1Zcubntp0dvHt9NHYqSZLSTG6FuZ/view?usp=drive_link) and is **only** accessible via ports **8000** and **8888.**_

**Answer:**

- Screenshot

  Tes curl biasa dan curl dengan port 8000 ke domain yang menuju ke Slav :
  
  ![](https://drive.google.com/uc?export=view&id=1fYea3YPeX_YAs-9guyzl_UKx8f-3qumP)

- Explanation

  Install nginx :

  ```
  apt-get update
  apt-get install -y nginx
  ```

  Buatkan folder tempat untuk menyimpan file-file konfig web server :

  ```
  mkdir -p /myscripts/myweb
  mkdir -p /myscripts/myconfig
  mkdir -p /myscripts/tmp
  ```

  Buat file konfigurasi nginx di `/myscripts/myconfig/nginx.conf` dan spesifikasi akses port dengan `listen 8000` dan `listen 8888` :

  ```
  user www-data;
  worker_processes auto;
  pid /myscripts/tmp/nginx.pid;
  events { worker_connections 768; }
  
  http {
  
      # LOG FORMAT
      log_format jarkom_format "[$time_local] Jarkom Node Slav Access from $remote_addr using method \"$request\" returned status $status with $body_bytes_sent bytes sent in $request_time seconds";
  
      # LOG FILES
      access_log /myscripts/tmp/access.log jarkom_format;
      error_log /myscripts/tmp/error.log;
  
      # SERVER BLOCK
      server {
          # HANYA LISTEN DI PORT 8000 DAN 8888
          listen 8000;
          listen 8888;
  
          server_name parkov.com;
          root /myscripts/myweb;
          index slav.html;
  
          location / {
              try_files $uri $uri/ =404;
          }
      }
  }
  ```

  Masukkan file `slav.html` yang diberikan soal :

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Slav Defense Guide (Offline)</title>
      <style>
        /* General Reset and Base Styles */
        body {
          font-family: Arial, Helvetica, sans-serif;
          margin: 0;
          padding: 40px 20px;
          background-color: #f3f4f6; /* Light gray background */
          min-height: 100vh;
          display: flex;
          flex-direction: column;
          align-items: center;
        }
        .container {
          max-width: 900px;
          width: 100%;
        }
  
        /* Color Variables (Simplified Palette) */
        :root {
          --primary-gray: #374151;
          --primary-dark: #0f172a;
          --card-bg: #ffffff;
          --text-color: #374151;
          --heading-color: #111827;
        }
  
        /* Header Styling */
        header {
          text-align: center;
          margin-bottom: 40px;
        }
        header h1 {
          font-size: 32px;
          font-weight: 800;
          color: var(--primary-dark);
          letter-spacing: -1px;
          margin-bottom: 8px;
        }
        header p {
          font-size: 18px;
          color: #6b7280;
        }
  
        /* Card Styling */
        .card {
          background-color: var(--card-bg);
          padding: 30px;
          border-radius: 12px;
          box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
            0 4px 6px -2px rgba(0, 0, 0, 0.05);
          border-top: 4px solid var(--primary-gray); /* Darker border for Slav */
        }
  
        .card-header {
          display: flex;
          align-items: center;
          margin-bottom: 16px;
        }
        .card-header span {
          font-size: 28px;
          margin-right: 12px;
        }
        .card-header h2 {
          font-size: 24px;
          font-weight: 700;
          color: var(--primary-gray);
        }
        .card h3 {
          font-size: 20px;
          font-weight: 600;
          color: var(--heading-color);
          margin-bottom: 20px;
        }
  
        /* Content Styles */
        .content p {
          color: var(--text-color);
          line-height: 1.6;
          margin-bottom: 20px;
        }
  
        /* Code Block/Key Lines */
        .key-sequence {
          background-color: #e5e7eb;
          padding: 15px;
          border-radius: 8px;
          margin-bottom: 20px;
        }
        .key-sequence h4 {
          font-size: 16px;
          font-weight: 700;
          margin-bottom: 8px;
          color: var(--primary-dark);
        }
        .key-sequence code {
          display: block;
          background-color: #d1d5db;
          font-family: monospace;
          padding: 10px;
          border-radius: 4px;
          font-size: 14px;
          color: var(--primary-dark);
          white-space: pre-wrap; /* Ensure wrapping on smaller screens */
        }
  
        /* List Styles */
        .variations-list {
          list-style: disc;
          margin-left: 20px;
          padding-left: 0;
          color: var(--text-color);
          line-height: 1.5;
        }
        .variations-list li {
          margin-bottom: 8px;
        }
        .variations-list strong {
          font-weight: 600;
        }
  
        /* Footer */
        footer {
          margin-top: 40px;
          padding-top: 20px;
          text-align: center;
          color: #6b7280;
          font-size: 14px;
          border-top: 1px solid #e5e7eb;
        }
  
        /* Responsive adjustments */
        @media (min-width: 768px) {
          header h1 {
            font-size: 44px;
          }
          .card {
            padding: 40px;
          }
        }
      </style>
    </head>
    <body>
      <div class="container">
        <header>
          <h1>The Slav Defense</h1>
          <p>A solid, classical, and structurally sound response to 1. d4.</p>
        </header>
  
        <main>
          <!-- SLAV DEFENSE CARD -->
          <div class="card">
            <div class="card-header">
              <span role="img" aria-label="Rook icon">♜</span>
              <h2>Key Strategies</h2>
            </div>
            <h3 class="opening-move">Start: 1. d4 d5 2. c4 c6</h3>
  
            <div class="content">
              <p>
                The Slav is a reliable way for Black to meet 1. d4. The key idea
                of 2... c6 is to reinforce the d5 pawn while keeping the
                light-squared bishop free to develop outside the pawn chain (on f5
                or g4). It often leads to positional maneuvering rather than the
                sharp tactical lines found in the Sicilian, offering excellent
                control over the center.
              </p>
  
              <!-- Key Lines -->
              <div class="key-sequence">
                <h4>Key Move Sequence (Slav Accepted)</h4>
                <code title="1. d4 d5 2. c4 c6 3. Nf3 Nf6 4. Nc3 dxc4">
                  1. d4 d5 2. c4 c6 3. Nf3 Nf6 4. Nc3 dxc4
                </code>
              </div>
  
              <!-- Sub-Variations -->
              <div class="variations">
                <h3>Major Sub-Variations:</h3>
                <ul class="variations-list">
                  <li>
                    <strong class="font-medium">Semi-Slav:</strong> Black plays
                    ...e6 in addition to ...c6. This leads to complex Queen's
                    Gambit Declined structures where Black accepts a blocked c8
                    bishop for a strong central defense.
                  </li>
                  <li>
                    <strong class="font-medium">Anti-Slav Variations:</strong>
                    White avoids 3. Nc3, often playing 3. Nf3 followed by 4. e3 or
                    4. Qb3, attempting to gain space and challenge Black's
                    development early.
                  </li>
                  <li>
                    <strong class="font-medium">Chebanenko Slav:</strong> Black
                    plays 3... a6, securing the b5 square for their light-squared
                    bishop or knight, leading to more original and dynamic lines.
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </main>
  
        <footer>
          <p>This document is made for Computer Networks 2025. <br />-adieos</p>
        </footer>
      </div>
    </body>
  </html>
  ```

  Start service nginx :

  ```
  nginx -c /myscripts/myconfig/nginx.conf
  ```

<br>

## Soal 10

> Untuk memudahkan akses, buatlah satu domain lagi dengan nama **openings.com** yang mengarah ke **Petrov.** Lalu, konfigurasikan juga **Petrov** sebagai **Reverse Proxy** yang akan melakukan forward request ke server yang sesuai berdasarkan URL profile yang diminta oleh klien dengan ketentuan sebagai berikut:
> - Request untuk “openings.com/**sicilian**” harus dialihkan ke web server **Sicilian.**
> - Request untuk “openings.com/**slav**” harus dialihkan ke web server **Slav.**

> _To facilitate access, create another domain with the name **openings.com** that points to **Petrov.** Then, configure **Petrov** as a **Reverse Proxy** that will forward requests to the appropriate server based on the profile URL requested by the client with the following conditions:_
> - _Requests for “openings.com/**sicilian**” must be forwarded to web server **Sicilian.**_
> - _Request for “openings.com/**slav**” must be forwarded to web server **Slav.**_

**Answer:**

- Screenshot

  Tes curl ke `openings.com/Sicilian` dan `openings.com/Slav` :
  
  ![](https://drive.google.com/uc?export=view&id=1tbSgnjAE7GLyYPH4tB7iEUZ9TAEr8DKu)

- Explanation

  1. Konfigurasi DNS Server `Caro-Kann`

     Tambahkan zona domain `openings.com` di `/etc/bind/named.conf.local` :

     ```
      zone "openings.com" {
          type master;
          file "/etc/bind/jarkom/openings.com";
          also-notify { 10.64.41.194; };
          allow-transfer { 10.64.41.194; };
      };
     ```

     Tambahkan database `openings.com` di `/etc/bind/jarkom/openings.com` :

     ```
      $TTL    604800
      @       IN      SOA     openings.com. root.openings.com. (
                           2023101001         ; Serial
                               604800         ; Refresh
                                86400         ; Retry
                              2419200         ; Expire
                               604800 )       ; Negative Cache TTL
      ;
      @       IN      NS      openings.com.
      @       IN      A       10.64.41.217
      www     IN      CNAME   openings.com.
     ```

     Restart service bind9 :

     ```
     service bind9 restart

     \\ ATAU

     named -g
     ```
 
  2. Konfigurasi DNS Slave `Alekhine`

     Tambahkan zona domain untuk `openings.com`

     ```
      zone "openings.com" {
          type slave;
          masters { 10.64.41.193; };
          file "/var/lib/bind/openings.com";
      };
     ```

     Restart service bind9 :

     ```
     service bind9 restart

     \\ ATAU

     named -g
     ```
 
  4. Konfigurasi Reverse Proxy `Petrov`
 
     Install nginx :

     ```
     apt-get update
     apt-get install -y nginx
     ```
  
     Buat file konfigurasi nginx di `/myscripts/myconfig/nginx.conf` untuk **Reverse Proxy** yang mengarahkan `openings.com` ke masing-masing web server :
  
     ```
      user www-data;
      worker_processes auto;
      # PID file ditaruh di folder custom tmp
      pid /myscripts/tmp/nginx.pid;
      events { worker_connections 768; }
      
      http {
          include /etc/nginx/mime.types;
          default_type application/octet-stream;
      
          # LOG FORMAT
          log_format jarkom_format "[$time_local] Jarkom Node Petrov Access from $remote_addr using method \"$request\" returned status $status with $body_bytes_sent bytes sent in $request_time seconds";
      
          # LOGGING ke folder custom
          access_log /myscripts/tmp/access.log;
          error_log /myscripts/tmp/error.log;
      
          # SERVER BLOCK (Reverse Proxy)
          server {
              listen 80;
              server_name openings.com www.openings.com;
      
              #       PROXY KE SICILIAN
              location /sicilian {
                  #           PENTING: Tanda slash (/) di akhir IP untuk menghapus prefix "/sicilian"
                  proxy_pass http://10.64.41.1/;
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
              }
      
              #       PROXY KE SLAV (Port 8000)
              location /slav {
                  #           PENTING: Tanda slash (/) di akhir URL
                  proxy_pass http://10.64.40.1:8000/;
                  proxy_set_header Host $host;
                  proxy_set_header X-Real-IP $remote_addr;
              }
          }
      }
      ```

<br>

## Soal 11

> Tambahkan juga konfigurasi agar request untuk “openings.com/**random**” akan mengalihkan request ke webserver **Sicilian** dan **Slav** dengan algoritma _round-robin_.

> _Additionally, configure requests for "openings.com/**random**" to be redirected to the **Sicilian** and **Slav** web servers using a round-robin algorithm._

**Answer:**

- Screenshot

  Tes curl `openings.com/random` sebanyak 8 kali. Jika round-robin berhasil, maka seharusnya ada 4 baris log di masing-masing node web server :
  <br> <br>
  Isi `access.log` sebelum tes curl :
  
  ![](https://drive.google.com/uc?export=view&id=1zCrfFNhhdhTpxzMFOENtNBojYQZddVIp)

  Isi `access.log` setelah tes curl :
  
  ![](https://drive.google.com/uc?export=view&id=12uS50TWsRpF-q034wGHg-zNoYbBOKQRd)

- Explanation

  Di `Petrov`, tambahkan algoritma _round-robin_ dengan `upstream backend_server` di file `/myscripts/myconfig/nginx.conf` untuk `openings.com/random` :

  ```
  user www-data;
  worker_processes auto;
  # PID file ditaruh di folder custom tmp
  pid /myscripts/tmp/nginx.pid;
  events { worker_connections 768; }
  
  http {
      include /etc/nginx/mime.types;
      default_type application/octet-stream;
  
      # LOG FORMAT
      log_format jarkom_format "[$time_local] Jarkom Node Petrov Access from $remote_addr using method \"$request\" returned status $status with $body_bytes_sent bytes sent in $request_time seconds";
  
      # LOGGING ke folder custom
      access_log /myscripts/tmp/access.log;
      error_log /myscripts/tmp/error.log;
  
      # --- BAGIAN LOAD BALANCER (UPSTREAM) ---
      # Definisi grup server (Round Robin secara default)
      upstream backend_servers {
          server 10.64.41.1;      # Sicilian (Port 80)
          server 10.64.40.1:8000; # Slav (Port 8000)
      }
  
      # SERVER BLOCK (Reverse Proxy)
      server {
          listen 80;
          server_name openings.com www.openings.com;
  
          #       PROXY KE SICILIAN
          location /sicilian {
              #           PENTING: Tanda slash (/) di akhir IP untuk menghapus prefix "/sicilian"
              proxy_pass http://10.64.41.1/;
              proxy_set_header Host $host;
              proxy_set_header X-Real-IP $remote_addr;
          }
  
          #       PROXY KE SLAV (Port 8000)
          location /slav {
              #           PENTING: Tanda slash (/) di akhir URL
              proxy_pass http://10.64.40.1:8000/;
              proxy_set_header Host $host;
              proxy_set_header X-Real-IP $remote_addr;
          }
          #       PROXY KE RANDOM (LOAD BALANCING)
          location /random {
              #           Arahkan ke nama upstream "backend_servers"
              #           Tanda slash (/) di akhir PENTING agar path "/random" dihapus sebelum dikirim ke backend
              proxy_pass http://backend_servers/;
              proxy_set_header Host $host;
              proxy_set_header X-Real-IP $remote_addr;
          }
      }
  }
  ```

<br>

## Soal 12

> Anatoly Parkov berencana untuk melakukan ekspansi secara besar-besaran. Maka dari itu, hapus seluruh konfigurasi Static Routing dan ubah agar seluruh router menggunakan Dynamic Routing. Gunakan protokol RIP!

> _Anatoly Parkov plans to perform a great expansion. Therefore, remove all Static Routing configurations and configure all routers to use Dynamic Routing. Use the RIP protocol!_

**Answer:**

- Screenshot

  Hasil **Dynamic Routing** dengan `show ip route` dan tes koneksi antar node :
  ![](https://drive.google.com/uc?export=view&id=1hfVNaqdUORNVyXqz5mx3_HQBN2Jz9ux-)

- Explanation

  Nyalakan semua service yang diperlukan **Dynamic Routing** di setiap router :

  ```
  ./zebra -d
  ./ripd -d
  ./mgmtd -d

  vtysh

  conf t
  router rip 
  ```

  Lakukan perintah `network <NID>/<NETMASK>` di setiap router. <br> `Lucena` :
  ```
  network 10.64.41.128/26
  network 10.64.41.208/29
  ```
  
  `Zugzwang` :
  ```
  network 10.64.41.216/29
  network 10.64.41.0/25
  network 10.64.41.192/28
  network 10.64.40.0/24
  ```
  
  `Smith-Morra` :
  ```
  network 10.64.41.224/30
  network 10.64.32.0/21
  network 10.64.0.0/19
  ```
  
  `Zwischenzug` :
  ```
  network 10.64.41.208/29
  network 10.64.41.216/29
  ```
  
  `Fianchetto` :
  ```
  network 10.64.41.208/29
  network 10.64.41.224/30
  ```
  

<br>

## Soal 13

> Untuk meningkatkan keamanan, konfigurasikan firewall **Smith-Morra** untuk melakukan pembatasan koneksi SSH ke server DNS. Drop semua packet SSH yang berasal dari seluruh client yang memiliki tujuan ke **Caro-Kann** atau **Alekhine.**

> _To increase security, configure the **Smith-Morra** firewall to restrict SSH connections to the **DNS server.** Drop all SSH packets from all clients destined for **Caro-Kann** or **Alekhine.**_

**Answer:**

- Screenshot

  Tes koneksi (`ping` dan `ssh`) dari node client (`Stafford`) dan node non-client (`Slav`) :
  
  ![](https://drive.google.com/uc?export=view&id=1PIChfHq65bz8SASBioLurVKVYJ0A72Vd)

- Explanation

  Setup firewall dengan iptables yang men-_drop_ paket dengan port 22 (ssh) yang mau di-_forward_ melalui node `Smith-Morra` :

  ```
  iptables -A FORWARD -p tcp --dport 22 -d 10.64.41.193 -j DROP
  iptables -A FORWARD -p tcp --dport 22 -d 10.64.41.194 -j DROP
  ```

<br>

## Soal 14

> Nampaknya, web server juga manusia sehingga hanya ingin bekerja di hari kerja. Maka dari itu, semua client hanya bisa mengakses **Sicilian** dan **Slav** pada hari Senin-Jumat pada pukul 09:00-17:00.

> _Apparently, web servers are humans too, so they only want to work on weekdays. Therefore, all clients can only access **Sicilian** and **Slav** on Monday through Friday, 9:00 AM to 5:00 PM._

**Answer:**

- Screenshot

  Tes curl saat didalam dan diluar jangka waktu dari soal :
  
  ![](https://drive.google.com/uc?export=view&id=1mLPUFTZohQ4hZCGq5ZJ-klEybkjGmjTj) 

- Explanation

  Di `Smith-Morra` :

  Setup iptables agar menerima koneksi yang sudah _established_ untuk tidak menghalangi koneksi internet :

  ```
  iptables -A FORWARD -m state --state ESTABLISHED,RELATED -j ACCEPT
  ```

  Setup iptables agar menerima paket ke `Sicilian` (port 80) dan `Slav` (port 8000, 8888) yang berada di jangka waktu sesuai soal :
  ```
  iptables -A FORWARD -d 10.64.41.1 -p tcp --dport 80 -m time --timestart 09:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
  iptables -A FORWARD -d 10.64.40.1 -p tcp -m multiport --dports 8000,8888 -m time --timestart 09:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
  ```

  Setup iptables agar men-drop semua paket yang selain kondisi diatas walaupun port nya sama :
  ```
  iptables -A FORWARD -d 10.64.41.1 -p tcp --dport 80 -j DROP
  iptables -A FORWARD -d 10.64.40.1 -p tcp -m multiport --dports 8000,8888 -j DROP
  ```

<br>

## Soal 15

> Terakhir, Gerry Paskarov berpesan untuk selalu melakukan logging, sehingga konfigurasikan fitur logging untuk melakukan log terhadap seluruh paket yang di-DROP pada firewall **Smith-Morra.**
> _Finally, Gerry Paskarov advises to always perform logging, so configure a logging feature to log all packets dropped on the **Smith-Morra** firewall._

**Answer:**

- Screenshot

  ![](https://drive.google.com/uc?export=view&id=)

- Explanation

  `Put your explanation in here`

<br>
  
## Problems

## Revisions (if any)
