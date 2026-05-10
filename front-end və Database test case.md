import os

# Define the content of the markdown file
markdown_content = """# Test Case Hesabatı (QA Testing)

Bu sənəd sistemin login, tətbiq yaradılması, silinməsi və çıxış funksionallıqlarının yoxlanılmasını əhatə edir.

---

## 1. Login funksionallığı (Valid Credentials)
**Description:** Qeydiyyatdan keçmiş email və şifrə ilə sistemə daxil olmaq.

* **Steps:**
    1. `Cebrayilov7703@gmail.com` emailini daxil et.
    2. `Tebriz373!` şifrəsini daxil et.
    3. ”Login” düyməsini sıx.
* **Expected Result:** İstifadəçi uğurla qeydiyyatdan keçməli və sistemə daxil olmalıdır.
* **Actual Result:** İstifadəçi sistemə uğurla daxil oldu.
* **Database Verification:**
    ```sql
    select * from profiles where first_name = 'Təbriz';
    ```
    *Nəticə:* Təbriz adlı istifadəçi profili tapıldı (ID: 7576e0a4-8e37-4a5b-964a-0f4765abfc0c).

---

## 2. Yalnış şifrə ilə daxil olmaq
**Description:** Səhv şifrə daxil edildikdə təhlükəsizliyin yoxlanılması.

* **Steps:**
    1. Login səhifəsinə daxil olmaq.
    2. Düzgün email daxil etmək (`Cebrayilov7703@gmail.com`).
    3. Yalnış şifrə yazıb “Login” sıxmaq.
* **Expected Result:** "Invalid credentials" xətası çıxmalıdır.
* **Actual Result:** Sistem girişə icazə vermədi və qırmızı rəngdə xəta mesajı göstərdi.
* **Database Verification:**
    ```sql
    select * from profiles where first_name = 'Təbriz';
    ```
    *Nəticə:* Profillər cədvəlində heç bir dəyişiklik baş vermədi. Giriş uğursuz oldu.

---

## 3. Dashboard-da yeni application yaratmaq
**Description:** Dashboard vasitəsilə yeni müraciət (Application) yaratmaq.

* **Steps:**
    1. Dashboard-da “New Application” düyməsini sıxmaq.
    2. Açılan pəncərədə sənəd növünü seçmək.
    3. Bütün məcburi xanaları doldurmaq.
    4. ”Approve for Payment” düyməsini sıxaraq müraciəti təsdiqləmək.
    5. Dashboard siyahısına qayıdıb yeni müraciəti tapmaq.
* **Expected Result:** Müraciət uğurla yaranmalı, Dashboard-da görünməli və statusu "pending" olmalıdır.
* **Actual Result:** Yeni application yarandı və statusu "pending" olaraq göstərildi.
* **Database Verification:**
    ```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```
    *Nəticə:* Applications cədvəlində yeni bir sətir yarandı və məlumatlar əks olundu.

---

## 4. Dashboard-da yalnış məlumat daxil etmək
**Description:** Formdakı xanalara uyğun olmayan simvollar daxil edərək validasiyanı yoxlamaq.

* **Steps:**
    1. “New Application” düyməsini sıxmaq.
    2. Ad və soyad xanalarına rəqəm daxil etmək.
    3. ”Pasport no” xanasına hərflər daxil etmək.
    4. Tarix xanasına gələcək tarix (məs: 2041) daxil etmək.
    5. ”Approve for Payment” düyməsini sıxmaq.
* **Expected Result:** Sistem məlumatları qəbul etməməli, “Yalnış format” xətası göstərməli və yeni application yaranmamalıdır.
* **Actual Result:** Sistem xəta verdi, yeni application yaranmadı.
* **Database Verification:**
    ```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```
    *Nəticə:* Database-də heç bir dəyişiklik baş vermədi.

---

## 5. History bölməsində müraciətin silinməsini yoxlamaq
**Description:** Silinmiş müraciətin "History" bölməsindən təmizləndiyini yoxlamaq.

* **Steps:**
    1. History bölməsində mövcud müraciəti qeyd etmək.
    2. “Delete” düyməsinə basmaq.
* **Expected Result:** History bölməsində silinmiş məlumat görünməməlidir.
* **Actual Result:** Məlumat bölmədən uğurla silindi.
* **Database Verification:**
    ```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```
    *Nəticə:* Supabase-də silinmiş məlumat tapılmadı.

---

## 6. Axtarış xanasına məntiqsiz simvollar daxil etmək
**Description:** Axtarış xanasına bazada olmayan və ya çox uzun simvollar daxil edildikdə sistemin davranışını yoxlamaq.

* **Steps:**
    1. Əsas səhifədən axtarış bölməsinə keçmək.
    2. Təsadüfi, məntiqsiz simvollar və ya çox uzun mətn yazmaq.
    3. ”Enter” düyməsini sıxmaq.
* **Expected Result:** Sistem tərəfindən məlumat tapılmadığına dair xəta və ya xəbərdarlıq mesajı çıxmalıdır.
* **Actual Result:** Heç bir məlumat tapılmadı, lakin sistem xəta mesajı vermədi (İnformasiya boş qaldı).
* **Database Verification:** Applications cədvəlində heç bir dəyişiklik baş vermədi.

---

## 7. Profildən çıxış etmək (Logout)
**Description:** İstifadəçinin sistemdən düzgün şəkildə çıxışının yoxlanılması.

* **Steps:**
    1. Sol menyuda “Logout” düyməsini sıxmaq.
    2. Çıxış prosesini gözləmək.
* **Expected Result:** İstifadəçi dərhal Login səhifəsinə yönləndirilməli.
* **Actual Result:** Profil sessiyası dayandırıldı və login səhifəsinə yönləndirmə baş tutdu.
* **Database Verification:**
    ```sql
    select * from profiles where first_name = 'Təbriz';
    ```
    *Nəticə:* Aktiv sessiya profili tapılmadı.
"""

file_path = "/mnt/data/test_case_report.md"
with open(file_path, "w", encoding="utf-8") as f:
    f.write(markdown_content)

print(file_path)
```bash
python ds_python_interpreter
