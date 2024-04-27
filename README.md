#client.py
import socket
import time
import threading

def english_to_indonesian_color(english_color):
    color_mapping = {
        "red": "merah",
        "green": "hijau",
        "blue": "biru",
        "yellow": "kuning",
        "purple": "ungu",
        "orange": "oranye",
        "black": "hitam",
        "white": "putih",
        "brown": "coklat",
        "pink": "merah muda",
    }
    return color_mapping.get(english_color.lower(), "tidak dikenali")

server_ip = "127.0.0.1"  # Ganti dengan alamat IP server
server_port = 12345

client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)



while True:
    try:
        def input_with_timeout(prompt ,timeout):
            print(prompt, flush=True)
            response = [None]  # Response will be stored here
            def input_thread():
                try:
                    response[0] = input()
                except:
                    pass

            thread = threading.Thread(target=input_thread)
            thread.start()
            thread.join(timeout)

            if thread.is_alive():
                print(f"\nAnda tidak menjawab selama {timeout} detik\n")
                print("Tekan Enter untuk melanjutkan\n")
                thread.join()
                
                return None
            else:
                return response[0]
            
        client_socket.sendto("request_color".encode("utf-8"), (server_ip, server_port))
        color, server_address = client_socket.recvfrom(1024)
        color = color.decode("utf-8")
        print(f"Warna yang diterima: {color}")

        # Klien memiliki waktu 5 detik untuk merespons
        response = input_with_timeout("Apa warna dalam bahasa Indonesia? ", 5)

        indonesian_color = english_to_indonesian_color(color)
        if response is None:
            print("Waktu habis. Nilai feedback: 0")
        elif response.lower() == indonesian_color:
            print("Jawaban benar! Nilai feedback: 100")
        else:
            print("Jawaban salah. Nilai feedback: 0")

        print("Tunggu 10 detik untuk menerima warna baru\n")
        time.sleep(10)  # Tunggu 10 detik sebelum mengirim permintaan lagi
    except KeyboardInterrupt:
        print("\nKlien berhenti.")
        break

client_socket.close()

#server
import socket
import time
import threading

def english_to_indonesian_color(english_color):
    color_mapping = {
        "red": "merah",
        "green": "hijau",
        "blue": "biru",
        "yellow": "kuning",
        "purple": "ungu",
        "orange": "oranye",
        "black": "hitam",
        "white": "putih",
        "brown": "coklat",
        "pink": "merah muda",
    }
    return color_mapping.get(english_color.lower(), "tidak dikenali")

server_ip = "127.0.0.1"  # Ganti dengan alamat IP server
server_port = 12345

client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)



while True:
    try:
        def input_with_timeout(prompt ,timeout):
            print(prompt, flush=True)
            response = [None]  # Response will be stored here
            def input_thread():
                try:
                    response[0] = input()
                except:
                    pass

            thread = threading.Thread(target=input_thread)
            thread.start()
            thread.join(timeout)

            if thread.is_alive():
                print(f"\nAnda tidak menjawab selama {timeout} detik\n")
                print("Tekan Enter untuk melanjutkan\n")
                thread.join()
                
                return None
            else:
                return response[0]
            
        client_socket.sendto("request_color".encode("utf-8"), (server_ip, server_port))
        color, server_address = client_socket.recvfrom(1024)
        color = color.decode("utf-8")
        print(f"Warna yang diterima: {color}")

        # Klien memiliki waktu 5 detik untuk merespons
        response = input_with_timeout("Apa warna dalam bahasa Indonesia? ", 5)

        indonesian_color = english_to_indonesian_color(color)
        if response is None:
            print("Waktu habis. Nilai feedback: 0")
        elif response.lower() == indonesian_color:
            print("Jawaban benar! Nilai feedback: 100")
        else:
            print("Jawaban salah. Nilai feedback: 0")

        print("Tunggu 10 detik untuk menerima warna baru\n")
        time.sleep(10)  # Tunggu 10 detik sebelum mengirim permintaan lagi
    except KeyboardInterrupt:
        print("\nKlien berhenti.")
        break

client_socket.close()



penjelasan kode server

Kode mengimpor modul socket untuk membuat socket jaringan, modul random untuk menghasilkan warna secara acak, dan modul time untuk operasi terkait waktu, meskipun tidak digunakan dalam kode ini.
Fungsi generate_random_color() membuat daftar warna-warna yang tersedia, kemudian memilih warna secara acak dari daftar tersebut menggunakan random.choice().
Server_ip dan server_port menyimpan alamat IP dan nomor port server. Alamat IP ditetapkan sebagai "127.0.0.1" (localhost), dan nomor port ditetapkan sebagai 12345.
Socket UDP dibuat menggunakan socket.socket(socket.AF_INET, socket.SOCK_DGRAM), kemudian diikat ke alamat IP dan nomor port server dengan server_socket.bind((server_ip, server_port)).
Kode mencetak pesan yang menunjukkan bahwa server berjalan di alamat IP dan nomor port yang telah ditetapkan Set connected_clients digunakan untuk menyimpan daftar alamat klien yang terhubung ke server. Dalam loop while True, server menunggu permintaan dari klien. Jika permintaan diterima dan berisi pesan "request_color", server memanggil generate_random_color() untuk mendapatkan warna secara acak, dan mengirimkan warna tersebut kembali ke klien.
Jika klien baru terhubung ke server, alamat klien ditambahkan ke set connected_clients, dan pesan dicetak untuk menunjukkan bahwa klien telah terhubung.
Jika terjadi interupsi keyboard (KeyboardInterrupt), loop akan berhenti, dan socket server akan ditutup. Secara keseluruhan, 
kode ini menciptakan server UDP yang mengirimkan warna secara acak kepada klien yang terhubung ketika klien mengirim permintaan 
"request_color". Server ini berjalan di alamat IP 127.0.0.1 (localhost) dan nomor port 12345.

penjelasan kode client
Kode menggunakan modul socket untuk membuat socket jaringan, modul time untuk operasi waktu, dan modul threading untuk membuat thread baru.
Fungsi `english_to_indonesian_color(english_color)` menghubungkan warna dalam bahasa Inggris ke dalam bahasa Indonesia dengan menggunakan kamus `color_mapping`. Jika warna dalam bahasa Inggris tidak ada dalam kamus, maka akan dikembalikan "tidak dikenali".
Variabel `server_ip` dan `server_port` menyimpan alamat IP dan nomor port server (sama dengan kode server sebelumnya).
Sebuah socket UDP dibuat dengan menggunakan `socket.socket(socket.AF_INET, socket.SOCK_DGRAM)` untuk klien.
Fungsi `input_with_timeout(prompt, timeout)` digunakan untuk membaca input dari pengguna dengan batas waktu `timeout` detik. Fungsi ini membuat thread baru yang menjalankan `input_thread()` untuk membaca input dari pengguna. Jika pengguna tidak merespons dalam `timeout` detik, maka akan mencetak pesan dan mengembalikan `None`.
Dalam loop `while True`, klien mengirimkan permintaan "request_color" ke server dan menunggu balasan berupa warna dalam bahasa Inggris.
Setelah menerima warna dalam bahasa Inggris dari server, klien mencetak warna tersebut dan meminta pengguna untuk menerjemahkan warna tersebut ke dalam bahasa Indonesia menggunakan `input_with_timeout()` dengan waktu tunggu 5 detik.
Jawaban pengguna dibandingkan dengan terjemahan warna dalam bahasa Indonesia menggunakan `english_to_indonesian_color()`. Jika jawaban benar, maka akan dicetak pesan "Jawaban benar! Nilai feedback: 100", jika salah atau waktu habis, maka akan dicetak pesan "Jawaban salah. Nilai feedback: 0" atau "Waktu habis. Nilai feedback: 0".
Setelah memberikan feedback, klien akan menunggu selama 10 detik sebelum mengirim permintaan warna baru ke server.
Jika terjadi interupsi keyboard (KeyboardInterrupt), loop akan berhenti, dan klien akan menutup socket.
Secara keseluruhan, kode ini membuat klien UDP yang terhubung ke server warna dari kode sebelumnya. Klien akan meminta warna dalam bahasa Inggris dari server, dan meminta pengguna untuk menerjemahkan warna tersebut ke dalam bahasa Indonesia dengan batasan waktu 5 detik. Jika pengguna menjawab dengan benar, maka akan diberikan nilai feedback 100, jika salah atau waktu habis, maka nilai feedback adalah 0. Setelah memberikan feedback, klien akan menunggu 10 detik sebelum meminta warna baru dari server.
