#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct {
    char name[50];
    float price;
    int stock;
} Product;

typedef struct {
    char name[50];
    float price;
    int quantity;
} CartItem;

#define MAX_PRODUCTS 10
#define MAX_CART_ITEMS 10

Product products[MAX_PRODUCTS] = {
    {"Whey Protein", 29.99, 10},
    {"Casein Protein", 34.99, 5},
    {"Soy Protein", 24.99, 8},
    {"Pea Protein", 27.99, 7},
    {"Egg Protein", 31.99, 6}
};

CartItem cart[MAX_CART_ITEMS];
int cartSize = 0;

void displayProducts() {
    printf("Available Products:\n");
    for (int i = 0; i < MAX_PRODUCTS; i++) {
        if (products[i].stock > 0) {
            printf("%d. %s - $%.2f (Stock: %d)\n", i + 1, products[i].name, products[i].price, products[i].stock);
        }
    }
}

void addToCart(int productIndex, int quantity) {
    if (productIndex < 0 || productIndex >= MAX_PRODUCTS || products[productIndex].stock < quantity) {
        printf("Invalid product selection or insufficient stock.\n");
        return;
    }

    for (int i = 0; i < cartSize; i++) {
        if (strcmp(cart[i].name, products[productIndex].name) == 0) {
            cart[i].quantity += quantity;
            products[productIndex].stock -= quantity;
            printf("Added %d more %s to your cart.\n", quantity, cart[i].name);
            return;
        }
    }

    if (cartSize < MAX_CART_ITEMS) {
        strcpy(cart[cartSize].name, products[productIndex].name);
        cart[cartSize].price = products[productIndex].price;
        cart[cartSize].quantity = quantity;
        products[productIndex].stock -= quantity;
        cartSize++;
        printf("Added %s to your cart.\n", products[productIndex].name);
    } else {
        printf("Your cart is full.\n");
    }
}

void removeFromCart(int cartIndex) {
    if (cartIndex < 0 || cartIndex >= cartSize) {
        printf("Invalid cart selection.\n");
        return;
    }

    for (int i = 0; i < MAX_PRODUCTS; i++) {
        if (strcmp(products[i].name, cart[cartIndex].name) == 0) {
            products[i].stock += cart[cartIndex].quantity;
            break;
        }
    }

    for (int i = cartIndex; i < cartSize - 1; i++) {
        cart[i] = cart[i + 1];
    }

    cartSize--;
    printf("Removed item from your cart.\n");
}

void displayCart() {
    printf("Your Cart:\n");
    for (int i = 0; i < cartSize; i++) {
        printf("%d. %s - $%.2f (Quantity: %d)\n", i + 1, cart[i].name, cart[i].price, cart[i].quantity);
    }
}

void checkout() {
    float total = 0.0;
    for (int i = 0; i < cartSize; i++) {
        total += cart[i].price * cart[i].quantity;
    }
    printf("Your total is: $%.2f\n", total);
    printf("Thank you for your purchase!\n");
    cartSize = 0;
}

int main() {
    int choice, productIndex, quantity, cartIndex;

    while (1) {
        printf("\n1. Display Products\n2. Add to Cart\n3. Remove from Cart\n4. View Cart\n5. Checkout\n6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1:
                displayProducts();
                break;
            case 2:
                printf("Enter product number: ");
                scanf("%d", &productIndex);
                printf("Enter quantity: ");
                scanf("%d", &quantity);
                addToCart(productIndex - 1, quantity);
                break;
            case 3:
                printf("Enter cart item number: ");
                scanf("%d", &cartIndex);
                removeFromCart(cartIndex - 1);
                break;
            case 4:
                displayCart();
                break;
            case 5:
                checkout();
                break;
            case 6:
                exit(0);
            default:
                printf("Invalid choice.\n");
        }
}
}
