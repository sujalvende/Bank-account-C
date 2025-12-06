#include<stdio.h>
#include<stdlib.h>
#include<string.h>

#define accountfile "account.dat"
#define tchar 50

typedef struct acoount_detalis{
    char name[tchar];
    int acc_no;
    float balance;
}acc_det;

int get_next_accno();
void create_acc();
void display_acc();
void search_acc();
void deposit_acc();
void withdraw_acc();
void update_acc();
void delete_acc();

int main(){
    
    int option;
    
    while(1){
        
        int i;
        
         printf("\n\n\n\n**********Straw Hat Bank**********\n\n\n");
        printf("1. Create New Account\n");
        printf("2. Display All Account\n");
        printf("3. Search Amount\n");
        printf("4. Deposit Money\n");
        printf("5. Withdraw Money\n");
        printf("6. Update Account\n");
        printf("7. Delete Account\n");
        printf("8. Exit\n");
        printf("\nEnter here (1-8) - ");
        if(scanf("%d",&option) != 1){
            printf("Invalid option try again.......");
        }
        getchar();
        if(option == 8){
            printf("\n\nYou are now successful exited...........");
            break; 
        }
        
        switch(option){
        
        case 1:
            create_acc();
            break;
        case 2:
            display_acc();
            break;
        case 3:
            search_acc();
            break;
        case 4:
            deposit_acc();
            break;
        case 5:
            withdraw_acc();
            break;
        case 6:
            update_acc();
            break;
        case 7:
            delete_acc();
            break;
        case 8:
            printf("\n\nGood Byy....\n");
            break;
        default:
            printf("\n\nInvalid option try again.............");
        }
        
        
    }
    
    
    
    return 0;
}

int get_next_accno(){
    FILE *facc;
    facc = fopen(accountfile,"rb");
    if(facc == NULL)
    return 1001;
    
    acc_det acc;
    int max = 1000;
    while(fread(&acc,sizeof(acc_det),1,facc) == 1){
        if(acc.acc_no > max)
            max = acc.acc_no;
    }
    fclose(facc);
    return max + 1;
}

void create_acc(){
    acc_det acc;
    acc.acc_no = get_next_accno();
    
    printf("\n---- Create Account ----\n");
    printf("Enter name - ");
    fgets(acc.name,50,stdin);
    acc.name[strcspn(acc.name,"\n")] = '\0';
    
    if(!acc.name){
        return;
    }
    
    printf("Enter initial deposit ammount - ");
    scanf("%f",&acc.balance);
    getchar();
    if(acc.balance < 0){
        printf("Invalid ammount. Account creation canceled.......");
    }
    
    FILE *facc = fopen(accountfile,"ab");
    if(facc == NULL){
        perror("Unable to open data file");
        return;
    }
    fwrite(&acc,sizeof(acc_det),1,facc);
    fclose(facc);
    printf("Account is created successfully............");
    printf("\n\nYour account number will be %d",acc.acc_no);
}

void display_acc(){
    FILE *facc;
    facc = fopen(accountfile,"rb");
    if(facc == NULL){
        printf("No record to found.........");
        return;
    }
    acc_det acc;
    printf("\n\n---- All Accounts ----\n\n");
    printf("%-10s %-25s %10s\n","Amount_No","Name","Balance");
    printf("\n-----------------------------------------------\n");
    int found = 0;
    while(fread(&acc,sizeof(acc_det),1,facc) == 1){
        printf("%-10d %-25s %10.2f\n",acc.acc_no,acc.name,acc.balance);
        found = 1;
    }
    if(found == 0){
        printf("No account to diplay.......");
    }
}

void search_acc(){
    int target;
    printf("Enter here account number - ");
    scanf("%d",&target);
    if(target < 1000){
        printf("Invalid input try again.......");
        return;
    }
    
    FILE *facc = fopen(accountfile, "rb");
    if(facc == NULL){
        printf("No account to be found.....");
        return;
    }
    
    acc_det acc;
    int found = 0;
    while(fread(&acc,sizeof(acc_det), 1,facc) == 1){
    if(acc.acc_no == target){
        printf("Account found:\n");
        printf("\nAccount_No = %d",acc.acc_no);
        printf("\nName = %s",acc.name);
        printf("\nBalance = %f\n",acc.balance);
        found = 1;
        break;
    }
    }
    if(found != 1){
        printf("There is no %d account number in bank. Try again......",target);
        
    }
    fclose(facc);
}

void deposit_acc(){
    int target;
    float amt;
    printf("Enter your account number - ");
    scanf("%d",&target);
    if(target < 1){
         printf("Invalid input try again......."); 
         return; 
    }
    printf("Enter here deposit ammount - ");
    scanf("%f",&amt);
    if(amt < 0){
        printf("Invalid ammount try again");
        return;    }
    
    acc_det acc;
    int found = 0;
    FILE *facc = fopen(accountfile, "rb+");
    if(facc == NULL){
        printf("No account to be found.......");
        return;
            }
    
    while(fread(&acc,sizeof(acc_det),1,facc) == 1){
        if(acc.acc_no == target){
            acc.balance = acc.balance + amt;
            fseek(facc,-((long)sizeof(acc_det)),SEEK_CUR);
            fwrite(&acc,sizeof(acc_det),1,facc);
            printf("Deposite ammount successfully.......");
            found = 1;
            }
    }
    
    if(found == 0){
        printf("No account of %d account number is found. Try again......",target);
    }
}

void withdraw_acc(){
    int target;
    float amt;
    printf("Enter your account number - ");
    if(scanf("%d",&target) != 1){
        printf("Invalid input....");
        return;
    }
    printf("Enter withdraw amount - ");
    if(scanf("%f",&amt) != 1){
        printf("Invalid amount tryagain......");
        return;
    }
    
    acc_det acc;
    int found = 0;
    FILE *facc = fopen(accountfile, "rb+");
    if(!facc){
        printf("No account to be found......");
        return;
    }
    
    while(fread(&acc,sizeof(acc_det), 1,facc) == 1){
        if(acc.acc_no == target){
            if(amt > acc.balance){
                printf("Insufficient balance in account.....");
            }
            else{
                acc.balance = acc.balance - amt;
                fseek(facc,-((long)sizeof(acc_det)),SEEK_CUR);
                fwrite(&acc,sizeof(acc_det), 1,facc);
                printf("Amount withdraw successfully.......");
                found = 1;
            }
        }
    }
    if(!found){
        printf("No account of %d account number is found...........",target);
    }
}

void update_acc(){
    int target;
    printf("Enter your account number - ");
    if(scanf("%d",&target) != 1){
        printf("Invalid input try again.......");
        return;
    }
    getchar();
    
    acc_det acc; 
    int found = 0;  
    FILE *facc = fopen(accountfile,"rb+");
    if(!facc){
        printf("No account to be found.......");
        return;
        }
    
    
    while(fread(&acc,sizeof(acc_det), 1,facc) == 1){
        if(acc.acc_no == target){
        printf("Current Name = %s\n",acc.name);
            printf("Enter new name - ");
            fgets(acc.name,50,stdin);
            acc.name[strcspn(acc.name,"\n")] = '\0';
            fseek(facc,-((long)sizeof(acc_det)), SEEK_CUR);
            fwrite(&acc,sizeof(acc_det), 1,facc);
            printf("Account details are updated sucessfully..........");
            found = 1;
        }
    }
    if(!found){
        printf("No account of %d account number is found.......",target);
    }
}

void delete_acc(){
    int target;
    printf("Enter your account number - ");
    if(scanf("%d",&target) != 1){
        printf("Invalid input try again.........");
        return;
    }
    
    FILE *facc = fopen(accountfile, "rb");
    if(!facc){
        printf("No account to be found..........");
        return;
    }
    
    FILE *tem = fopen("temp.dat","wb");
    if(!tem){
        fclose(facc);
        perror("Unable to create temporary file.....");
        return;
    }
    
    acc_det acc;
    int found = 0;
    while(fread(&acc,sizeof(acc_det), 1,facc) == 1){
        if(acc.acc_no == target){
            found = 1;
            continue;
            }
        fwrite(&acc,sizeof(acc_det), 1,tem);    
    }
    fclose(tem);
    fclose(facc);
    if(found){
        remove(accountfile);
        rename("temp.dat",accountfile);
        printf("Account of %s deleted successfully",acc.name);
        }
    else{
        remove("temp.dat");
        printf("No account of %d account number is found.........",target);
    }
}
    