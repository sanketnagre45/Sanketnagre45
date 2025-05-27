#include <stdio.h>
#include<string.h>
#define MAX 5
struct Transaction 
{
    char type[10];
    float amount;
};

int main() {
    int pin = 1234, enteredPin;
    float balance = 1000.0, deposit, withdraw;
    int option;
    struct Transaction history[MAX];
    int count = 0;
    
    printf("===============================\n");
    printf("***** Welcome to the ATM ******\n");
    printf("==============================\n");
    printf("\n");
    printf("Enter your 4 digit PIN: ");
    scanf("%d", &enteredPin);

    if (enteredPin != pin) 
    {
        printf("Incorrect PIN Access denied.\n");
        return 0;
    }
    do {
        
        printf("======================\n");
        printf("\n ****ATM Menu **** \n");
        printf("=======================\n");
        printf("\n");
        printf("1. Check Balance\n");
        printf("2. Deposit Money\n");
        printf("3. Withdraw Money\n");
        printf("4. Change PIN\n");
        printf("5. Mini Statement\n");
        printf("6. Exit\n");
        printf("Choose option: ");
        scanf("%d", &option);
        if (option == 1) 
        {
            printf("Your balance is: ₹%f\n", balance);
        }
        else if (option == 2) 
        {
            printf("Enter deposit amount: ");
            scanf("%f",&deposit);

            if (deposit > 0) 
            {
                balance+=deposit;
                printf("Deposited. New balance: ₹%f\n", balance);

                if (count < MAX) 
                {
                    strcpy(history[count].type, "Deposit");
                    history[count].amount = deposit;
                    count++;
                } else 
                {
                    for(int i=1; i<MAX;i++) 
                    {
                    history[i-1] = history[i];
                    }
                    strcpy(history[MAX-1].type,"Deposit");
                    history[MAX-1].amount = deposit;
                }
            }else
            {
                printf("Invalid amount.\n");
            }
        }

        else if (option==3) 
        {
            printf("Enter withdraw amount: ");
            scanf("%f", &withdraw);

            if (withdraw > 0 && withdraw <= balance)
            {
                balance -= withdraw;
                printf("Withdrawn. New balance: ₹%.2f\n", balance);

                if (count < MAX)
                {
                    strcpy(history[count].type, "Withdraw");
                    history[count].amount = withdraw;
                    count++;
                } else {
                    for (int i =1; i<MAX;i++) 
                    {
                       history[i-1]=history[i];
                    }
                    strcpy(history[MAX-1].type, "Withdraw");
                    history[MAX-1].amount = withdraw;
                }
            } else 
            {
                printf("Invalid or not enough balance.\n");
            }
        }
        else if (option == 4) {
            printf("Enter new PIN: ");
            scanf("%d", &pin);
            printf("PIN changed.\n");
        }
        else if (option == 5) {
            printf("**** Mini Statement ****\n");
            if (count == 0) 
            {
                printf("No transactions yet.\n");
            } else {
                for (int i = 0; i < count; i++) 
                {
                printf("%d.%s ₹%.2f\n",i+1, history[i].type, history[i].amount);
                }
                }
                }
        else if (option==6) 
        {
            printf("Thank you for using the ATM\n");
            printf("=====================================\n");
            
            printf("HAVE A NICE DAY\n");
            printf("============================\n");
        }
        else 
        {
            printf("Invalid option Try again.\n");
        }
    } while (option != 6);
    
    return 0;
}
