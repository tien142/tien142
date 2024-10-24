#include <stdio.h>
#include <string.h>
#include <ctype.h>
#define max 1000 
#define RESET   "\033[0m"
#define RED     "\033[31m"
#define GREEN   "\033[32m"
#define YELLOW  "\033[33m"
#define BLUE    "\033[34m"
#define MAGENTA "\033[35m"
#define CYAN    "\033[36m"
#define WHITE   "\033[37m"
#define BRIGHT_RED "\033[91m"
#define BRIGHT_GREEN "\033[92m"
#define BRIGHT_YELLOW "\033[93m"
#define BRIGHT_BLUE "\033[94m"
#define BRIGHT_MAGENTA "\033[95m"
#define BRIGHT_CYAN "\033[96m"
void nhap(char s[]){
	printf(GREEN"Nhap chuoi ky tu: "RESET);
    fgets(s, max, stdin);
    s[strlen(s)-1] = 0;
} 
// Bai 1: đếm khoảng trắng trong chuổi 
int dem_space(char s[]) {
    int dem = 0;
    for (int i = 0; i < strlen(s); i++)
        if (isspace(s[i]))
            dem++;
    return dem;
}

// Bai 2: kiểm tra đối xứng 
void str_reverse(char s[]) {
    /*
    int l = 0, r = strlen(s) - 1;
    while (l < r) {
        char t = s[l];
        s[l] = s[r];
        s[r] = t;
        l++; r--;
    }
    */
    int n = strlen(s);
    for (int i = 0; i < n/2; i++) {
        char t = s[i];
        s[i] = s[n-1-i];
        s[n-1-i] = t;
    }
}

// Bai 3: 
bool doi_xung(char s[]) {
    /*
    int l = 0, r = strlen(s)-1;
    while (l < r) {
        if (s[l] != s[r])
            return false;
        l++; r--;
    }
    */
   int n = strlen(s);
    for (int i = 0; i < n/2; i++)
        if (s[i] != s[n-1-i])
            return false;
    return true;
}

// Bai 4 - tuong duong ham strupr()
void in_hoa(char s[]) {
    for (int i = 0; i < strlen(s); i++)
        if (islower(s[i]))
            s[i] = toupper(s[i]);
}

// Bai 5 - tuong duong ham strlwr()
void in_thuong(char s[]) {
    for (int i = 0; i < strlen(s); i++)
        if (isupper(s[i]))
            s[i] = tolower(s[i]);
}

// Bai 6
void ten_rieng(char s[]) {
    s[0] = toupper(s[0]);
    for (int i = 1; i < strlen(s); i++) {
        s[i] = isspace(s[i-1]) ? toupper(s[i]) : tolower(s[i]);
    }
}

// Bai 7
void tach_ten(char s[], char ten[]) {
    char * t = strrchr(s, ' ');
    if (t != NULL)
        strcpy(ten, t+1);
    else  
        strcpy(ten, s);
}

// Bai 8
void tach_ho(char s[], char ho[]) {
    char * t = strrchr(s, ' ');
    if (t != NULL) {
        int l = t-s;
        strncpy(ho, s, l);
        ho[l] = 0;
    }
    else  
        strcpy(ho, s);
}
int main(){
	char s[max],ten[max],ho[max]; 
	int choice; 
	nhap(s);
	do{
		printf("------------Menu-------------\n"); 
		printf(BRIGHT_RED"1.Tim khoang trang trong chuoi da cho.\n"RESET);
		printf(BRIGHT_GREEN"2.Kiem tra chuoi da cho co doi xung khong.\n"RESET); 
		printf(BRIGHT_YELLOW"3.In ra dang in hoa cua chuoi,\n"RESET);
		printf(BRIGHT_BLUE"4.In ra dang in thuong cua chuoi.\n"RESET);
		printf(BRIGHT_MAGENTA"5.In ra ten rieng cua chuoi.\n"RESET);
		printf(BRIGHT_CYAN"6.Tach ten.\n"RESET);
		printf(WHITE "7.Tach ho.\n"RESET);
		printf(BLUE"8.Dao nguoc chuoi da nhap.\n"RESET); 
		printf(RED"0.Thoat!\n"RESET);
		scanf("%d", &choice);
		switch(choice){
			case 1:
				printf(RED"Chuoi da cho co %d khoang trang.\n"RESET, dem_space(s)); 
				break;
			case 2:
				printf(BLUE"Chuoi da cho la %s\n"RESET, doi_xung(s) ? RED "doi xung" RESET : GREEN "khong doi xung" RESET ); 
				break; 
			case 3:
				in_hoa(s);
				printf(RED "Dang in hoa : %s\n"RESET, s); 
				break;
			case 4:
				in_thuong(s);
				printf(BLUE "Dang in thuong: %s\n"RESET, s); 
				break;
			case 5:
				ten_rieng(s);
				printf(YELLOW"Dang ten rieng:  %s \n"RESET, s); 
				break;
			case 6:
				tach_ten(s, ten);
    			printf(CYAN"Phan ten:  %s\n"RESET, ten); 
				break;
			case 7:
				tach_ho(s, ho);
    			printf(MAGENTA"Phan ho: %s\n"RESET, ho); 
				break; 
			case 8:
				str_reverse(s);
    			printf(BLUE"Dao nguoc la: %s\n"RESET, s); 
				break; 
    		default:
				printf(RED"lua chon khong hop le\n"RESET); 
		} 
	}while(choice!=0);  
	return 0; 
} 
