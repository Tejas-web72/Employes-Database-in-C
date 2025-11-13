#include <stdio.h>

#define SIZE 10

struct employee {
    char name[30];
    double basic, allowance, gross;
};

// Function to calculate gross salary
void calc_salary(struct employee *e) {
    e->gross = e->basic + e->allowance;
}

// Function to sort employees by gross salary (descending)
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
    struct employee employees[SIZE];
    int n;

    printf("Enter number of employees (max %d): ", SIZE);
    scanf("%d", &n);

    if (n > SIZE || n <= 0) {
        printf("Invalid number of employees!\n");
        return 1;
    }

    // Input employee details
    for (int i = 0; i < n; i++) {
        printf("\nEnter details of employee %d\n", i + 1);
        printf("Name: ");
        scanf("%s", employees[i].name);
        printf("Basic Salary: ");
        scanf("%lf", &employees[i].basic);
        printf("Allowance: ");
        scanf("%lf", &employees[i].allowance);

        calc_salary(&employees[i]);
    }

    // Sort employees by gross salary (descending)
    sort_salary(employees, n);

    // Display sorted salary details
    printf("\n-------------------------------------------------\n");
    printf(" No | Name           | Basic   | Allowance | Gross Salary\n");
    printf("-------------------------------------------------\n");
    for (int i = 0; i < n; i++) {
        printf("%3d | %-14s | %-7.2lf | %-9.2lf | %-12.2lf\n",
               i + 1,
               employees[i].name,
               employees[i].basic,
               employees[i].allowance,
               employees[i].gross);
    }
    printf("-------------------------------------------------\n");

    return 0;
}
