# Kullanma Kılavuzu: GitHub Otomatik Yükleme Programı

Bu Python programı, belirtilen bir klasörü izler ve bu klasörde yapılan değişiklikleri otomatik olarak bir GitHub deposuna yükler. Program, GitHub Personal Access Token kullanarak çalışır.

---

## Özellikler

- Belirtilen klasördeki **yeni dosyaları** GitHub'a yükler.
- Mevcut dosyalarda yapılan **düzenlemeleri** algılar ve günceller.
- Silinen dosyaları GitHub'dan kaldırır.
- Herhangi bir işlem olduğunda otomatik olarak commit ve push işlemi gerçekleştirir.

---

## Gereksinimler

1. **Python 3+** yüklü olmalı.
2. `watchdog` kütüphanesi kurulu olmalı:
   ```bash
   pip install watchdog
   ```
3. GitHub Personal Access Token oluşturulmuş olmalı.

---

## Kurulum Adımları

### 1. Personal Access Token Oluşturma
1. GitHub hesabınıza giriş yapın.
2. Profil resminize tıklayın ve **Settings > Developer settings > Personal access tokens** yolunu izleyin.
3. **Generate new token** seçeneğine tıklayın.
4. Şu izinleri seçin:
   - **repo**
   - **workflow**
5. Token'ı oluşturduktan sonra kopyalayın ve güvenli bir yerde saklayın.

---

### 2. Çevre Değişkeni Ayarlama

#### **Linux/macOS:**
1. Terminalde şu komutu çalıştırın:
   ```bash
   export GITHUB_TOKEN=ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   ```
2. Kalıcı yapmak için `~/.bashrc` veya `~/.zshrc` dosyasına şu satırı ekleyin:
   ```bash
   export GITHUB_TOKEN=ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   ```
3. Terminali yeniden başlatın veya şu komutu çalıştırın:
   ```bash
   source ~/.bashrc
   ```

#### **Windows:**
1. "Environment Variables" (Çevre Değişkenleri) ayarlarını açın.
2. **User variables** bölümünde yeni bir değişken oluşturun:
   - **Variable name**: `GITHUB_TOKEN`
   - **Variable value**: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`
3. Kaydedin ve bilgisayarınızı yeniden başlatın.

---

### 3. Programı Düzenleme

1. Aşağıdaki alanları dosya içinde düzenleyin:
   - **`LOCAL_FOLDER`**: İzlenecek klasörün tam yolu.
   - **`GITHUB_REPO_URL`**: GitHub depo URL'si. Örnek format:
     ```plaintext
     https://<kullanıcı_adı>:{os.getenv('GITHUB_TOKEN')}@github.com/<kullanıcı_adı>/<repo_adı>.git
     ```
   - **`BRANCH_NAME`**: Çalışılacak dal. Varsayılan: `main`.

---

### 4. Programı Çalıştırma

1. Programı terminalden şu komutla çalıştırın:
   ```bash
   python auto_push_to_github.py
   ```
2. Program çalışmaya başladığında, `LOCAL_FOLDER` içindeki tüm değişiklikler otomatik olarak GitHub'a yüklenir.

---

## Kullanım Örnekleri

### 1. Yeni Dosya Eklemek
- `LOCAL_FOLDER` içine yeni bir dosya ekleyin.
- Program dosyayı otomatik olarak GitHub deposuna yükleyecektir.

### 2. Mevcut Dosyayı Güncellemek
- `LOCAL_FOLDER` içindeki bir dosyayı düzenleyin.
- Program değişiklikleri algılar ve güncellenmiş dosyayı GitHub'a gönderir.

### 3. Dosya Silmek
- `LOCAL_FOLDER` içindeki bir dosyayı silin.
- Program silmeyi algılar ve GitHub deposundan da bu dosyayı kaldırır.

---

## Hata Ayıklama

### 1. Çevre Değişkeni Hatası
- Eğer token bulunamazsa, şu hatayı alırsınız:
  ```plaintext
  ValueError: GITHUB_TOKEN çevre değişkeni ayarlı değil.
  ```
- Çözüm: Çevre değişkenini doğru ayarladığınızdan emin olun.

### 2. Git Push Hatası
- Eğer `git push` sırasında hata alırsanız:
  - Token'ınızın doğru olduğundan emin olun.
  - GitHub depo URL'sini kontrol edin.

---

## Ekstra Bilgiler

- Programın sürekli çalışması için bir **terminal oturumu** açık olmalıdır.
- Büyük klasörlerde performans sorunları yaşanabilir. Gereksiz dosyaları `.gitignore` ile hariç tutabilirsiniz.

---

## Lisans

Bu yazılım MIT Lisansı ile lisanslanmıştır.
