#include <stdio.h>


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
    int n;
    struct employee employees[10];


    printf("Enter number of employees (max 10): ");
    scanf("%d", &n);


    for (int i = 0; i < n; i++) {
        printf("\nEnter details of employee %d\n", i + 1);
        printf("Name: ");
        scanf("%s", employees[i].name);
        printf("Basic Salary: ");
        scanf("%f", &employees[i].basic);
        printf("Allowance: ");
        scanf("%f", &employees[i].allowance);


        calc_salary(&employees[i]);
    }


    sort_salary(employees, n);


    printf("\n---------------------------------------------\n");
    printf(" No | Name           | Basic   | Allowance | Gross Salary\n");
    printf("---------------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("%3d | %-14s | %-7.2f | %-9.2f | %-12.2f\n",
               i + 1,
               employees[i].name,
               employees[i].basic,
               employees[i].allowance,
               employees[i].gross);
    }
    printf("---------------------------------------------\n");


    return 0;
}

