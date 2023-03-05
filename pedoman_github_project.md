## I. Panduan Pembuatan Issue
### 1. Penamaan
Issue dalam Github merepresentasikan satu buah task dalam sprint yang terkait dari sebuah project. Konvensi penamaan Issue bisa mengikuti petunjuk
```
[Optional Module] [Type] Task Title/Short Description
```

- `Optional Module` biasa terkait dengan service yang terdefinisi dalam satu repositori. 
- `Type` biasa terbagi menjadi sebagai berikut:

    | Type 	| Deskripsi 	|
    |---	|---	|
    | `API` atau `BE` 	| Task fitur yang dikembangkan terkait Backend atau API 	|
    | `FE` 	| Task fitur yang dikembangkan adalah Frontend 	|
    | `KA` 	| Task yang dilakukan adalah Knowledge Aqcuisition. Biasanya task yang muncul adalah support untuk menggali pengetahuan lebih lanjut untuk menyelesaikan task fitur. 	|
    | `TW` 	| Task yang dilakukan adalah Technical Work. Biasanya task yang dikategorikan dalam tipe ini adalah task support yang membantu secara teknis menyelesaikan task fitur. 	|
    | `DOCS`| Task yang didefinisikan untuk menyimpan beberapa dokumen atau catatan pendukung terkait task tertentu. Task jenis ini biasa muncul juga untuk menampung hasil task berjenis `KA` 	|
    | `QA` 	| Task yang dilakukan adalah terkait pengujian. Scope dari task ini bisa sesuai dengan scope fitur, atau bisa menjadi satu kesatuan, yang berupa workflow yang terdiri dari beberapa fitur. |

- `Task Title/Short Description` bisa dibuat menjadi `[Optional SubModule Name]: [Detail of task]`. SubModule Name biasanya merepresentasikan satu buah langkah yang memiliki detail dari bagian selanjutnya.   

Berikut contoh penamaan issue berdasarkan panduan:

```
[Authentication] [API] Login: Endpoint Login with Username & Password
```
```
[Authentication] [API] Login: Endpoint Login with Magic Link
```
```
[KA] Login: Research about implementation OAuth Login with Google
```

```
[TW] Update SSL of Staging Server
```

### 2. Detail Task
Detail dari task diharapkan memberikan tiga hal, yaitu:
1. Deskripsi singkat terkait fitur yang ingin dikembangkan.
2. Informasi yang tersedia terkait fitur, seperti design/mockup/wireframe, API Endpoint Spesification, ataupun Database Table yang digunakan.
3. Output yang ingin dihasilkan dari fitur, atau Definition of Done, baik itu adalah halaman web berdasarkan design, file atau report yang dihasilkan, ataupun API endpoint yang dibutuhkan.

Tiga elemen di atas hanya merupakan panduan, dari penerapannya bisa kurang, bisa juga lebih. Yang diharapkan adalah detail dari task berisi sebanyak mungkin info yang dibutuhkan developer untuk menyelesaikan tasknya.

Berikut adalah contoh-contoh Detail Task 

```
[Authentication] [API] Login: Endpoint Login with Username & Password

RestAPI Endpoint Login with username, and password, and return the access_token that needed to access the rest of system. 

Database table:
- check the username and password to user table.
- if successfully login, create the entry of session in the user_session table.

Endpoint URL: /auth/login

Request Body:
{
    "username": "johndoe@mail.com",
    "password": "KS12ke>!" 
}

Response Body Success:
{
    "code": 200,
    "message": "successfully logged in",
    "data": {
        "access_token": "DwOwsK4VYFhqPdVWWZqyezxtyUEKMAUI",
        "refresh_token": "jiHC6uPsQqUxkWTk0vgoCpPf7R8nfneB",
        "expiry_in": 6000,
        "session_id": "0813fd185a8aebae67525887bcbb5a7d8d60c74cc88badc1f5b47b5004c9b46fd1e1f74e99904b52b06b949fd3a62b6d"
    }
}

Response Body Error
{
    "code": 500,
    "message": "Failed to Login"
}

```

```
[Backoffice] [FE] Login: Create Page Login

Design of the web: [mockup or design. image or url]

Message Error Copywriting List: [url to [DOCS] issue] 

The output page has to be accesible by URL of [main-url]/app/login
```

```
[KA] Research about Oauth Sign in with Google

Do a feasibility study of implementing OAuth Login with "Sign in witth Google" button, implemented with VueJS and Golang.

Reference to start with: 
- https://medium.com/@bnprashanth256/oauth2-with-google-account-gmail-in-go-golang-1372c237d25e
- https://developers.google.com/identity/sign-in/web/sign-in
- https://codevoweb.com/google-oauth-authentication-with-vue-mongodb-and-golang/



```
## II. Panduan Kanban Board
Pembagian tipe kolom yang ada dalam Kanban project 
| Tipe 	| Deksripsi 	| Aktor 	|
|---	|---	|---	|
| Backlog 	| Berisi issue yang telah teridentifikasi, tapi mungkin belum didetailkan atau belum akan diimplementasikan dalam sprint berjalan.  	| Lead Programmer, System Analyst, atau Scrum Master 	|
| Ready 	| Berisi issue yang telah didetailkan dan diassign ke developer, dan siap diimplementasikan dalam sprint berjalan. 	| Lead Programmer, System Analyst (jika ada), atau Scrum Master 	|
| In Progress 	| Berisi issue yang mulai atau sedang dikerjakan oleh assignee 	| Assigned Programmer 	|
| Complete 	| Berisi issue yang telah selesai dibuat, dan dilakukan pengujian awal oleh asignee 	| Assigned Programmer 	|
| In Review 	| Berisi issue yang sedang dalam Review 	| Lead Programmer, QA Engineer 	|
| Done 	| Berisi issue yang telah selesai direview dan dianggap mencapai Definition of Done 	| Lead Programmer, QA Engineer 	|
| Documentation 	| Berisi issue yang mengandung dokumentasi yang diperlukan terkait issue. Berisi issue dengan type [DOCS] 	| Assignee 	|

