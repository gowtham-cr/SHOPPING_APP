# SHOPPING_APP
//SHOPPING_APP_PROJECT.JAVA
package Day_class;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

class Product {
    private int id;
    private String name;
    private double price;
    private String description;

    public Product(int id, String name, double price, String description) {
        this.id = id;
        this.name = name;
        this.price = price;
        this.description = description;
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

    public String getDescription() {
        return description;
    }
}

class ShoppingCart {
    private List<Product> cartItems;

    public ShoppingCart() {
        this.cartItems = new ArrayList<>();
    }

    public void addToCart(Product product) {
        cartItems.add(product);
    }

    public void displayCart() {
        if (cartItems.isEmpty()) {
            System.out.println("Your shopping cart is empty.");
        } else {
            System.out.println("Your shopping cart:");
            for (Product product : cartItems) {
                System.out.println(product.getName() + " - $" + product.getPrice());
            }
            System.out.println("Total: $" + calculateTotal());
        }
    }

    public double calculateTotal() {
        double total = 0;
        for (Product product : cartItems) {
            total += product.getPrice();
        }
        return total;
    }
}

public  class SimpleShoppingApp {
    private static List<Product> products = new ArrayList<>();
    private static ShoppingCart cart = new ShoppingCart();
    private static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeProducts();

        System.out.println("Welcome to Simple Shopping App!");

        while (true) {
            displayMenu();
            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline character

            switch (choice) {
                case 1:
                    displayProducts();
                    break;
                case 2:
                    addToCart();
                    break;
                case 3:
                    viewCart();
                    break;
                case 4:
                    checkout();
                    return;
                case 5:
                    System.out.println("Thank you for using Simple Shopping App!");
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    private static void initializeProducts() {
        // Initialize some sample products
        products.add(new Product(1, "Laptop", 999.99, "Powerful laptop for all your needs."));
        products.add(new Product(2, "Smartphone", 599.99, "Latest model with great features."));
        products.add(new Product(3, "Headphones", 149.99, "Noise-cancelling headphones."));
        products.add(new Product(4, "Book", 19.99, "Bestseller by Famous Author."));
    }

    private static void displayMenu() {
        System.out.println("\nMenu:");
        System.out.println("1. View Products");
        System.out.println("2. Add to Cart");
        System.out.println("3. View Cart");
        System.out.println("4. Checkout");
        System.out.println("5. Exit");
        System.out.print("Enter your choice: ");
    }

    private static void displayProducts() {
        System.out.println("\nAvailable Products:");
        for (Product product : products) {
            System.out.println(product.getId() + ". " + product.getName() + " - $" + product.getPrice());
            System.out.println("   " + product.getDescription());
        }
    }

    private static void addToCart() {
        System.out.print("\nEnter product ID to add to cart: ");
        int productId = scanner.nextInt();
        scanner.nextLine(); // Consume newline character

        Product selectedProduct = null;
        for (Product product : products) {
            if (product.getId() == productId) {
                selectedProduct = product;
                break;
            }
        }

        if (selectedProduct != null) {
            cart.addToCart(selectedProduct);
            System.out.println(selectedProduct.getName() + " added to cart.");
        } else {
            System.out.println("Product not found.");
        }
    }

    private static void viewCart() {
        cart.displayCart();
    }

    private static void checkout() {
        System.out.println("\nChecking out...");
        cart.displayCart();
        System.out.println("Thank you for shopping with us!");
    }
}
