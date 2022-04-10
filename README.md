#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <string.h>

struct HoTen {
	char ho[20];
	char dem[20];
	char ten[20];
};
 
struct nguoi{
	struct HoTen hovaten;
    char gt[5];
    char dc[30];
    int sdt;
};

void menu();
void nhapHoTen(struct HoTen* ten); 
void nhap(nguoi &n);
void nhapN(nguoi a[], int n);
void xuat(nguoi n);
void xuatN(nguoi a[], int n);
void sapXepTheoTen(struct nguoi* ds, int sl);
void xuatFile(nguoi a[], int n, char fileName[]);
 
int main(){
    int key;
    char fileName[] = "DSLL.txt";
    int n;
    menu();
    bool daNhap = false;
    do{
        printf("Nhap so nguoi: "); scanf("%d", &n);
    }while(n <= 0);
    nguoi a[n];
    while(true){
        system("cls");
        menu();
        printf("\nNhap lua chon cua ban: ");
        scanf("%d",&key);
        switch(key){
            case 1:
                printf("\nBan da chon nhap DS lien lac!");
                nhapN(a, n);
                printf("\nBan da nhap thanh cong!");
                daNhap = true;
                printf("\nBam phim bat ky de tiep tuc!");
                getch();
                break;
            case 2:
                if(daNhap){
                    printf("\nBan da chon xuat DS lien lac!");
                    xuatN(a, n);
                }else{
                    printf("\nNhap DS lien lac truoc!!!!");
                }
                printf("\nBam phim bat ky de tiep tuc!");
                getch();
                break;
            case 3:
                if(daNhap){
                    printf("\nBan da chon sap xep theo ten!");
                    sapXepTheoTen(a, n);
                    xuatN(a, n);
                }else{
                    printf("\nNhap DS truoc!!!!");
                }
                printf("\nBam phim bat ky de tiep tuc!");
                getch();
                break;
            case 4:
                if(daNhap){
                    printf("\nBan da chon xuat DSLL!");
                    xuatFile(a, n, fileName);
                }else{
                    printf("\nNhap DS truoc!!!!");
                }
                printf("\nXuat DSLL thanh cong vao file %s!", fileName);
                printf("\nBam phim bat ky de tiep tuc!");
                getch();
                break;
            case 0:
                printf("\nBan da chon thoat chuong trinh!");
                getch();
                return 0;
            default:
                printf("\nKhong co chuc nang nay!");
                printf("\nBam phim bat ky de tiep tuc!");
                getch();
                break;
        }
    }
}
 
void menu(){
    printf("******************************************\n");
	printf("******************************************\n");
    printf("**    CHUONG TRINH QUAN LY DSLL   :)    **\n");
    printf("**      1. Nhap DS lien lac             **\n");
    printf("**      2. Hien thi danh sach lien lac  **\n");
    printf("**      3. Sap xep theo ten             **\n");
    printf("**      4. Xuat DS lien lac             **\n");//xuat ra file
	printf("**      0. Thoat                        **\n");
    printf("******************************************\n");
    printf("******************************************\n");
} 

void nhapHoTen(struct HoTen* ten) {
	printf("Ho: ");
	scanf("%s", ten->ho);
	printf("Dem: ");
	getchar();
	gets(ten->dem);
	printf("Ten: ");
	scanf("%s", ten->ten);
}
 
void nhap(nguoi &n){
    nhapHoTen(&n.hovaten);fflush(stdin);
    printf("Nhap gioi tinh: "); gets(n.gt);
    printf("Nhap dia chi: "); gets(n.dc);
    printf("Nhap so dien thoai: "); scanf("%d", &n.sdt);
}
 
void nhapN(nguoi a[], int n){
    for(int i = 0; i< n; ++i){
  	    printf("\n==============================");
        printf("\nNhap nguoi thu %d:\n", i+1);
        nhap(a[i]);
    }
}
 
void xuat(nguoi n){
	printf("\nHo ten : %s %s %s",n.hovaten.ho, n.hovaten.dem, n.hovaten.ten);
    printf("\nGioi tinh: %s", n.gt);
    printf("\nDia chi: %s", n.gt);
    printf("\nSo dien thoai: %d", n.sdt);
}
 
void xuatN(nguoi a[], int n){
    for(int i = 0;i < n;++i){
  	    printf("\n==============================");
        printf("\nThong tin nguoi thu %d:\n", i+1);
        xuat(a[i]);
    }
}

void sapXepTheoTen(struct nguoi* ds, int sl) {
	int i, j;
	for(i = 0; i < sl - 1; i++) {
		for(j = sl - 1; j > i; j --) {
			if(strcmp(ds[j].hovaten.ten, ds[j-1].hovaten.ten) < 0) {
				struct nguoi n = ds[j];
				ds[j] = ds[j - 1];
				ds[j - 1] = n;
			}
		}
	}
}
 
void xuatFile(nguoi a[], int n, char fileName[]){
    FILE * fp;
    fp = fopen (fileName,"w");
    fprintf(fp, "%20s%20s%20s%5s%30s%11s\n", "Ho","Dem","Ten","GT","Dia chi","SDT");
    for(int i = 0;i < n;i++){
        fprintf(fp, "%20s%20s%20s%5s%30s%11s\n", a[i].hovaten.ho,a[i].hovaten.dem,a[i].hovaten.ten, a[i].gt, a[i].dc, a[i].sdt);
    }
    fclose (fp);
}
