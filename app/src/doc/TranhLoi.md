# 📋 CHECKLIST TRÁNH LỖI KHI PHÁT TRIỂN ANDROID APP

## 🎯 **CÁC FILE QUAN TRỌNG CẦN KIỂM TRA THEO THỨ TỰ**

### 1. **🔧 build.gradle.kts (Module: app)**

```kotlin
// ✅ KIỂM TRA TRƯỚC KHI CODE:
android {
    namespace = "com.example.tenproject"  // ← PHẢI KHỚP với package name
    compileSdk = 34

    defaultConfig {
        applicationId = "com.example.tenproject"  // ← PHẢI KHỚP với namespace
        // ...
    }
}
```

**❌ LỖI THƯỜNG GẶP:**

- Namespace không khớp với package name trong Java
- ApplicationId khác với namespace

### 2. **📱 AndroidManifest.xml**

```xml
<!-- ✅ TEMPLATE AN TOÀN: -->
<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <application
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar"  <!-- ← Theme an toàn -->
        android:label="@string/app_name">

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!-- Các Activity khác -->
        <activity
            android:name=".ResultActivity"
            android:parentActivityName=".MainActivity"/>
    </application>
</manifest>
```

**❌ LỖI THƯỜNG GẶP:**

- Theme không tồn tại (như `@style/Theme.MyApplication`)
- Quên đăng ký Activity mới
- Sai tên Activity

### 3. **🎨 Layout XML Files**

```xml
<!-- ✅ TEMPLATE AN TOÀN cho activity_main.xml: -->
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/editTextA"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Nhập hệ số a"
        android:inputType="numberDecimal|numberSigned" />

    <!-- Các view khác... -->

</LinearLayout>
```

**❌ LỖI THƯỜNG GẶP:**

- Thiếu dấu `=` trong attributes
- Sử dụng `white` thay vì `#ffffff`
- ID trùng lặp
- Thiếu closing tags

### 4. **☕ Activity Java Files**

```java
// ✅ TEMPLATE AN TOÀN:
package com.example.tenproject;  // ← PHẢI KHỚP với thư mục

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.EditText;
import android.widget.Button;
// ← CHỈ import những gì cần thiết

public class MainActivity extends AppCompatActivity {

    // ✅ Khai báo biến UI
    private EditText editTextA, editTextB, editTextC;
    private Button buttonSolve, buttonClear;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // ✅ Initialize UI components
        initializeUI();
        setupEventListeners();
    }

    private void initializeUI() {
        editTextA = findViewById(R.id.editTextA);
        // ...
    }

    private void setupEventListeners() {
        buttonSolve.setOnClickListener(v -> solveEquation());
        // ...
    }
}
```

**❌ LỖI THƯỜNG GẶP:**

- Import sai: `import android.app.AppComponentFactory;`
- Package name không khớp với thư mục
- Quên `findViewById()` hoặc sai ID
- Logic phức tạp trong `onCreate()`

### 5. **📝 strings.xml**

```xml
<!-- ✅ file: app/src/main/res/values/strings.xml -->
<resources>
    <string name="app_name">Tên App Của Bạn</string>
    <string name="solve_button">Giải</string>
    <string name="clear_button">Xóa</string>
    <!-- Định nghĩa tất cả strings ở đây -->
</resources>
```

---

## 🚀 **QUY TRÌNH PHÁT TRIỂN AN TOÀN**

### **BƯỚC 1: SETUP PROJECT**

```bash
1. Tạo project với package name rõ ràng
2. Kiểm tra build.gradle.kts (namespace = applicationId)
3. Build ngay sau khi tạo project → phải thành công
```

### **BƯỚC 2: TẠO LAYOUT**

```bash
1. Tạo layout XML đơn giản trước
2. Build after each layout → check syntax
3. Test layout bằng cách preview trong Android Studio
```

### **BƯỚC 3: TẠO ACTIVITY CƠ BẢN**

```java
// Chỉ có onCreate() và setContentView()
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    Log.d("MainActivity", "Activity created successfully");
}
```

### **BƯỚC 4: THÊM CHỨC NĂNG TỪNG BƯỚC**

```bash
1. Thêm findViewById() → Build → Test
2. Thêm event listeners → Build → Test
3. Thêm logic → Build → Test
4. Thêm navigation → Build → Test
```

---

## ⚠️ **TOP 10 LỖI PHẢI TRÁNH**

| STT | LỖI                            | CÁCH TRÁNH                                 |
| --- | ------------------------------ | ------------------------------------------ |
| 1   | Namespace không khớp           | Check build.gradle vs package name         |
| 2   | Theme không tồn tại            | Dùng `Theme.AppCompat.Light.DarkActionBar` |
| 3   | Import sai AppComponentFactory | Chỉ import những gì cần thiết              |
| 4   | XML syntax error               | Kiểm tra dấu `=`, quotes, closing tags     |
| 5   | ID không tồn tại               | Copy chính xác ID từ XML sang Java         |
| 6   | Quên đăng ký Activity          | Thêm vào AndroidManifest ngay khi tạo      |
| 7   | Logic phức tạp trong onCreate  | Tách thành methods riêng                   |
| 8   | Không handle null              | Luôn check null before sử dụng             |
| 9   | Exception không bắt            | Wrap risky code trong try-catch            |
| 10  | Quên super.onCreate()          | Luôn gọi super trước tiên                  |

---

## 🔍 **LỆNH DEBUG HỮU ÍCH**

```bash
# Xem logcat realtime
adb logcat | grep -i "error\|exception\|crash"

# Clear build cache
./gradlew clean

# Build debug
./gradlew assembleDebug

# Install debug APK
./gradlew installDebug
```

---

## 📱 **TESTING CHECKLIST**

### **✅ Trước khi submit:**

- [ ] App compile thành công
- [ ] App build thành công
- [ ] App launch không crash
- [ ] Tất cả UI elements hiển thị
- [ ] Button clicks hoạt động
- [ ] Navigation between screens works
- [ ] Input validation works
- [ ] Error handling works
- [ ] App không crash khi rotate screen

### **✅ Files cần kiểm tra cuối cùng:**

- [ ] `build.gradle.kts` - namespace correct
- [ ] `AndroidManifest.xml` - all activities registered
- [ ] Layout XML files - no syntax errors
- [ ] Activity Java files - clean imports, proper logic
- [ ] `strings.xml` - all strings defined

---

## 💡 **BEST PRACTICES**

1. **Always build after each change**
2. **Use meaningful variable names**
3. **Comment your code**
4. **Keep methods short and focused**
5. **Handle edge cases**
6. **Test on different screen sizes**
7. **Use version control (Git)**
8. **Create backup before major changes**

---

## 🆘 **KHI GẶP LỖI:**

1. **Đọc error message cẩn thận**
2. **Check file và line number được báo lỗi**
3. **Google search exact error message**
4. **Comment out recent changes để isolate**
5. **Use `Log.d()` để debug**
6. **Ask for help với specific error message**

---

## 🎯 **TARGET CHO DỰ ÁN TIẾP THEO:**

- [ ] Zero compilation errors
- [ ] Zero runtime crashes
- [ ] Clean, readable code
- [ ] Proper error handling
- [ ] Good user experience
- [ ] Responsive UI
- [ ] Efficient performance

**Nhớ: "Prevention is better than cure" - Tránh lỗi tốt hơn sửa lỗi! 🚀**
