#include<stdio.h>      pointer
#include<math.h>

int main() {
    float a[10], *ptr, mean, std, sum = 0, sumstd = 0;
    int n, i;
    
    printf("Enter the number of elements\n");
    scanf("%d", &n);
    printf("Enter the array elements\n");
    
    for (i = 0; i < n; i++) {
        scanf("%f", &a[i]);
    }
    
    ptr = a;
    for (i = 0; i < n; i++) {
        sum = sum + *ptr;
        ptr++;
    }
    
    mean = sum / n;
    ptr = a;
    
    for (i = 0; i < n; i++) {
        sumstd = sumstd + pow((*ptr - mean), 2);
        ptr++;
    }
    
    std = sqrt(sumstd / n);
    
    printf("Sum=%.3f\t", sum);
    printf("Mean=%.3f\t", mean);
    printf("Standard deviation=%.3f\t", std);
    
    return 0;
}



string
#include<stdio.h>
#include<string.h>

int Length(char s1[]);
int compare(char s1[], char s2[]);
void concat(char s1[], char s2[]);

int main() {
    char s1[200], s2[100];
    int len, res;

    printf("\n Enter the String s1: ");
    gets(s1);
    printf("\n Enter the String s2: ");
    gets(s2);

    len = Length(s1);
    printf("\n Length of the String s1 is: %d", len);

    len = Length(s2);
    printf("\n Length of the String s2 is: %d", len);

    res = compare(s1, s2);
    if (res == 0)
        printf("\n Both the Strings are Equal \n");
    else
        printf("\n The Strings are not Equivalent \n");

    concat(s1, s2);
    printf("\n Concatenated string is: %s", s1);

    return 0;
}

int Length(char s1[]) {
    int len = 0;
    while (s1[len] != '\0')
        len++;
    return len;
}

int compare(char s1[], char s2[]) {
    int count = 0;
    while (s1[count] == s2[count]) {
        if (s1[count] == '\0' || s2[count] == '\0')
            break;
        count++;
    }
    if (s1[count] == '\0' && s2[count] == '\0')
        return 0;
    else
        return -1;
}

void concat(char s1[], char s2[]) {
    int i, j;
    i = strlen(s1);
    for (j = 0; s2[j] != '\0'; i++, j++)
        s1[i] = s2[j];
    s1[i] = '\0';
}



bubble

#include<stdio.h>

int main() {
    int n, i, j, a[10], temp;
    printf("Enter number of array elements (max 10): \n");
    scanf("%d", &n);

    if (n <= 0 || n > 10) {
        printf("Invalid number of elements. Please enter a number between 1 and 10.\n");
        return 1;
    }

    printf("Enter the array elements: \n");
    for (i = 0; i < n; i++) {
        scanf("%d", &a[i]);
    }

    printf("The original elements are: \n");
    for (i = 0; i < n; i++) {
        printf("%d\t", a[i]);
    }

    for (i = 0; i < n - 1; i++) {
        for (j = 0; j < n - i - 1; j++) {
            if (a[j] > a[j + 1]) {
                temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
            }
        }
    }

    printf("\nThe sorted elements are: \n");
    for (i = 0; i < n; i++) {
        printf("%d\t", a[i]);
    }

    return 0;
}




dbs
#include <stdio.h>
#include <string.h>

#define MAX_RECORDS 100
#define NAME_LEN 50
#define EMAIL_LEN 50

typedef struct {
    int id;
    char name[NAME_LEN];
    char email[EMAIL_LEN];
} Record;

Record table[MAX_RECORDS];
int record_count = 0;

void create_record(int id, char name[], char email[]) {
    if (record_count >= MAX_RECORDS) {
        printf("Database full.\n");
        return;
    }
    for (int i = 0; i < record_count; i++) {
        if (table[i].id == id) {
            printf("ID %d exists.\n", id);
            return;
        }
    }
    table[record_count] = (Record){id, "", ""};
    strncpy(table[record_count ].name, name, NAME_LEN);
    strncpy(table[record_count ].email, email, EMAIL_LEN);
    printf("Record %d created.\n", id);
    record_count++;
}

void read_record(int id) {
    for (int i = 0; i < record_count; i++) {
        if (table[i].id == id) {
            printf("ID: %d, Name: %s, Email: %s\n", id, table[i].name, table[i].email);
            return;
        }
    }
    printf("ID %d not found.\n", id);
}

void update_record(int id, char name[], char email[]) {
    for (int i = 0; i < record_count; i++) {
        if (table[i].id == id) {
            strncpy(table[i].name, name, NAME_LEN);
            strncpy(table[i].email, email, EMAIL_LEN);
            printf("ID %d updated.\n", id);
            return;
        }
    }
    printf("ID %d not found.\n", id);
}

void delete_record(int id) {
    for (int i = 0; i < record_count; i++) {
        if (table[i].id == id) {
            table[i] = table[--record_count];
            printf("Record %d deleted.\n", id);
            return;
        }
    }
    printf("ID %d not found.\n", id);
}

void show_records() {
    if (record_count == 0) {
        printf("No records.\n");
        return;
    }
    for (int i = 0; i < record_count; i++)
        printf("ID: %d, Name: %s, Email: %s\n", table[i].id, table[i].name, table[i].email);
}

int main() {
    int choice, id;
    char name[NAME_LEN], email[EMAIL_LEN];

    while (1) {
        printf("\n1.Create 2.Read 3.Update 4.Delete 5.Show 6.Exit\nChoice: ");
        scanf("%d", &choice);
        if (choice == 6) break;

        if (choice == 1 || choice == 3) {
            printf("ID: "); scanf("%d", &id);
            printf("Name: "); scanf("%s", name);
            printf("Email: "); scanf("%s", email);
        } else if (choice != 5) {
            printf("ID: "); scanf("%d", &id);
        }

        switch (choice) {
            case 1: create_record(id, name, email); break;
            case 2: read_record(id); break;
            case 3: update_record(id, name, email); break;
            case 4: delete_record(id); break;
            case 5: show_records(); break;
            default: printf("Invalid choice.\n");
        }
    }
    printf("Exiting...\n");
    return 0;
}






calender

#include <stdio.h>
#include <string.h>

#define MAX_EVENTS 100

typedef struct {
    int day, month, year;
    char name[50];
    char reminder[50];
} event;

event calendar[MAX_EVENTS];
int ecount = 0;

void addevent() {
    if (ecount >= MAX_EVENTS) {
        printf("Calendar is full.\n");
        return;
    }
    printf("Enter event name: ");
    scanf("%s", calendar[ecount].name);
    printf("Enter date (DD MM YYYY): ");
    scanf("%d %d %d", &calendar[ecount].day, &calendar[ecount].month, &calendar[ecount].year);
    strcpy(calendar[ecount].reminder, "");
    ecount++;
    printf("Event added.\n");
}

void viewevent() {
    if (ecount == 0) {
        printf("No events scheduled.\n");
        return;
    }
    for (int i = 0; i < ecount; i++) {
        printf("%d/%d/%d - %s\n", calendar[i].day, calendar[i].month, calendar[i].year, calendar[i].name);
    }
}

void setreminder() {
    char ename[50];
    printf("Enter event name: ");
    scanf("%s", ename);
    for (int i = 0; i < ecount; i++) {
        if (strcmp(calendar[i].name, ename) == 0) {
            printf("Enter reminder: ");
            scanf(" %[^\n]", calendar[i].reminder);
            printf("Reminder set.\n");
            return;
        }
    }
    printf("Event not found.\n");
}

void viewreminder() {
    int found = 0;
    for (int i = 0; i < ecount; i++) {
        if (strlen(calendar[i].reminder) > 0) {
            printf("%d/%d/%d - %s: %s\n", calendar[i].day, calendar[i].month, calendar[i].year, calendar[i].name, calendar[i].reminder);
            found = 1;
        }
    }
    if (!found) printf("No reminders set.\n");
}

int main() {
    int choice;
    do {
        printf("\n1. Add Event\n2. View Events\n3. Set Reminder\n4. View Reminders\n5. Exit\nEnter choice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1: addevent(); break;
            case 2: viewevent(); break;
            case 3: setreminder(); break;
            case 4: viewreminder(); break;
            case 5: printf("Exiting...\n"); break;
            default: printf("Invalid choice.\n");
        }
    } while (choice != 5);
    return 0;
}

