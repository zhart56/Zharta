package main

import (
	"fmt"
)

const HMAX int = 7

type riwayatTidur struct {
	hari, tanggal,jamTidur,jamBangun     string
	durasi, kualitastidur int
}
type arrTidur [HMAX]riwayatTidur

var nData int = 0

func main() {
	var dataTidur arrTidur
	var pick int

	for {
		menu()
		fmt.Print("Pilih menu ke-")
		fmt.Scanln(&pick)
		switch pick {
		case 1:
			tambahRiwayat(&dataTidur, &nData)
		case 2:
			editRiwayat(&dataTidur, nData)
		case 3:
			hapusRiwayat(&dataTidur, &nData)
		case 4:
			allData(dataTidur, nData)
		case 5:
			var Urutkan int
			fmt.Print("Urutkan berdasarkan (1: Durasi, 2: tanggal): ")
			fmt.Scanln(&Urutkan)
			selectionSort(&dataTidur, nData, Urutkan)
		case 6:
			var urutkan int
			fmt.Print("Urutkan berdasarkan (1: Durasi, 2: tanggal): ")
			fmt.Scanln(&urutkan)
			insertionSort(&dataTidur, nData, urutkan)
		case 7:
			sequentialSearch(dataTidur, nData)
		case 8:
			binarySearch(dataTidur, nData)
		case 9:
			rekapdandata(dataTidur, nData)
		case 10:
			fmt.Println("Terima kasih telah menggunakan program ini.")
			return
		default:
			fmt.Println("Pilihan tidak valid.\n")
		}
	}
}

func menu() {
	fmt.Println("----------------------------------")
	fmt.Println("             M E N U              ")
	fmt.Println("----------------------------------")
	fmt.Println("1. Tambah Riwayat Tidur")
	fmt.Println("2. Edit Riwayat Tidur")
	fmt.Println("3. Hapus Riwayat Tidur")
	fmt.Println("4. Tampilkan Semua Data")
	fmt.Println("5. Urutkan (Selection Sort)")
	fmt.Println("6. Urutkan (Insertion Sort)")
	fmt.Println("7. Cari (Sequential Search)")
	fmt.Println("8. Cari (Binary Search)")
	fmt.Println("9. Rekap & Rata-rata")
	fmt.Println("10. Keluar")
}

func tambahRiwayat(dataTidur *arrTidur, nData *int) {
	if *nData >= HMAX {
		fmt.Println("Data sudah penuh (Maksimal 7 hari).")
		return
	}

	fmt.Print("Masukkan hari: ")
	fmt.Scanln(&dataTidur[*nData].hari)
	fmt.Print("Masukkan tanggal: ")
	fmt.Scanln(&dataTidur[*nData].tanggal)
	fmt.Print("Masukkan jam tidur: ")
	fmt.Scanln(&dataTidur[*nData].jamTidur)
	fmt.Print("Masukkan jam bangun: ")
	fmt.Scanln(&dataTidur[*nData].jamBangun)
	fmt.Print("Masukkan kualitas tidur (1-5): ")
	fmt.Scanln(&dataTidur[*nData].kualitastidur)

	dataTidur[*nData].durasi = totDurasi(dataTidur[*nData].jamTidur, dataTidur[*nData].jamBangun)
	*nData++
	fmt.Println("Data berhasil ditambahkan.")
}
func persejam(jam string) (int, int) {
	var h, m int
	_, simpan := fmt.Sscanf(jam, "%d:%d", &h, &m)
	if simpan != nil || h < 0 || h > 23 || m < 0 || m > 59 {
		return 0, 0
	}
	return h, m

}

func totDurasi(tidur, bangun string) int {

	htidur, mtidur := persejam(tidur)
	hbangun, mbangun := persejam(bangun)
	totaltidur := htidur*60 + mtidur
	totalbangun := hbangun*60 + mbangun
	if totalbangun < totaltidur {
		return (1440 - totaltidur) + totalbangun
	}
	return totalbangun - totaltidur
}

func allData(T arrTidur, nData int) {
	var i int

	if nData == 0 {
		fmt.Println("Belum ada data.\n")
		return
	}
	fmt.Println("== Riwayat Tidur ==")
	for i = 0; i < nData; i++ {
		var durasi int
		durasi = totDurasi(T[i].jamTidur, T[i].jamBangun)
		fmt.Printf("Hari: %s, Tanggal: %s, Tidur: %s, Bangun: %s, Durasi: %d jam %d Menit, Kualitas: %d\n", T[i].hari,
			T[i].tanggal, T[i].jamTidur, T[i].jamBangun, durasi/60, durasi%60, T[i].kualitastidur)
	}
	fmt.Println()
}

func selectionSort(T *arrTidur, nData int, urutkan int) {
	var pass, i, idx int

	for pass = 0; pass < nData-1; pass++ {
		idx = pass
		for i = pass + 1; i < nData-1; i++ {
			if urutkan == 1 && (*T)[idx].durasi > (*T)[i].durasi {
				idx = i
			} else if urutkan == 2 && (*T)[idx].tanggal > (*T)[i].tanggal {
				idx = i
			}
		}
		(*T)[pass] = (*T)[idx]
		(*T)[idx] = (*T)[pass]
	}
	fmt.Println("Data berhasil diurutkan.")
}

func insertionSort(T *arrTidur, nData int, urutkan int) {
	var pass, i int
	var temp riwayatTidur

	for pass = 1; pass < nData; pass++ {
		i = pass
		temp = (*T)[pass]
		for i > 0 {
			if urutkan == 1 && temp.durasi < (*T)[i-1].durasi {
				for i > 0 && temp.durasi < (*T)[i-1].durasi {
					(*T)[i] = (*T)[i-1]
					i--
				}
			} else if urutkan == 2 && temp.tanggal < (*T)[i-1].tanggal {
				for i > 0 && temp.tanggal < (*T)[i-1].tanggal {
					(*T)[i] = (*T)[i-1]
					i--
				}
			} else {
				break
			}
		}
		(*T)[i] = temp
	}
	fmt.Println("Data berhasil diurutkan.")
}

func sequentialSearch(T arrTidur, nData int) {
	var findH string
	var i, found int

	found = -1
	i = 0

	fmt.Print("Masukkan nama hari yang dicari: ")
	fmt.Scanln(&findH)

	for i < nData && found == -1 {
		if T[i].hari == findH {
			found = i
		}
		i++
	}

	if found != -1 {
		fmt.Println("Data ditemukan:")
		var durasi int
		durasi = totDurasi(T[found].jamTidur, T[found].jamBangun)
		fmt.Printf("Hari: %s, Tanggal: %s, Tidur: %s, Bangun: %s, Durasi: %d jam %d menit, Kualitas: %d\n", T[found].hari,
			T[found].tanggal, T[found].jamTidur, T[found].jamBangun, durasi/60, durasi%60, T[found].kualitastidur)
	} else {
		fmt.Println("Data tidak ditemukan.")
	}
}

func binarySearch(T arrTidur, nData int) {
	var found, left, right, mid int
	var findH string
	if nData == 0 {
		fmt.Println("Belum ada data untuk dicari.")
		return
	}
	insertionSort(&T, nData, 2) // urutkan berdasarkan tanggal sebelum pencarian biner

	fmt.Print("Dicari: ")
	fmt.Scanln(&findH)
	found = -1
	left = 0
	right = nData - 1

	for left <= right && found == -1 {
		mid = (left + right) / 2
		if findH == T[mid].hari {
			found = mid
		} else if findH > T[mid].hari {
			left = mid + 1
		} else {
			right = mid - 1
		}
	}

	if found == -1 {
		fmt.Println("Data tidak ditemukan")
	} else {
		fmt.Println("Data ditemukan:")
		var durasi int
		durasi = totDurasi(T[found].jamTidur, T[found].jamBangun)
		fmt.Printf("Hari: %s, Tanggal: %s, Tidur: %s, Bangun: %s, Durasi: %d jam %d menit, Kualitas: %d\n", T[found].hari,
			T[found].tanggal, T[found].jamTidur, T[found].jamBangun, durasi/60,durasi%60, T[found].kualitastidur)
	}
}
func rekapdandata(t arrTidur, ndata int) {
	var temp arrTidur
	var start, total, i int
	var ratarata float64

	if ndata == 0 {
		fmt.Println("Belum ada data.")
		return
	}

	temp = t
	insertionSort(&temp, nData, 2)

	start = 0
	if ndata > 7 {
		start = ndata - 7
	}
	total = 0
	fmt.Println("== Rekap 7 hari terakhir==")
	for i = start; i < nData; i++ {
		var durasi int
		durasi = totDurasi(temp[i].jamTidur, temp[i].jamBangun)
		fmt.Printf("Hari: %s, Tanggal: %s, Durasi: %d jam %d menit\n", temp[i].hari,
			temp[i].tanggal, durasi/60, durasi%60)
	
		total += durasi/60
	}
	ratarata = float64(total) / float64(nData-start)
	fmt.Printf("Rata-rata durasi tidur: %.2f jam\n", ratarata)

	if ratarata < 7 {
		fmt.Println("Saran: Tidur lebih awal untuk mencukupi kebutuhan 7-9 jam per hari.")
	} else {
		fmt.Println("Saran: Pertahankan pola tidur yang baik!")
	}

}
func editRiwayat(T *arrTidur, nData int) {
	if nData == 0 {
		fmt.Println("Belum ada data untuk diubah.")
		return
	}
	var idx int
	fmt.Print("Masukkan data yang akan diubah (hari,tanggal,jam tidur, jam bangun, kualitas tidur) (", nData-1, "): ")
	fmt.Scanln(&idx)
	if idx < 0 || idx >= nData {
		fmt.Println("Indeks tidak valid.")
		return
	}
	fmt.Printf("Edit data hari %s:\n", T[idx].hari)
	fmt.Scanln(&T[idx].hari)
	fmt.Printf("Edit data tanggal %s:\n", T[idx].tanggal)
	fmt.Scanln(&T[idx].tanggal)
	fmt.Print("Jam tidur (0-24): ")
	fmt.Scanln(&T[idx].jamTidur)
	fmt.Print("Jam bangun (0-24): ")
	fmt.Scanln(&T[idx].jamBangun)
	fmt.Print("Kualitas tidur (1-5): ")
	fmt.Scanln(&T[idx].kualitastidur)
	T[idx].durasi = totDurasi(T[idx].jamTidur, T[idx].jamBangun)
	fmt.Println("Data berhasil diubah.")
}

func hapusRiwayat(T *arrTidur, nData *int) {
	if *nData == 0 {
		fmt.Println("Belum ada data untuk dihapus.")
		return
	}
	var idx int
	fmt.Print("Masukkan indeks data yang akan dihapus (0-", *nData-1, "): ")
	fmt.Scanln(&idx)
	if idx < 0 || idx >= *nData {
		fmt.Println("Indeks tidak valid.")
		return
	}
	for i := idx; i < *nData-1; i++ {
		T[i] = T[i+1]
	}
	*nData--
	fmt.Println("Data berhasil dihapus.")
}
