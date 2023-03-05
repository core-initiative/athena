## I. Branching
Branch yang direkomendasikan ada dalam repositori

### 1. Branch `master`, atau  Branch `main`
Branch yang berisi source code production yang stabil. Hasil merge dari branch `devel`.
### 2. Branch `devel`
Branch yang berisi source code level pengembangan yang belum siap dirilis. Hasil merge dari branch-branch feature yang dibuat oleh tim developer.
### 3. Branch `issue`
Branch yang dibuat berdasarkan pengembangan fitur yang dilakukan oleh seorang developer. Branch ini dibuat dari branch `devel`. Setelah selesai pembuatan fitur, dari dilakukan Merge Pull Request ke branch `devel`. Penamaan yang disarankan dibuat berdasarkan nomor isue yang didefinisikan di project, seperti `issue-[NO_ISSUE]_[FEATURE-TITLE]`. Contoh `issue-140_login-endpoint-login-with-email-password`.
### 4. Branch `release` (opsional)
Branch dibuat setelah fitur-fitur dari rilis terkait selesai dan siap dirilis. Branch ini dibuat dari branch `devel`. Jika ada perbaikan bug dari rilis tertentu, dibuat berdasarkan branch `release` terkait. Setelah selesai akan dimerge kembali ke branch `devel` dan `master`.
### 5. Branch `hotfix` (opsional)
Branch yang dibuat untuk memperbaiki bug yang muncul di branch `release`. Branch ini dibuat dari branch `release` dan setelah selesai memperbaiki kode di branch `realease`, branch ini juga dimerge ke branch `devel` dan branch `master`/`main` 

Branch `release` dan `hotfix` menjadi Branch opsional sesuai dengan kebutuhan, jika rilis dari aplikasi tidak memiliki rencana rilis, maka cukup kode siap produksi berada di Branch `master` atau `main`.

## II. Panduan Workflow Git

- Project pada awal memndapatkan commit berupa boilerplate yang merupakan codebase generik dari project. Codebase ini akan dipush di branch `main` atau `master`. Branch ini akan menerima update kode dari branch `devel`, dan branch `hotfix` jika ada.
- Buat branch `devel` dari branch `main` atau `master` yang akan menampung kode dari project yang sudah dibangun, tapi belum siap memasuki environment produksi. 
- Jika ada fitur yang ingin dikembangkan, buat branch `issue` terkait. Setelah fitur selesai dikembangkan, buat Pull Request (PR) ke branch `develop`.

### Contoh Skenario
1. Misalkan fitur yang ingin dibangun adalah fitur login dengan Captcha. Issue github yang dibuat misalnya adalah issue nomor 140 dari repositori project terkait. Maka buat branch `issue-140_endpoint-login-with-email-password` dari branch `devel`.
```bash
$ git checkout devel
Switched to branch 'devel'
Your branch is up to date with 'origin/devel'

$ git checkout -b issue-140_login-with-captcha
Switched to a new branch 'issue-140_endpoint-login-with-email-password'
```
2. Lakukan pengembangan fitur dan jika sudah selesai, lakukan commit dan push ke branch `issue-140_endpoint-login-with-email-password`. Panduan commit dan commit message bisa dilihat di bagian III.
```bash
$ git commit -m "feat: add feature login with email and password"

$ git push 
```

3. Lakukan Pull Request (PR) dari branch `issue-140-endpoint-login-with-email-password` ke branch `devel`. Petunjuk untuk melakukan PR bisa dilihat di [sini](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request?tool=webui).

4. Dari Lead Programmer, atau programmer lain yang dimintakan untuk melakukan review, bisa memberikan komentar, feedback, atau perbaikan tambahan di antarmuka Github Web. Jika sudah dianggap selesai, maka bisa dilakukan merge dari PR terkait. Petunjuk untuk melakukan merge PR bisa dilihat di [sini](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/merging-a-pull-request).

5. Setelah reviewer melakukan merge PR, maka branch `feature` issue terkait bisa ditutup. Petunjuk untuk menghapus branch terkait bisa dilihat di [sini](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-branches-in-your-repository/deleting-and-restoring-branches-in-a-pull-request).

## III. Panduan Commit dan Commit Message

Commit dilakukan ketika ada perubahan yang cukup berarti dan tidak merusak jalannya program, ataupun unit test jika ada. Commit juga bisa dilakukan untuk melakukan pengelompokan perubahan di beberapa file yang secara logis memudahkan programmer lain untuk mengerti perubahan yang dilakukan.

Mengadopsi [Conventional Commits dari freecodecamp](https://www.freecodecamp.org/news/how-to-write-better-git-commit-messages/), berikut adalah panduan struktur message terkait commit messages yang direkomendasikan.

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]

```

- `type` yang bisa digunakan adalah:

    | Tipe 	| Deskripsi 	|
    |---	|---	|
    | `feat` 	| perubahan dalam commit mengandung fitur baru. 	|
    | `fix` 	| perubahan yang dilakukan adalah untuk bugfix. 	|
    | `chore` 	| perubahan yang dilakukan tidak membawa fitur baru, ataupun melakukan bugfixing. Contohnya adalah jika melakukan update dari dependecies. 	|
    | `refactor` 	| perubahan yang dilakukan dalam code adalah refactor yang tidak membawa fitur baru ataupun bugfix, misalnya mengoptimalkan alur ataupun algoritma   	|


- `optional scope` bisa diisi dengan module terkait, jika project yang dikembangkan merupakan project monolithic yang menampung kode baik dari backend maupun frontend. 

- `optional body` bisa diisi dengan detail dari perubahan yang dilakukan. 

- `optional footer(s)` bisa mengacu ke panduan Convention Commit di [sini](https://www.conventionalcommits.org/en/v1.0.0/).

Contoh dari pesan commit yang dibuat:
```
feat: Add function to check password complexity
```
```
feat: Add new parameter to return value of login endpoint

Refer to issue #140 
```

```
refactor: improve algorithm for checking password complexity
```

## IV. Panduan Pull Request

Idealnya setiap Pull Request memiliki satu pasangan terkait sebuah issue yang mencerminkan sebuah fitur yang dibangun. Hal ini memudahkan untuk modularitas dalam melakukan pengujian fitur terkait.

Sebaiknya Pull Message Request juga mengikuti panduan Commit Message di title dari issue, serta nomor dari issue terkait. Contohnya:
```
feat: add feature endpoint login with email and password #140
```