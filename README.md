import java.util.Scanner;

abstract class Penumpang {
    protected String nama;
    protected String noTiket;
    protected double harga;

    public Penumpang(String nama, String noTiket, double harga) {
        this.nama = nama;
        this.noTiket = noTiket;
        this.harga = harga;
    }

    public abstract double hitungHargaTiket();

    public void tampilkanData() {
        System.out.println("Nama        : " + nama);
        System.out.println("No Tiket    : " + noTiket);
        System.out.println("Harga Tiket : " + hitungHargaTiket());
    }

    public void tampilkanData(boolean detail) {
        tampilkanData();
        if (detail) {
            System.out.println("");
        }
    }
}

class PenumpangReguler extends Penumpang {
    public PenumpangReguler(String nama, String noTiket, double harga) {
        super(nama, noTiket, harga);
    }

    @Override
    public double hitungHargaTiket() {
        return harga;
    }

    @Override
    public void tampilkanData(boolean detail) {
        tampilkanData();
        if (detail) {
            System.out.println("Kategori    : Reguler");
        }
    }
}

class PenumpangVIP extends Penumpang {
    public PenumpangVIP(String nama, String noTiket, double harga) {
        super(nama, noTiket, harga);
    }

    @Override
    public double hitungHargaTiket() {
        return harga + (harga * 0.2);
    }

    @Override
    public void tampilkanData(boolean detail) {
        tampilkanData();
        if (detail) {
            System.out.println("Kategori    : VIP");
            System.out.println("Fasilitas   : Lounge & Prioritas Boarding");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.print("Masukkan nama penumpang   : ");
        String nama = input.nextLine();

        System.out.print("Masukkan nomor tiket     : ");
        String noTiket = input.nextLine();

        System.out.print("Masukkan harga dasar     : ");
        double harga = input.nextDouble();

        System.out.print("Jenis penumpang (1=Reguler, 2=VIP): ");
        int pilihan = input.nextInt();

        Penumpang penumpang;

        if (pilihan == 2) {
            penumpang = new PenumpangVIP(nama, noTiket, harga);
        } else {
            penumpang = new PenumpangReguler(nama, noTiket, harga);
        }

        System.out.println("\n=== DATA PENUMPANG ===");
        penumpang.tampilkanData(true);

        input.close();
    }
}
