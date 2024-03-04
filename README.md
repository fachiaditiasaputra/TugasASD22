class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def tambah_di_awal(self, data):
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node

    def tambah_di_akhir(self, data):
        new_node = Node(data)
        if not self.head:
            self.head = new_node
            return
        current = self.head
        while current.next:
            current = current.next
        current.next = new_node

    def tambah_di_antara(self, posisi, data):
        if posisi < 0:
            print("Posisi tidak valid")
            return
        if posisi == 0:
            self.tambah_di_awal(data)
            return
        new_node = Node(data)
        current = self.head
        prev = None
        count = 0
        while current and count < posisi:
            prev = current
            current = current.next
            count += 1
        if not current:
            print("Posisi melebihi panjang Linked List")
            return
        prev.next = new_node
        new_node.next = current

    def hapus_di_awal(self):
        if not self.head:
            print("Linked List kosong")
            return
        self.head = self.head.next

    def hapus_di_akhir(self):
        if not self.head:
            print("Linked List kosong")
            return
        if not self.head.next:
            self.head = None
            return
        current = self.head
        while current.next.next:
            current = current.next
        current.next = None

    def hapus_di_posisi(self, posisi):
        if not self.head:
            print("Linked List kosong")
            return
        if posisi == 0:
            self.hapus_di_awal()
            return
        current = self.head
        prev = None
        count = 0
        while current and count < posisi:
            prev = current
            current = current.next
            count += 1
        if not current:
            print("Posisi melebihi panjang Linked List")
            return
        prev.next = current.next

    def tampilkan(self):
        if not self.head:
            print("Linked List kosong")
            return
        current = self.head
        while current:
            print(current.data, end=" -> ")
            current = current.next
        print("None")

class TokoIkanHias:
    def __init__(self):
        self.ikan_hias = LinkedList()
        self.counter = 0

    def tambah_ikan_hias(self, nama, jenis, makanan, jenis_kelamin, harga, stok):
        self.counter += 1
        new_ikan = {
            'id': self.counter,
            'nama': nama,
            'jenis': jenis,
            'makanan': makanan,
            'jenis_kelamin': jenis_kelamin,
            'harga': harga,
            'stok': stok,
        }
        self.ikan_hias.tambah_di_akhir(new_ikan)

    def lihat_ikan_hias(self):
        self.ikan_hias.tampilkan()

    def ubah_ikan_hias(self, id_ikan, field, ikan_baru):
        current = self.ikan_hias.head
        while current:
            if current.data['id'] == id_ikan:
                current.data[field] = ikan_baru
                print("=====================")
                print("Ikan Berhasil Diubah")
                print("=====================")
                return
            current = current.next
        print("=====================")
        print("Ikan Tidak Ditemukan")
        print("=====================")

    def hapus_ikan_hias(self, id_ikan):
        current = self.ikan_hias.head
        prev = None
        while current:
            if current.data['id'] == id_ikan:
                if not prev:
                    self.ikan_hias.hapus_di_awal()
                else:
                    prev.next = current.next
                print("===========================")
                print("Ikan Hias Berhasil Dihapus")
                print("===========================")
                return
            prev = current
            current = current.next
        print("=====================")
        print("Ikan Tidak Ditemukan")
        print("=====================")

def main():
    toko = TokoIkanHias()

    while True:
        print("-------------------------")
        print("Pilihan Menu Ikan Hias ")
        print("-------------------------")
        print("1. Tambah ikan hias")
        print("2. Lihat ikan hias")
        print("3. Ubah ikan hias")
        print("4. Hapus ikan hias")
        print("5. Keluar Program")
        print("-------------------------")

        pilihan = input("Masukkan Pilihan Anda:")

        if pilihan == '1':
            nama = input("Masukkan Nama Ikan Hias:")
            jenis = input("Masukkan Jenis Ikan Hias:")
            makanan = input("Masukkan Jenis Makanan Ikan Hias:")
            jenis_kelamin = input("Masukkan Jenis Kelamin Ikan Hias:")
            harga = float(input("Masukkan Harga Ikan Hias:"))
            stok = int(input("Masukkan Stok Ikan Hias:"))
            toko.tambah_ikan_hias(nama, jenis, makanan, jenis_kelamin, harga, stok)

        elif pilihan == '2':
            toko.lihat_ikan_hias()

        elif pilihan == '3':
            id_ikan = int(input("Masukkan ID Ikan Hias Yang Ingin Diubah:"))
            field = input("Masukkan Nama field Yang Ingin Diubah (nama/jenis/makanan/jenis_kelamin/harga/stok):")
            ikan_baru = input("Masukkan Ikan Hias Baru:")
            toko.ubah_ikan_hias(id_ikan, field, ikan_baru)

        elif pilihan == '4':
            id_ikan = int(input("Masukkan ID Ikan Hias Yang Ingin Dihapus:"))
            toko.hapus_ikan_hias(id_ikan)

        elif pilihan == '5':
            print("Keluar Dari Program")
            break

        else:
            print("Pilihan Tidak Valid. Silahkan Masukkan Pilihan Yang Benar")

if __name__ == "__main__":
    main()

