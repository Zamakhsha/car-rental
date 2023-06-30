#include <stdio.h>
#include <stdlib.h>
#include <conio.h>
#include <windows.h>
#include <string.h>

COORD coord = {0,0};

void gotoxy(int x,int y)
{
    coord.X = x;
    coord.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),coord);
}

void displayReceipt(const char nama[],int no_kp,const char no_plat[], const char kereta[], int masa, const char sewa[], const char pulang[], float harga, float totalAmount)
{
	printf("\n");
	printf("\n");
	printf("\n=====================================");
    printf("---- Resit ----\n");
    printf("Nama Penyewa: %s\n", nama);
    printf("Nombor Kad Pengenalan Penyewa: %d\n", no_kp);
    printf("Nombor Plat Kereta: %s\n", no_plat);
    printf("Model Kereta: %s\n", kereta);
    printf("Masa (Jam): %.2f\n", masa);
    printf("Tarikh Mula Sewaan: %s\n", sewa);
    printf("Tarikh Pulangan Kereta: %s\n", pulang);
    printf("Harga per Hari: RM%.2f\n", harga);
    printf("Jumlah Bayaran: RM%.2f\n", totalAmount);
    printf("\n=====================================");
    printf("Terima kasih kerana menyewa kereta dengan kami!\n");
}

typedef struct {
    char brand[50];
    char model[50];
    char plateNumber[20];
    char colour[20];
    double fuelTankSize;
    double dailyRate;
} Car;

void displayCarDetails(Car cars[], int numCars, int startIndex) {
    for (int i = startIndex; i < startIndex + numCars; i++) {
        printf("%d. %s\n", i + 1, cars[i].model);
        printf("- Plate Number: %s\n", cars[i].plateNumber);
        printf("- Color: %s\n", cars[i].colour);
        printf("- Fuel Tank Size: %.1f L\n", cars[i].fuelTankSize);
        printf("- Daily Rate: RM %.2f\n\n", cars[i].dailyRate);
    }
}

int main()
{
    FILE *fp, *ft;
    char another, choice;

    struct emp
    {
        char no_plat[10];
        char kereta[20];
        int masa;
        char sewa[10];
        char pulang[10];
        char nama[40];
        int no_kp;
        float harga;
        float totalAmount;
    };

    struct emp e;

    char empno_plat[10];

    long int recsize;

    fp = fopen("EMP.DAT","rb+");
    if(fp == NULL)
    {
        fp = fopen("EMP.DAT","wb+");
        if(fp == NULL)
        {
            printf("Cannot open file");
            exit(1);
        }
    }

    recsize = sizeof(e);

    Car cars[27];

    // SUV
    strcpy(cars[0].brand, "Honda");
    strcpy(cars[0].model, "BR-V");
    strcpy(cars[0].plateNumber, "VCJ 4850");
    strcpy(cars[0].colour, "PUTIH");
    cars[0].fuelTankSize = 42.0;
    cars[0].dailyRate = 174.00;
    
        strcpy(cars[1].brand, "Honda");
    strcpy(cars[1].model, "BR-V");
    strcpy(cars[1].plateNumber, "VCE 4140");
    strcpy(cars[1].colour, "PUTIH");
    cars[1].fuelTankSize = 42.0;
    cars[1].dailyRate = 174.00;

    strcpy(cars[2].brand, "Honda");
    strcpy(cars[2].model, "BR-V");
    strcpy(cars[2].plateNumber, "VCH 160");
    strcpy(cars[2].colour, "MERAH");
    cars[2].fuelTankSize = 42.0;
    cars[2].dailyRate = 174.00;

    strcpy(cars[3].brand, "Perodua");
    strcpy(cars[3].model, "Ativa");
    strcpy(cars[3].plateNumber, "VJA 4471");
    strcpy(cars[3].colour, "SILVER");
    cars[3].fuelTankSize = 36.0;
    cars[3].dailyRate = 193.00;

    strcpy(cars[4].brand, "Perodua");
    strcpy(cars[4].model, "Ativa");
    strcpy(cars[4].plateNumber, "VAM 2931");
    strcpy(cars[4].colour, "BIRU");
    cars[4].fuelTankSize = 36.0;
    cars[4].dailyRate = 193.00;

    strcpy(cars[5].brand, "Perodua");
    strcpy(cars[5].model, "Ativa");
    strcpy(cars[5].plateNumber, "VCX 2754");
    strcpy(cars[5].colour, "MERAH");
    cars[5].fuelTankSize = 36.0;
    cars[5].dailyRate = 193.00;

    strcpy(cars[6].brand, "Proton");
    strcpy(cars[6].model, "X50");
    strcpy(cars[6].plateNumber, "VJD 8971");
    strcpy(cars[6].colour, "MERAH");
    cars[6].fuelTankSize = 45.0;
    cars[6].dailyRate = 230.00;

    strcpy(cars[7].brand, "Proton");
    strcpy(cars[7].model, "X50");
    strcpy(cars[7].plateNumber, "VCP 6432");
    strcpy(cars[7].colour, "MERAH");
    cars[7].fuelTankSize = 45.0;
    cars[7].dailyRate = 230.00;

    strcpy(cars[8].brand, "Proton");
    strcpy(cars[8].model, "X50");
    strcpy(cars[8].plateNumber, "VCD 1412");
    strcpy(cars[8].colour, "PUTIH");
    cars[8].fuelTankSize = 45.0;
    cars[8].dailyRate = 230.00;

    // MPV
    strcpy(cars[9].brand, "Toyota");
    strcpy(cars[9].model, "Innova");
    strcpy(cars[9].plateNumber, "VAU 2263");
    strcpy(cars[9].colour, "SILVER");
    cars[9].fuelTankSize = 55.0;
    cars[9].dailyRate = 246.00;

    strcpy(cars[10].brand, "Toyota");
    strcpy(cars[10].model, "Innova");
    strcpy(cars[10].plateNumber, "VCW 2228");
    strcpy(cars[10].colour, "SILVER");
    cars[10].fuelTankSize = 55.0;
    cars[10].dailyRate = 246.00;

    strcpy(cars[11].brand, "Toyota");
    strcpy(cars[11].model, "Innova");
    strcpy(cars[11].plateNumber, "VBE 8233");
    strcpy(cars[11].colour, "HITAM");
    cars[11].fuelTankSize = 55.0;
    cars[11].dailyRate = 246.00;

    strcpy(cars[12].brand, "Perodua");
    strcpy(cars[12].model, "Alza");
    strcpy(cars[12].plateNumber, "VBM 8732");
    strcpy(cars[12].colour, "PUTIH");
    cars[12].fuelTankSize = 42.0;
    cars[12].dailyRate = 138.00;

    strcpy(cars[13].brand, "Perodua");
    strcpy(cars[13].model, "Alza");
    strcpy(cars[13].plateNumber, "VBM 8769");
    strcpy(cars[13].colour, "BIRU");
    cars[13].fuelTankSize = 42.0;
    cars[13].dailyRate = 138.00;

    strcpy(cars[14].brand, "Perodua");
    strcpy(cars[14].model, "Alza");
    strcpy(cars[14].plateNumber, "VBM 8746");
    strcpy(cars[14].colour, "PUTIH");
    cars[14].fuelTankSize = 42.0;
    cars[14].dailyRate = 138.00;

    strcpy(cars[15].brand, "Volkswagen");
    strcpy(cars[15].model, "Tiguan Allspace");
    strcpy(cars[15].plateNumber, "VHH 7846");
    strcpy(cars[15].colour, "PUTIH");
    cars[15].fuelTankSize = 60.0;
    cars[15].dailyRate = 376.00;

    strcpy(cars[16].brand, "Volkswagen");
    strcpy(cars[16].model, "Tiguan Allspace");
    strcpy(cars[16].plateNumber, "VEK 7685");
    strcpy(cars[16].colour, "HITAM");
    cars[16].fuelTankSize = 60.0;
    cars[16].dailyRate = 376.00;

    strcpy(cars[17].brand, "Volkswagen");
    strcpy(cars[17].model, "Tiguan Allspace");
    strcpy(cars[17].plateNumber, "VJN 4547");
    strcpy(cars[17].colour, "HITAM");
    cars[17].fuelTankSize = 60.0;
    cars[17].dailyRate = 376.00;

    // Economic
    strcpy(cars[18].brand, "Perodua");
    strcpy(cars[18].model, "Axia");
    strcpy(cars[18].plateNumber, "VCK 5181");
    strcpy(cars[18].colour, "SILVER");
    cars[18].fuelTankSize = 33.0;
    cars[18].dailyRate = 112.00;

    strcpy(cars[19].brand, "Perodua");
    strcpy(cars[19].model, "Axia");
    strcpy(cars[19].plateNumber, "VCH 2905");
    strcpy(cars[19].colour, "DARK BLUE");
    cars[19].fuelTankSize = 33.0;
    cars[19].dailyRate = 112.00;

    strcpy(cars[20].brand, "Perodua");
    strcpy(cars[20].model, "Axia");
    strcpy(cars[20].plateNumber, "VAT 7195");
    strcpy(cars[20].colour, "MERAH");
    cars[20].fuelTankSize = 33.0;
    cars[20].dailyRate = 112.00;

    strcpy(cars[21].brand, "Perodua");
    strcpy(cars[21].model, "Bezza");
    strcpy(cars[21].plateNumber, "VDB 8571");
    strcpy(cars[21].colour, "ROSE GOLD");
    cars[21].fuelTankSize = 36.0;
    cars[21].dailyRate = 139.00;

    strcpy(cars[22].brand, "Perodua");
    strcpy(cars[22].model, "Bezza");
    strcpy(cars[22].plateNumber, "VCN 2429");
    strcpy(cars[22].colour, "MAROON");
    cars[22].fuelTankSize = 36.0;
    cars[22].dailyRate = 139.00;

    strcpy(cars[23].brand, "Perodua");
    strcpy(cars[23].model, "Bezza");
    strcpy(cars[23].plateNumber, "VCX 4313");
    strcpy(cars[23].colour, "COFFEE");
    cars[23].fuelTankSize = 36.0;
    cars[23].dailyRate = 139.00;

    strcpy(cars[24].brand, "Perodua");
    strcpy(cars[24].model, "Myvi");
    strcpy(cars[24].plateNumber, "VCK 2025");
    strcpy(cars[24].colour, "PUTIH");
    cars[24].fuelTankSize = 36.0;
    cars[24].dailyRate = 138.00;

    strcpy(cars[25].brand, "Perodua");
    strcpy(cars[25].model, "Myvi");
    strcpy(cars[25].plateNumber, "VG 706");
    strcpy(cars[25].colour, "HITAM");
    cars[25].fuelTankSize = 36.0;
    cars[25].dailyRate = 138.00;

    strcpy(cars[26].brand, "Perodua");
    strcpy(cars[26].model, "Myvi");
    strcpy(cars[26].plateNumber, "VAU 2662");
    strcpy(cars[26].colour, "MERAH");
    cars[26].fuelTankSize = 36.0;
    cars[26].dailyRate = 138.00;

    while(1)
    {
		system("cls");
        gotoxy(25,7);
        printf("SELAMAT DATANG KE SUPERB CAR RENTAL");
        gotoxy(35,10);
        printf("1. ADD RECORD");
        gotoxy(35,12);
        printf("2. LIST RECORDS");
        gotoxy(35,14);
        printf("3. MODIFY RECORD");
        gotoxy(35,16);
        printf("4. DELETE RECORD");
        gotoxy(35,18);
        printf("5. CHOOSE CAR");
        gotoxy(35,22);
        printf("YOUR CHOICE ");
        fflush(stdin);
        choice  = getche();
        switch(choice)
    {
            case '1':
            	system("cls");
                fseek(fp,0,SEEK_END);
                another = 'Y';
                while(another == 'Y' || another == 'y')
                {
                	printf("\n");
                	printf("\n");
                	printf("\nEnter Renter's Name: ");
                    fflush(stdin);
                    gets(e.nama);
                    printf("\nEnter Renter's IC Number: ");
                    scanf("%d",&e.no_kp);
                    printf("\nEnter Plate Number: ");
                    scanf("%s",e.no_plat);
                    printf("\nEnter Car Model: ");
                    fflush(stdin);
                    gets(e.kereta);
                    printf("\nEnter Rental Duration (day): ");
                    scanf("%f",&e.masa);
                    printf("\nEnter Rental Start Date (DD/MM/YYYY): ");
                    fflush(stdin);
                    gets(e.sewa);
                    printf("\nEnter Car Return Date (DD/MM/YYYY): ");
                    fflush(stdin);
                    gets(e.pulang);
                    printf("\nEnter Price per Day: ");
                    scanf("%f",&e.harga);
                    
                    float totalAmount = e.masa * e.harga; // Perhitungan total amount

                    fwrite(&e,recsize,1,fp);
                    
                    displayReceipt(e.nama, e.no_kp, e.no_plat, e.kereta, e.masa, e.sewa, e.pulang, e.harga, totalAmount); // Memaparkan resit

                    printf("\nAdd Another Record (Y/N): ");
                    fflush(stdin);
                    another = getche();
                }
                break;
            case '2':
                system("cls");
                rewind(fp);
                while(fread(&e,recsize,1,fp)==1)
                {
                	printf("\n=====================================");
                	printf("\nNama Penyewa: %s",e.nama);
                	printf("\nNombor Kad Pengenalan Penyewa: %d",e.no_kp);
                    printf("\nNombor Plat Kereta: %s",e.no_plat);
                    printf("\nModel Kereta: %s",e.kereta);
                    printf("\nMasa (Jam): %.2f",e.masa);
                    printf("\nTarikh Mula Sewaan: %s",e.sewa);
                    printf("\nTarikh Pulangan Kereta: %s",e.pulang);
                    printf("\nHarga per Hari: RM%.2f",e.harga);
                    printf("\n=====================================");
                    
                }
                	printf("\nBACK<<< (Y/N): ");
                    fflush(stdin);
                    another = getche();
                break;
            case '3':
                system("cls");
                another = 'Y';
                while(another == 'Y' || another == 'y')
                {
                    printf("Enter the Plate Number of the car to modify: ");
                    scanf("%s", empno_plat);
                    rewind(fp);
                    while(fread(&e,recsize,1,fp)==1)
                    {
                        if(strcmp(e.no_plat,empno_plat) == 0)
                        {
                        	printf("\nEnter New Renter's Name: ");
                            fflush(stdin);
                            gets(e.nama);
                            printf("\nEnter New Renter's IC Number: ");
                            scanf("%d",&e.no_kp);
                            printf("\nEnter New Plate Number: ");
                            scanf("%s",e.no_plat);
                            printf("\nEnter New Car Model: ");
                            fflush(stdin);
                            gets(e.kereta);
                            printf("\nEnter New Rental Duration (Day): ");
                            scanf("%f",&e.masa);
                            printf("\nEnter New Rental Start Date (DD/MM/YYYY): ");
                            fflush(stdin);
                            gets(e.sewa);
                            printf("\nEnter New Car Return Date (DD/MM/YYYY): ");
                            fflush(stdin);
                            gets(e.pulang);
                            printf("\nEnter Price per Day: ");
                            scanf("%f",&e.harga);

                            fseek(fp,-recsize,SEEK_CUR);
                            fwrite(&e,recsize,1,fp);
                            break;
                        }
                    }
                    printf("\nModify Another Record (Y/N): ");
                    fflush(stdin);
                    another = getche();
                }
                break;
            case '4':
                system("cls");
                another = 'Y';
                while(another == 'Y' || another == 'y')
                {
                    printf("\nEnter the Plate Number of the car to delete: ");
                    scanf("%s",empno_plat);
                    ft = fopen("temp.dat","wb");
                    rewind(fp);
                    while(fread(&e,recsize,1,fp) == 1)
                    {
                        if(strcmp(e.no_plat,empno_plat) != 0)
                        {
                            fwrite(&e,recsize,1,ft);
                        }
                    }
                    fclose(fp);
                    fclose(ft);
                    remove("rental.dat");
                    rename("temp.dat","rental.dat");

                    fp = fopen("rental.dat","rb+");
                    printf("\nDelete Another Record (Y/N): ");
                    fflush(stdin);
                    another = getche();
                }
                break;

            case '5':
                system("cls");
                another = 'Y';
                while(another == 'Y' || another == 'y')
                {
                    int choice;
    int startIndex;

    printf("Selamat datang ke Superb Car Rental!\n");
    printf("1. SUV\n");
    printf("2. MPV\n");
    printf("3. Ekonomi\n");
    printf("Sila pilih jenis kereta anda: ");
    scanf("%d", &choice);

    switch (choice) {
        case 1:
            printf("Pilihan SUV:\n");
            printf("1. Honda\n");
            printf("2. Perodua\n");
            printf("3. Proton\n");
            printf("Sila pilih jenama SUV anda: ");
            scanf("%d", &choice);

            switch (choice) {
                case 1:
                    printf("SUV - Honda\n");
                    startIndex = 0;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 2:
                    printf("SUV - Perodua\n");
                    startIndex = 3;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 3:
                    printf("SUV - Proton\n");
                    startIndex = 6;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                default:
                    printf("Pilihan tidak sah.\n");
            }
            break;
        case 2:
            printf("Pilihan MPV:\n");
            printf("1. Toyota\n");
            printf("2. Perodua\n");
            printf("3. Volkswagen\n");
            printf("Sila pilih jenama MPV anda: ");
            scanf("%d", &choice);

            switch (choice) {
                case 1:
                    printf("MPV - Toyota\n");
                    startIndex = 9;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 2:
                    printf("MPV - Perodua\n");
                    startIndex = 12;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 3:
                    printf("MPV - Volkswagen\n");
                    startIndex = 15;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                default:
                    printf("Pilihan tidak sah.\n");
            }
            break;
        case 3:
            printf("Pilihan Ekonomi:\n");
            printf("1. Perodua - Axia\n");
            printf("2. Perodua - Bezza\n");
            printf("3. Perodua - Myvi\n");
            printf("Sila pilih jenama Ekonomi anda: ");
            scanf("%d", &choice);

            switch (choice) {
                case 1:
                    printf("Ekonomi - Perodua Axia\n");
                    startIndex = 18;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 2:
                    printf("Ekonomi - Perodua Bezza\n");
                    startIndex = 21;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                case 3:
                    printf("Ekonomi - Perodua Myvi\n");
                    startIndex = 24;
                    displayCarDetails(cars, 3, startIndex);
                    break;
                default:
                    printf("Pilihan tidak sah.\n");
            }
            		printf("\nFOUND YOUR BEST CAR!(Y/N):");
                    fflush(stdin);
                    another = getche();


                break;

                        }
                    }
                }
            }
    }
