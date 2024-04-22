import java.util.Scanner;
public class SimpleECommerceSystem {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        System.out.println("Welcome to E-commerce System");
        // product1
        ElectronicProduct p1 = new ElectronicProduct();
        p1.setName("smartphone");
        p1.setProductId(1);
        p1.setPrice(599.9f);
        p1.setBrand("Samsung");
        p1.setWarrantyPeriod(1);
        // product2
        ClothingProduct p2 = new ClothingProduct();
        p2.setName("T-shirt");
        p2.setProductId(2);
        p2.setPrice(19.99f);
        p2.setSize("Medium");
        p2.setFabric("Cotton");
        // product3
        BookProduct p3 = new BookProduct();
        p3.setName("OOP");
        p3.setProductId(3);
        p3.setPrice(39.99f);
        p3.setAuthor("O'Reilly");
        p3.setPublisher("X Publications");
        // customer
        Customer c = new Customer();
        System.out.println("Please enter your id:");
        int id = input.nextInt();
        System.out.println("Please enter your name:");
        String name = input.next();
        System.out.println("Please enter your address:");
        String address = input.next();
        c.setCustomerId(id);
        c.setName(name);
        c.setAddress(address);
        Order o = new Order();
        o.setCustomerId(id);
        Cart cart = new Cart();
        System.out.println("How many producs you want to add to cart?");
        int nProduct = input.nextInt();
        cart.setnProduct(nProduct);
        for (int i = 0; i < nProduct; i++) {
            System.out.println("which product you would like to add? 1-smartphone 2-T-shirt 3-OOP");
            int product = input.nextInt();
            switch (product) {
                case 1:
                    cart.addProduct(p1);
                    break;
                case 2:
                    cart.addProduct(p2);
                    break;
                case 3:
                    cart.addProduct(p3);
                    break;
                default:
                    System.out.println("Product is not available");
                    break;
            }
        }
        System.out.println("Do you want to remove any product from the cart?1-Yes 2-No");
        int removeProduct = input.nextInt();
        if (removeProduct == 1) {
            while (true) {
                System.out.println("How many products do you want to remove?");
                int removedProducts = input.nextInt();
                if (removedProducts > nProduct) {
                    System.out.println("Not valid number");
                } else {
                    for (int i = 0; i < removedProducts; i++) {
                        System.out.println("which product you would like to remove? 1-smartphone 2-T-shirt 3-OOP");
                        int product = input.nextInt();
                        switch (product) {
                            case 1:
                                cart.removeProduct(p1);
                                break;
                            case 2:
                                cart.removeProduct(p2);
                                break;
                            case 3:
                                cart.removeProduct(p3);
                                break;
                            default:
                                System.out.println("Product is not available");
                                break;
                        }
  }
                    break;
                }
            }
        }
        o.setProducts(cart.getProducts());
        o.setTotalPrice(cart.calculatePrice());
        System.out.println("Your total is $" + cart.calculatePrice() + ". Do you want to place your order? 1-Yes 2-No");
        int placeOrder = input.nextInt();
        if (cart.placeOrder(placeOrder)) {
            o.printOrderInfo();
        }
    }

}
***********************************************************************************************************
public class Product {

    private int productId;
    private String name;
    private float price;

    public int getProductId() {
        return productId;
    }

    public void setProductId(int productId) {

        if (productId < 0) {
            this.productId = Math.abs(productId);
        } else {
            this.productId = productId;
        };
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public float getPrice() {
        return price;
    }

    public void setPrice(float price) {
        if (price < 0) {
            this.price = Math.abs(price);
        } else {
            this.price = price;
        }
    }

    @Override
    public String toString() {
        return name + " -$" + price;
    }
}
*******************************************************************************************************
public class ElectronicProduct extends Product {

    String brand;
    int warrantyPeriod;

    String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public int getWarrantyPeriod() {
        return warrantyPeriod;
    }

    public void setWarrantyPeriod(int warrantyPeriod) {

        if (warrantyPeriod < 0) {
            this.warrantyPeriod = Math.abs(warrantyPeriod);
        } else {
            this.warrantyPeriod = warrantyPeriod;
        };

    }

}
*****************************************************************************************************************
public class ClothingProduct extends Product {

    String size;
    String Fabric;

    public String getSize() {
        return size;
    }

    public void setSize(String size) {
        this.size = size;
    }

    public String getFabric() {
        return Fabric;
    }

    public void setFabric(String Fabric) {
        this.Fabric = Fabric;
    }

}
*********************************************************************************************************
public class BookProduct extends Product {

    String author;
    String Publisher;

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getPublisher() {
        return Publisher;
    }

    public void setPublisher(String Publisher) {
        this.Publisher = Publisher;
    }

}
*****************************************************************************************************
public class Customer {

    int customerId;
    String name;
    String address;

    public int getCustomerId() {
        return customerId;
    }

    public void setCustomerId(int customerId) {
       if (customerId < 0) {
            this.customerId = Math.abs(customerId);
        } else {
            this.customerId = customerId;
        };
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

}
********************************************************************************************************
public class Cart {

    int counter = 0;
    int customerId;
    int nProduct;
    Product[] products;

    public int getCustomerId() {
        return customerId;
    }

    public void setCustomerId(int customerId) {
        this.customerId = customerId;
    }

    public int getnProduct() {
        return nProduct;
    }

    public void setnProduct(int nProduct) {
        this.nProduct = Math.abs(nProduct);
        products = new Product[nProduct];

    }

    public Product[] getProducts() {
        return products;
    }

    public void setProducts(Product[] products) {
        this.products = products;
    }

    public void addProduct(Product p) {
        products[counter] = p;
        counter++;

    }

    public void removeProduct(Product p) {
        Product[] products2 = new Product[getnProduct() - 1];
        int indexRemoved = 0;
        for (int i = 0; i < products.length; i++) {
            if (products[i].getProductId() == p.getProductId()) {
                indexRemoved = i;
                break;

            }
        }
        int p2_iterator = 0;
        for (int i = 0; i < products.length; i++) {
            if (i != indexRemoved) {
                products2[p2_iterator] = products[i];
                p2_iterator++;
            }

        }
        setnProduct(getnProduct() - 1);
        setProducts(products2);

    }

    public float calculatePrice() {
        float totalPrice = 0;
        for (int i = 0; i < nProduct; i++) {
            totalPrice += products[i].getPrice();
        }
        return totalPrice;
    }

    public boolean placeOrder(int place) {
        if (place == 1) {
            return true;
        } else {
            return false;
        }

    }

}
*************************************************************************************************************
public class Order {

    int customerId;
    int orderId = 0;
    int nProduct;
    Product[] products = new Product[nProduct];
    float totalPrice;

    public Order() {
        orderId++;
    }

    public int getCustomerId() {
        return customerId;
    }

    public Product[] getProducts() {
        return products;
    }

    public void setProducts(Product[] products) {
        this.products = products;
    }

    public void setCustomerId(int customerId) {
        this.customerId = customerId;
    }

    public float getTotalPrice() {
        return totalPrice;
    }

    public void setTotalPrice(float totalPrice) {
        this.totalPrice = totalPrice;
    }

    public void printOrderInfo() {
        System.out.println("Here's your order's detiles ");
        System.out.println("order id: " + orderId);
        System.out.println("customer's id: " + getCustomerId());
        System.out.println("Products: ");
        for (Product product : products) {
            System.out.println(product.getName() + " $" + product.getPrice());
        }
        System.out.println("Total price: $" + getTotalPrice());

    }
}


