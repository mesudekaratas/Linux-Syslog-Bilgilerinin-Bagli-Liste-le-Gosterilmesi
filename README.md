# Linux Syslog Bilgilerinin Bagli Liste ile Gosterilmesi
veri yapıları ve algoritmalar dersi ödevi 22.02.25
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Node {
    char log[256];
    struct Node* next;
} Node;

Node* yeniDugum(char* log) {
    Node* yeni = (Node*)malloc(sizeof(Node));
    strcpy(yeni->log, log);
    yeni->next = NULL;
    return yeni;
}
void ekle(Node** bas, char* log) {
    Node* yeni = yeniDugum(log);
    if (*bas == NULL) {
        *bas = yeni;
        return;
    }
    Node* temp = *bas;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = yeni;
}
void yazdir(Node* bas) {
    while (bas != NULL) {
        printf("%s\n", bas->log);
        bas = bas->next;
    }
}

void temizle(Node* bas) {
    Node* temp;
    while (bas != NULL) {
        temp = bas;
        bas = bas->next;
        free(temp);
    }
}

int main() {
    Node* bas = NULL;

    ekle(&bas, "Sistem baslatildi.");
    ekle(&bas, "Kullanici giris yapti.");
    ekle(&bas, "Hata: Yetkisiz erisim girisimi.");

    printf("Syslog Kayitlari:\n");
    yazdir(bas);

    temizle(bas);
    return 0;
}

