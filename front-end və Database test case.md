select * from profiles where first_name = 'Təbriz';
    ```

---

## 3. Dashboard-da application yaratmaq
**Təsvir:** Dashboard vasitəsilə yeni müraciət (Application) yaratmaq.

*   **Addımlar:**
    1. Dashboard-da “New Application” düyməsini sıxmaq.
    2. Açılan pəncərədə sənəd növünü seçmək.
    3. Bütün məcburi xanaları doldurmaq.
    4. ”Approve for Payment” düyməsini sıxaraq müraciəti təsdiqləmək.
    5. Dashboard siyahısına qayıdıb yeni müraciəti tapmaq.
*   **Gözlənilən Nəticə:** Müraciət uğurla yaranmalı, Dashboard siyahısında görünməli və statusu `pending` olmalıdır.
*   **Faktiki Nəticə:** Dashboard-da yeni application yarandı və statusu `pending` olaraq göstərildi.
*   **Verilənlər Bazası (Supabase SQL):** Applications cədvəlində yeni bir sətir yarandı.
    
```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```
    *ID:* `7576e0a4-8e37-4a5b-964a-0f4765abfc0c`

---

## 4. Dashboard-da application-a yalnış məlumat daxil etmək
**Təsvir:** Dashboard-da formdakı xanalara uyğun olmayan simvollar daxil etmək.

*   **Addımlar:**
    1. “New Application” düyməsini sıxmaq.
    2. Ad və soyad xanalarına rəqəm daxil etmək.
    3. ”Pasport no” xanasına hərflər daxil etmək.
    4. Tarix xanasına gələcək tarix (məs: 2041-ci il) daxil etmək.
    5. ”Approve for Payment” düyməsini sıxmaq.
*   **Gözlənilən Nəticə:** Sistem məlumatları qəbul etməməli, “Yalnış format” xətası göstərməli və yeni application yaranmamalıdır.
*   **Faktiki Nəticə:** Sistem xəta verdi, yeni application yaranmadı.
*   **Verilənlər Bazası (Supabase SQL):** `applications` cədvəlində heç bir dəyişiklik baş vermədi.
    
```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```

---

## 5. ”History” bölməsində müraciətin silindiyini yoxlamaq
**Təsvir:** Müraciət silindiyi halda məlumatların “History” bölməsindən də itdiyini yoxlamaq.

*   **Addımlar:**
    1. History bölməsində mövcud müraciəti qeyd etmək.
    2. “Delete” düyməsinə basmaq.
*   **Gözlənilən Nəticə:** History bölməsində silinmiş məlumat görünməməlidir.
*   **Faktiki Nəticə:** History bölməsindən məlumat silinmişdir.
*   **Verilənlər Bazası (Supabase SQL):**
    
```sql
    select * from applications where email = 'cebrayilov7703@gmail.com';
    ```

---

## 6. Axtarış xanasına məntiqsiz simvol daxil etmək
**Təsvir:** Axtarış xanasına məntiqsiz və çox uzun simvollar daxil edildikdə sistemin davranışı.

*   **Addımlar:**
    1. Əsas səhifədən axtarış butonuna click etmək.
    2. Bazada olmayan təsadüfi simvollar və ya çox uzun mətn yazmaq.
    3. ”Enter” düyməsinə click etmək.
*   **Gözlənilən Nəticə:** Sistem tərəfindən xəta mesajı və ya "Nəticə tapılmadı" bildirilməlidir.
*   **Faktiki Nəticə:** Heç bir məlumat tapılmadı, lakin sistem xəta mesajı vermədi.
*   **Verilənlər Bazası (Supabase SQL):** Cədvəllərdə heç bir dəyişiklik baş vermədi.

---

## 7. Profildən çıxış etmək
**Təsvir:** İstifadəçinin sistemdən düzgün şəkildə çıxışının yoxlanması.

*   **Addımlar:**
    1. Sol menyuda “Logout” düyməsini sıxmaq.
    2. Sistemdən çıxış mesajını gözləmək.
*   **Gözlənilən Nəticə:** İstifadəçi dərhal Login səhifəsinə yönləndirilməli.
*   **Faktiki Nəticə:** Profil (sessiya) silindi və login səhifəsinə yönləndirildi.
*   **Verilənlər Bazası (Supabase SQL):**
    
```sql
    select * from profiles where first_name = 'Təbriz';
    ```
    *Nəticə:* Təbriz adlı istifadəçi profili tapılmadı (və ya sessiya aktiv deyil).
