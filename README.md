[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-c66648af7eb3fe8bc4f294546bfd86ef473780cde1dea487d3c4ff354943c9ae.svg)](https://classroom.github.com/online_ide?assignment_repo_id=7850026&assignment_repo_type=AssignmentRepo)
# Norma Spring Boot Final Project

![money transfer](money_transfer.jpg)

Bu bitirme projesi kapsamında bootcamp katılımcılarının bir online bankacılık sisteminin backend servislerini yazmaları 
beklenmektedir. Proje kapsamında beklenen minimum fonksiyonlar ve teknik ihtiyaçlar aşağıda listelenmiştir.

Bitirme projesi bireysel olarak implemente edilecek birbiriyle aynı olan projeler başarısız sayılacaktır. Bunun yanında
yardımlaşma, fikir alışverişi herzamanki gibi desteklenmektedir :) 

## Beklenen fonksiyonlar
* Müşteri yönetimi
* Hesap yönetimi
* Kart yönetimi
* Transfer yönetimi

### Müşteri yönetimi
Yaratılacak API'lar aracılığıyla; müşteri yaratma, güncelleme ve silme işlemleri mümkün olacaktır. Silme işlemi hesaplarında
parası bulunan yada kredi kartı borcu bulunan müşteriler için mümkün olmayacak.

### Hesap yönetimi
Banka müşterilerinin yatırımlarını kontrol etmek amacıyla kullanabilmeleri için hesap yaratmalarına, silmelerine API'lar
aracılığıyla izin verilecektir. Kullanıcılar iki farkılı türde hesap açabilecek, vadesiz mevduat hesabı ve birikim hesabı.
İki hesap arası para transferi yapılabilecek, vadesiz mevduat hesabı başka hesaplara para transferi için kullanılabilecekken
birikim hesabından doğrudan para transferi yapılamayacak. Hesaplar TL, Euro yada Dolar para birimlerinde açılabilecek.

### Kart yönetimi
Müşterilere banka tarafından bankamatiklerde yada alışverişte kullanılmak üzere ön ödemeli banka kartı ve kredi kartları
sunulmaktadır. Bu kartların yaratılması, müşteri ve hesapla ilişkilendirilmesi, kart kullanarak para transferi (alışveriş) 
fonksiyonları API'lar aracılığıyla sağlanacaktır.

Ayrıca kredi kartları için; borç sorgulama, hesaptan borç ödeme, bankamatikten borç ödeme, ekstre görüntüleme (JSON formatında) 
işlemleri yine API aracılığı ile yapılabilecek.

### Transfer yönetimi
Müşterilerin para transferlerini yönetmek için uygun API'lar sağlanmalıdır. Bir müşteri farklı para birimlerinde açılan 
hesaplar arası transfer yapmak isterse güncel para kuru https://api.exchangeratesapi.io/latest?base=TRY API'dan 
alınmalı ve dönüşüm yapılıp transfer öyle gerçekleştirilemeli. Transfer işlemleri sadece IBAN üzerinden gerçekleştirilebilecek.

## Teknik beklentiler
Yukarda belirtilen tüm operasyonlar tamamı Java ve Spring Boot  kullanılarak implemente edilecektir, proje genelinde
bootcamp boyunca öğrendiğimiz OOP prensipleri doğru şekilde uygulanmalıdır. 

Tüm fonksiyonlar REST API'lar aracılığı ile yerine getirilmeli ve API'lar swagger arayüzü ile dökümantasyonu yapılmalıdır.
Hata durumları uygun şekilde ele alınmalı ve hatalara uygun responselar üretilmeli.

Uygulama genelinde Spring Boot, Spring Rest ve JPA kullanılmalı, clean code ve SOLID prensiplerine uyulmalı, unit testler 
eklenmelidir.




# OnlineBankingApp
Norma Java Spring Bootcamp Final Project [codesandbox](https://codesandbox.io/s/github/172-Norma-Java-Spring-Bootcamp/final-project-zeynepsl/tree/main/online-banking/src/main/java/patika/bootcamp/onlinebanking?file=/OnlineBankingApplication.java)

# Account

## POST
- request:
  - 
 ``` 
 {
  "accountType": "CHECKING_ACCOUNT",
  "branchId": 1,
  "currencyId": 1,
  "customerId": 122
}
```
- response:
  - 
``` 
{
  "id": 16,
  "accountNumber": "1619871010537",
  "accountBalance": 0,
  "bankCode": "23232",
  "iban": "TR702323201619871010537",
  "blockedAt": null,
  "canBeActiveAt": null,
  "accountStatus": "PASSIVE",
  "accountType": "CHECKING_ACCOUNT",
  "currencyId": 1,
  "customerId": 122,
  "branchId": 1
}
```
- If the customer creates a checking account for the first time, a bank card is created
  - 
``` 
{
    "id": 2,
    "customerResponseDto": {
      "id": 122,
      "firstName": "sevde",
      "lastName": "salman",
      "email": "sevde@salman.com",
      "phoneNumber": "+901111111111",
      "secondaryEmail": "sevde@hotmail.com",
      "secondaryPhoneNumber": "+902222222222",
      "customerNumber": "987101",
      "age": 32,
      "birthDate": "1990-06-05",
      "gender": "FEMALE",
      "active": false,
      "confirmedByAdmin": true
    },
    "accountResponseDto": {
      "id": 16,
      "accountNumber": "1619871014066",
      "accountBalance": 0,
      "bankCode": "23232",
      "iban": "TR702323201619871014066",
      "blockedAt": null,
      "canBeActiveAt": null,
      "accountStatus": "PASSIVE",
      "accountType": "CHECKING_ACCOUNT",
      "currencyId": 1,
      "customerId": 122,
      "branchId": 1
    },
    "cardNumber": "1611619871014066",
    "isActive": true
  }
```
# Credit Card
## POST
- request:
  - 
``` 
{
  "bankBranchId": 1,
  "cardLimit": 7000,
  "customerId": 122,
  "password": "123456"
}
```
- response:
  - 
```
{
  "id": 25,
  "cardNumber": "1611619871014066",
  "isActive": true,
  "customerResponseDto": {
    "id": 122,
    "firstName": "sevde",
    "lastName": "salman",
    "email": "sevde@salman.com",
    "phoneNumber": "+901111111111",
    "secondaryEmail": "sevde@hotmail.com",
    "secondaryPhoneNumber": "+902222222222",
    "customerNumber": "987101",
    "age": 32,
    "birthDate": "1990-06-05",
    "gender": "FEMALE",
    "active": false,
    "confirmedByAdmin": true
  },
  "bankBranchResponseDto": {
    "id": 1,
    "branchName": "fatih sultan mehmet bulvari subesi",
    "branchCode": "161",
    "bankBranchAddressResponseDto": {
      "country": "turkiye",
      "city": "bursa",
      "district": "nilufer",
      "neighborhood": "fethiye"
    }
  },
  "cardLimit": 7000,
  "availableLimit": 7000,
  "periodExpenditures": 0,
  "accountCutOffDate": null,
  "paymentDueDate": null,
  "amountOfDebt": 0,
  "cvv": "123"
}
```

- online money transfer request:
  - 
 ``` 
 {
  "amount": 10,
  "cardNo": "1611619871014066",
  "cvv": "123",
  "dueDate": "2022-06-06T08:00:40.503Z",
  "firstName": "sevde",
  "lastName": "salman",
  "toAccountNumber": "1618643790510"
}
 ```
 - response:
   - 
 ```
 {
  "id": 2,
  "senderCustomerNUmber": "987101",
  "recipientIbanNo": "TR702323201618643790510",
  "transactionDate": "2022-06-06T08:04:23.105+00:00",
  "useAllBalance": false,
  "amount": 10,
  "modeOfPayment": "KrediKartiIleOdeme"
}
 ```
# Prepaid Card
## POST
- request:
  - 
```
{
  "customerId": 122,
  "password": "onodemekarti"
}
```

- response:
  - 
```
{
  "id": 18,
  "cardNumber": "1611619871014066",
  "isActive": true,
  "accountBalance": 0,
  "customerResponseDto": {
    "id": 122,
    "firstName": "sevde",
    "lastName": "salman",
    "email": "sevde@salman.com",
    "phoneNumber": "+901111111111",
    "secondaryEmail": "sevde@hotmail.com",
    "secondaryPhoneNumber": "+902222222222",
    "customerNumber": "987101",
    "age": 32,
    "birthDate": "1990-06-05",
    "gender": "FEMALE",
    "active": false,
    "confirmedByAdmin": true
  },
  "minBalance": 300,
  "maxBalance": 1000
}
```

# Transaction
## POST
- request:
  - 
```
{
  "amount": 10,
  "modeOfPayment": "IsyeriKirasi",
  "recipientIbanNo": "TR702323201616789318788",
  "senderIbanNo": "TR702323201618643790510",
  "useAllBalance": false
}
```
- response:
  - 
```
{
  "id": 3,
  "senderIbanNo": "TR702323201618643790510",
  "senderAccount": {
    "id": 12,
    "accountNumber": "1618643790510",
    "accountBalance": 160,
    "bankCode": "23232",
    "iban": "TR702323201618643790510",
    "blockedAt": null,
    "canBeActiveAt": null,
    "accountStatus": "PASSIVE",
    "accountType": "CHECKING_ACCOUNT",
    "currencyId": 1,
    "customerId": 72,
    "branchId": 1
  },
  "senderCustomerNUmber": "864379",
  "recipientIbanNo": "TR702323201616789318788",
  "transactionDate": "2022-06-06T08:31:46.164+00:00",
  "useAllBalance": false,
  "amount": 10,
  "modeOfPayment": "IsyeriKirasi"
}
```

