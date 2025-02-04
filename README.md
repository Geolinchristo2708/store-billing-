#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define product names and prices
char *productName[] = {
    "sugar", "milk", "vegetable masala", "washing powder", "salt", "poha", "oil",
    "tooth paste", "hair conditionar", "wheat flour", "red chilli", "maida", "coffee",
    "tea", "butter", "milk powder", "turmeric powder", "hair oil", "ghee", "face powder"
};
char product_name[20][20]; // Increased array size from 19 to 20
int product_quantity[20];

int count1 = 0, total_bill = 0, total_bill1 = 0, discount;

int sugar_p = 50, milk_p = 50, vegetable_masala_p = 50, washing_powder_p = 100, 
    salt_p = 20, poha_p = 50, oil_p = 200, tooth_paste_p = 40, hair_conditionar_p = 120, 
    wheat_flour_p = 50, red_chilli_p = 40, maida_p = 45, coffee_p = 200, tea_p = 100, 
    butter_p = 100, milk_powder_p = 150, turmeric_powder_p = 200, hair_oil_p = 60, 
    ghee_p = 300, face_powder_p = 70;

void generate_bill() {
    printf("\n\t  * AKSHAY GROCERY STORE BILL *\n");
    printf("|----------------------------------------------------\n");
    printf("| Product\t\tQuantity\t\tPrice |\n");
    for (int i = 0; i < count1; i++) {
        int price = 0;
        if (strcmp(product_name[i], "sugar") == 0) price = sugar_p;
        else if (strcmp(product_name[i], "milk") == 0) price = milk_p;
        else if (strcmp(product_name[i], "vegetable masala") == 0) price = vegetable_masala_p;
        else if (strcmp(product_name[i], "washing powder") == 0) price = washing_powder_p;
        else if (strcmp(product_name[i], "salt") == 0) price = salt_p;
        else if (strcmp(product_name[i], "poha") == 0) price = poha_p;
        else if (strcmp(product_name[i], "oil") == 0) price = oil_p;
        else if (strcmp(product_name[i], "tooth paste") == 0) price = tooth_paste_p;
        else if (strcmp(product_name[i], "hair conditionar") == 0) price = hair_conditionar_p;
        else if (strcmp(product_name[i], "wheat flour") == 0) price = wheat_flour_p;
        else if (strcmp(product_name[i], "red chilli") == 0) price = red_chilli_p;
        else if (strcmp(product_name[i], "maida") == 0) price = maida_p;
        else if (strcmp(product_name[i], "coffee") == 0) price = coffee_p;
        else if (strcmp(product_name[i], "tea") == 0) price = tea_p;
        else if (strcmp(product_name[i], "butter") == 0) price = butter_p;
        else if (strcmp(product_name[i], "milk powder") == 0) price = milk_powder_p;
        else if (strcmp(product_name[i], "turmeric powder") == 0) price = turmeric_powder_p;
        else if (strcmp(product_name[i], "hair oil") == 0) price = hair_oil_p;
        else if (strcmp(product_name[i], "ghee") == 0) price = ghee_p;
        else if (strcmp(product_name[i], "face powder") == 0) price = face_powder_p;

        printf("| %-18s\t%d\t\t%d \n", product_name[i], product_quantity[i], price * product_quantity[i]);
        printf("|----------------------------------------------------\n");
    }

    printf("| Total products: %d \tTotal amount: %d \n", count1, total_bill1);
    printf("| Discount: %d\n", discount);
    printf("| Payable amount: %d\n", total_bill);
    printf("|----------------------------------------------------\n");
}

void calculate_bill() {
    total_bill = 0;
    for (int i = 0; i < count1; i++) {
        int price = 0;
        for (int j = 0; j < 20; j++) {
            if (strcmp(product_name[i], productName[j]) == 0) {
                price = ((int[]){sugar_p, milk_p, vegetable_masala_p, washing_powder_p, salt_p, poha_p, oil_p, tooth_paste_p, hair_conditionar_p, wheat_flour_p, red_chilli_p, maida_p, coffee_p, tea_p, butter_p, milk_powder_p, turmeric_powder_p, hair_oil_p, ghee_p, face_powder_p})[j];
                break;
            }
        }
        total_bill += price * product_quantity[i];
    }

    total_bill1 = total_bill;
    if (total_bill >= 15000) discount = (15 * total_bill) / 100;
    else if (total_bill >= 10000) discount = (10 * total_bill) / 100;
    else if (total_bill >= 5000) discount = (5 * total_bill) / 100;
    else discount = 0;

    total_bill -= discount;
    generate_bill();
}

int main() {
    char temp_str[20];
    int check, count;

    printf("\n\n *WELCOME TO AKSHAY GROCERY STORE* \n \n");
    printf("Discount Rates:\n");
    printf(" - Below ₹5000: No discount\n");
    printf(" - ₹5000-₹9999: 5%% discount\n");
    printf(" - ₹10000-₹14999: 10%% discount\n");
    printf(" - Above ₹15000: 15%% discount\n\n");

    while (count1 < 20) {
        printf("Enter product name: ");
        fgets(temp_str, sizeof(temp_str), stdin);
        strtok(temp_str, "\n");

        int found = 0;
        for (int j = 0; j < 20; j++) {
            if (strcmp(temp_str, productName[j]) == 0) {
                strcpy(product_name[count1], temp_str);
                found = 1;
                break;
            }
        }
        if (!found) {
            printf("Invalid product name. Try again.\n");
            continue;
        }

        printf("Enter quantity: ");
        scanf("%d", &product_quantity[count1]);
        while ((getchar()) != '\n');

        count1++;
        printf("More items? (Y/N): ");
        char ch = getchar();
        while ((getchar()) != '\n');
        if (ch == 'Y' || ch == 'y') continue;
        else break;
    }

    calculate_bill();
    return 0;
}
