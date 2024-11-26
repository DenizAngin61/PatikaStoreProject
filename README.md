# PatikaStoreProject

Ürün sınıfı

public class Product {
    private int id;
    private String name;
    private double price;
    private String brand;

    public Product(int id, String name, double price, String brand) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.brand = brand;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    public String getBrand() {
        return brand;
    }

    @Override
    public String toString() {
        return "ID: " + id + ", Name: " + name + ", Price: " + price + ", Brand: " + brand;
    }
}


Mağaza yönetimi

import java.util.ArrayList;
import java.util.Scanner;

public class PatikaStore {
    private ArrayList<Product> products = new ArrayList<>();
    private Scanner scanner = new Scanner(System.in);

    public void start() {
        int choice;
        do {
            System.out.println("\n=== Patika Store ===");
            System.out.println("1. Ürünleri Listele");
            System.out.println("2. Ürün Ekle");
            System.out.println("3. Ürün Sil");
            System.out.println("4. Çıkış");
            System.out.print("Seçiminiz: ");
            choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    listProducts();
                    break;
                case 2:
                    addProduct();
                    break;
                case 3:
                    removeProduct();
                    break;
                case 4:
                    System.out.println("Çıkış yapılıyor...");
                    break;
                default:
                    System.out.println("Geçersiz seçim, tekrar deneyin.");
            }
        } while (choice != 4);
    }

    private void listProducts() {
        if (products.isEmpty()) {
            System.out.println("Hiç ürün yok.");
        } else {
            for (Product product : products) {
                System.out.println(product);
            }
        }
    }

    private void addProduct() {
        System.out.print("Ürün ID: ");
        int id = scanner.nextInt();
        scanner.nextLine(); // Buffer temizliği
        System.out.print("Ürün İsmi: ");
        String name = scanner.nextLine();
        System.out.print("Ürün Fiyatı: ");
        double price = scanner.nextDouble();
        scanner.nextLine(); // Buffer temizliği
        System.out.print("Ürün Markası: ");
        String brand = scanner.nextLine();

        products.add(new Product(id, name, price, brand));
        System.out.println("Ürün başarıyla eklendi!");
    }

    private void removeProduct() {
        System.out.print("Silmek istediğiniz ürün ID'sini girin: ");
        int id = scanner.nextInt();

        Product toRemove = null;
        for (Product product : products) {
            if (product.getId() == id) {
                toRemove = product;
                break;
            }
        }

        if (toRemove != null) {
            products.remove(toRemove);
            System.out.println("Ürün başarıyla silindi!");
        } else {
            System.out.println("Ürün bulunamadı.");
        }
    }

    public static void main(String[] args) {
        PatikaStore store = new PatikaStore();
        store.start();
    }
}


