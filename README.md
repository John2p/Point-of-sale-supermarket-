# Point-of-sale-supermarket-#include <iostream>
#include <string>

const float IBUPROFEN_PRICE = 300.0;
const float RANITIDINE_PRICE = 400.0;
int PRODUCT_QUANTITY_IBUPROFEN = 10;    // units of Ibuprofen available
int PRODUCT_QUANTITY_RANITIDINE = 5;   // units of Ranitidine available

void inputCustomerDetails() {
    std::cout << "Enter customer name: ";
    std::string name;
    std::cin >> name;
    // Additional code to process customer details if needed
}

bool checkProductAvailability(std::string productName) {
    if (productName == "Ibuprofen") {
        return PRODUCT_QUANTITY_IBUPROFEN > 0;
    } else if (productName == "Ranitidine") {
        return PRODUCT_QUANTITY_RANITIDINE > 0;
    }

    return false; // Product is unavailable
}

int enterProductQuantity(std::string productName) {
    std::cout << "Enter product quantity for " << productName << ": ";
    int quantity;
    std::cin >> quantity;

    if (productName == "Ibuprofen" && quantity > PRODUCT_QUANTITY_IBUPROFEN) {
        std::cout << "Only " << PRODUCT_QUANTITY_IBUPROFEN << " units of Ibuprofen available." << std::endl;
        return -1; // Invalid quantity
    } else if (productName == "Ranitidine" && quantity > PRODUCT_QUANTITY_RANITIDINE) {
        std::cout << "Only " << PRODUCT_QUANTITY_RANITIDINE << " units of Ranitidine available." << std::endl;
        return -1; // Invalid quantity
    }

    return quantity;
}

float calculateSubtotal(float price, int quantity) {
    return price * quantity;
}

float applyDiscountsOrPromotions(float price, int quantity, std::string productName) {
    if (quantity > 2) {
        float discountPerItem = 0.06 * price; // 6% discount rate
        float totalDiscount = discountPerItem * (quantity - 2);

        std::cout << "Discount applied for " << productName << ": Ksh " << totalDiscount << std::endl;

        return totalDiscount;
    }

    std::cout << "No discount applied for " << productName << "." << std::endl;
    return 0;
}

void selectPaymentMethod() {
    std::cout << "Payment Method: Cash" << std::endl;
}

void printReceipt(std::string productName, float subtotal, float total, float discount, int quantity) {
    std::cout << "----- Receipt -----" << std::endl;
    std::cout << "Product: " << productName << std::endl;
    std::cout << "Quantity: " << quantity << std::endl;
    std::cout << "Subtotal: Ksh " << subtotal << std::endl;

    if (discount > 0) {
        std::cout << "Discount (" << 6 << "%): Ksh " << discount << std::endl;
    }

    std::cout << "Total: Ksh " << total << std::endl;
    // Additional code to print other receipt details if needed
}

void updateInventory(std::string productName, int quantity) {
    if (productName == "Ibuprofen") {
        PRODUCT_QUANTITY_IBUPROFEN -= quantity;
    } else if (productName == "Ranitidine") {
        PRODUCT_QUANTITY_RANITIDINE -= quantity;
    }
}

void completeSale() {
    std::cout << "Sale completed!" << std::endl;
}

void displayOutOfStockMessage() {
    std::cout << "Product out of stock." << std::endl;
}

void restartOrExit() {
    // Code to restart or exit
}

int main() {
    inputCustomerDetails();

    std::string productName;
    std::cout << "Enter product name (Ibuprofen or Ranitidine): ";
    std::cin >> productName;

    if (checkProductAvailability(productName)) {
        int quantity = enterProductQuantity(productName);

        if (quantity != -1) {
            float price, subtotal, discount = 0;

            if (productName == "Ibuprofen") {
                price = IBUPROFEN_PRICE; // Use the price for Ibuprofen
            } else if (productName == "Ranitidine") {
                price = RANITIDINE_PRICE; // Use the price for Ranitidine
            }

            subtotal = calculateSubtotal(price, quantity);
            discount = applyDiscountsOrPromotions(price, quantity, productName);
            float total = subtotal - discount;

            selectPaymentMethod();
            printReceipt(productName, subtotal, total, discount, quantity);
            updateInventory(productName, quantity);
            completeSale();
        } else {
            restartOrExit();
        }
    } else {
        displayOutOfStockMessage();
        restartOrExit();
    }

    return 0;
}
