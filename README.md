#include <stdio.h>
#include <string.h>


struct employee {
    char name[30];
    float basic, allowance, gross;
};




void calc_salary(struct employee *e) {
    e->gross = e->basic + e->allowance;
}




void sort_salary(struct employee arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i].gross < arr[j].gross) {
                struct employee temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
    }
}


int main() {
    struct employee employees[10];
    int n;


    printf("Enter number of employees (max 10): ");
    if (scanf("%d", &n) != 1 || n <= 0 || n > 10) {
        printf("Invalid number of employees!\n");
        return 1;
    }


    getchar(); 


    
    for (int i = 0; i < n; i++) {
        printf("\nEnter details of employee %d\n", i + 1);


        printf("Name: ");
        fgets(employees[i].name, sizeof(employees[i].name), stdin);
        
        employees[i].name[strcspn(employees[i].name, "\n")] = 0;


        printf("Basic Salary: ");
        while (scanf("%f", &employees[i].basic) != 1) {
            printf("Invalid input. Enter a valid number: ");
            while (getchar() != '\n'); 
        }


        printf("Allowance: ");
        while (scanf("%f", &employees[i].allowance) != 1) {
            printf("Invalid input. Enter a valid number: ");
            while (getchar() != '\n'); 
        }


        getchar(); 
        calc_salary(&employees[i]);
    }


    
    sort_salary(employees, n);


    
    printf("\n-------------------------------------------------\n");
    printf(" No | Name           | Basic   | Allowance | Gross Salary\n");
    printf("-------------------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("%3d | %-14s | %-7.2f | %-9.2f | %-12.2f\n",
               i + 1,
               employees[i].name,
               employees[i].basic,
               employees[i].allowance,
               employees[i].gross);
    }
    printf("-------------------------------------------------\n");


    return 0;
}
