# 🧮 DỰ ÁN MỚI: CALCULATOR APP - MÁY TÍNH ANDROID

## 🎯 **MỤC TIÊU BÀI TẬP**

Tạo một ứng dụng máy tính đơn giản với:

- **Activity:** Xử lý logic tính toán và hiển thị kết quả
- **Pattern:** Clean Code, Error Handling, State Management

---

## 📋 **YÊU CẦU CHỨC NĂNG**

### **Basic Features:**

- **Layout:** GridLayout với các button số và phép tính
- [x] Hiển thị màn hình calculator
- [x] Các button số: 0-9
- [x] Các phép tính: +, -, \*, /
- [x] Button = để tính kết quả
- [x] Button C để xóa
- [x] Button CE để xóa số cuối
- [x] Hiển thị phép tính và kết quả

### **Advanced Features (Optional):**

- [x] Xử lý số thập phân
- [x] Xử lý lỗi chia cho 0
- [x] History của các phép tính
- [x] Copy kết quả

---

## 🎨 **THIẾT KẾ GIAO DIỆN**

### **Layout Structure:**

```
┌─────────────────────────────┐
│ TextView: Display (Kết quả) │
├─────────────────────────────┤
│ TextView: History           │
├─────────────────────────────┤
│  CE   C    ←    /          │
├─────────────────────────────┤
│  7    8    9    *          │
├─────────────────────────────┤
│  4    5    6    -          │
├─────────────────────────────┤
│  1    2    3    +          │
├─────────────────────────────┤
│  0    .    =               │
└─────────────────────────────┘
```

---

## 📱 **STEP 1: TẠO PROJECT MỚI**

### **1.1. Setup Project:**

```bash
Project Name: CalculatorApp
Package Name: com.example.calculatorapp
Language: Java
Minimum SDK: API 24
```

### **1.2. Kiểm tra build.gradle.kts:**

```kotlin
android {
    namespace = "com.example.calculatorapp"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.example.calculatorapp"
        minSdk = 24
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"
    }
}
```

---

## 🎨 **STEP 2: TẠO LAYOUT**

### **2.1. activity_main.xml:**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:background="#f0f0f0"
    android:padding="16dp">

    <!-- Display Area -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1"
        android:orientation="vertical"
        android:background="#ffffff"
        android:padding="16dp"
        android:layout_marginBottom="16dp"
        android:elevation="4dp">

        <!-- History Display -->
        <TextView
            android:id="@+id/textViewHistory"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="1"
            android:text=""
            android:textSize="16sp"
            android:textColor="#666666"
            android:gravity="end|bottom"
            android:padding="8dp" />

        <!-- Main Display -->
        <TextView
            android:id="@+id/textViewDisplay"
            android:layout_width="match_parent"
            android:layout_height="0dp"
            android:layout_weight="2"
            android:text="0"
            android:textSize="32sp"
            android:textColor="#000000"
            android:gravity="end|center_vertical"
            android:padding="8dp"
            android:background="#f8f8f8" />

    </LinearLayout>

    <!-- Button Area -->
    <GridLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:columnCount="4"
        android:rowCount="6">

        <!-- Row 1: CE, C, ←, / -->
        <Button android:id="@+id/buttonCE"
            style="@style/CalculatorButton.Function"
            android:text="CE" />

        <Button android:id="@+id/buttonC"
            style="@style/CalculatorButton.Function"
            android:text="C" />

        <Button android:id="@+id/buttonBackspace"
            style="@style/CalculatorButton.Function"
            android:text="←" />

        <Button android:id="@+id/buttonDivide"
            style="@style/CalculatorButton.Operator"
            android:text="/" />

        <!-- Row 2: 7, 8, 9, * -->
        <Button android:id="@+id/button7"
            style="@style/CalculatorButton.Number"
            android:text="7" />

        <Button android:id="@+id/button8"
            style="@style/CalculatorButton.Number"
            android:text="8" />

        <Button android:id="@+id/button9"
            style="@style/CalculatorButton.Number"
            android:text="9" />

        <Button android:id="@+id/buttonMultiply"
            style="@style/CalculatorButton.Operator"
            android:text="*" />

        <!-- Row 3: 4, 5, 6, - -->
        <Button android:id="@+id/button4"
            style="@style/CalculatorButton.Number"
            android:text="4" />

        <Button android:id="@+id/button5"
            style="@style/CalculatorButton.Number"
            android:text="5" />

        <Button android:id="@+id/button6"
            style="@style/CalculatorButton.Number"
            android:text="6" />

        <Button android:id="@+id/buttonSubtract"
            style="@style/CalculatorButton.Operator"
            android:text="-" />

        <!-- Row 4: 1, 2, 3, + -->
        <Button android:id="@+id/button1"
            style="@style/CalculatorButton.Number"
            android:text="1" />

        <Button android:id="@+id/button2"
            style="@style/CalculatorButton.Number"
            android:text="2" />

        <Button android:id="@+id/button3"
            style="@style/CalculatorButton.Number"
            android:text="3" />

        <Button android:id="@+id/buttonAdd"
            style="@style/CalculatorButton.Operator"
            android:text="+" />

        <!-- Row 5: 0, ., = -->
        <Button android:id="@+id/button0"
            style="@style/CalculatorButton.Number"
            android:layout_columnSpan="2"
            android:text="0" />

        <Button android:id="@+id/buttonDecimal"
            style="@style/CalculatorButton.Number"
            android:text="." />

        <Button android:id="@+id/buttonEquals"
            style="@style/CalculatorButton.Equals"
            android:text="=" />

    </GridLayout>

</LinearLayout>
```

### **2.2. styles.xml (tạo file trong res/values/):**

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>

    <!-- Base Calculator Button Style -->
    <style name="CalculatorButton">
        <item name="android:layout_width">0dp</item>
        <item name="android:layout_height">60dp</item>
        <item name="android:layout_columnWeight">1</item>
        <item name="android:layout_margin">2dp</item>
        <item name="android:textSize">18sp</item>
        <item name="android:textStyle">bold</item>
    </style>

    <!-- Number Button Style -->
    <style name="CalculatorButton.Number">
        <item name="android:background">#ffffff</item>
        <item name="android:textColor">#000000</item>
    </style>

    <!-- Operator Button Style -->
    <style name="CalculatorButton.Operator">
        <item name="android:background">#ff9500</item>
        <item name="android:textColor">#ffffff</item>
    </style>

    <!-- Function Button Style -->
    <style name="CalculatorButton.Function">
        <item name="android:background">#a6a6a6</item>
        <item name="android:textColor">#000000</item>
    </style>

    <!-- Equals Button Style -->
    <style name="CalculatorButton.Equals">
        <item name="android:background">#ff9500</item>
        <item name="android:textColor">#ffffff</item>
    </style>

</resources>
```

---

## ☕ **STEP 3: TẠO ACTIVITY**

### **3.1. MainActivity.java - Version cơ bản:**

```java
package com.example.calculatorapp;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    // UI Components
    private TextView textViewDisplay;
    private TextView textViewHistory;

    // Calculator State
    private String currentInput = "0";
    private String operator = "";
    private double firstOperand = 0;
    private boolean isOperatorPressed = false;
    private boolean isEqualsPressed = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initializeViews();
        setupButtonListeners();
    }

    private void initializeViews() {
        textViewDisplay = findViewById(R.id.textViewDisplay);
        textViewHistory = findViewById(R.id.textViewHistory);
    }

    private void setupButtonListeners() {
        // Number buttons
        setupNumberButton(R.id.button0, "0");
        setupNumberButton(R.id.button1, "1");
        setupNumberButton(R.id.button2, "2");
        setupNumberButton(R.id.button3, "3");
        setupNumberButton(R.id.button4, "4");
        setupNumberButton(R.id.button5, "5");
        setupNumberButton(R.id.button6, "6");
        setupNumberButton(R.id.button7, "7");
        setupNumberButton(R.id.button8, "8");
        setupNumberButton(R.id.button9, "9");

        // Decimal button
        findViewById(R.id.buttonDecimal).setOnClickListener(v -> appendDecimal());

        // Operator buttons
        setupOperatorButton(R.id.buttonAdd, "+");
        setupOperatorButton(R.id.buttonSubtract, "-");
        setupOperatorButton(R.id.buttonMultiply, "*");
        setupOperatorButton(R.id.buttonDivide, "/");

        // Function buttons
        findViewById(R.id.buttonEquals).setOnClickListener(v -> calculateResult());
        findViewById(R.id.buttonC).setOnClickListener(v -> clearAll());
        findViewById(R.id.buttonCE).setOnClickListener(v -> clearEntry());
        findViewById(R.id.buttonBackspace).setOnClickListener(v -> backspace());
    }

    private void setupNumberButton(int buttonId, String number) {
        findViewById(buttonId).setOnClickListener(v -> appendNumber(number));
    }

    private void setupOperatorButton(int buttonId, String op) {
        findViewById(buttonId).setOnClickListener(v -> setOperator(op));
    }

    // ============ CALCULATOR LOGIC ============

    private void appendNumber(String number) {
        if (currentInput.equals("0") || isOperatorPressed || isEqualsPressed) {
            currentInput = number;
            isOperatorPressed = false;
            isEqualsPressed = false;
        } else {
            currentInput += number;
        }
        updateDisplay();
    }

    private void appendDecimal() {
        if (isOperatorPressed || isEqualsPressed) {
            currentInput = "0.";
            isOperatorPressed = false;
            isEqualsPressed = false;
        } else if (!currentInput.contains(".")) {
            currentInput += ".";
        }
        updateDisplay();
    }

    private void setOperator(String op) {
        if (!operator.isEmpty() && !isOperatorPressed) {
            calculateResult();
        }

        firstOperand = Double.parseDouble(currentInput);
        operator = op;
        isOperatorPressed = true;

        // Update history
        textViewHistory.setText(currentInput + " " + operator);
    }

    private void calculateResult() {
        if (operator.isEmpty() || isOperatorPressed) {
            return;
        }

        try {
            double secondOperand = Double.parseDouble(currentInput);
            double result = performCalculation(firstOperand, secondOperand, operator);

            // Update history
            String calculation = firstOperand + " " + operator + " " + secondOperand + " =";
            textViewHistory.setText(calculation);

            // Update display
            currentInput = formatResult(result);
            updateDisplay();

            // Reset state
            operator = "";
            isEqualsPressed = true;

        } catch (Exception e) {
            showError("Lỗi tính toán");
        }
    }

    private double performCalculation(double first, double second, String op) {
        switch (op) {
            case "+":
                return first + second;
            case "-":
                return first - second;
            case "*":
                return first * second;
            case "/":
                if (second == 0) {
                    throw new ArithmeticException("Division by zero");
                }
                return first / second;
            default:
                return 0;
        }
    }

    private String formatResult(double result) {
        // Nếu là số nguyên, hiển thị không có thập phân
        if (result == Math.floor(result)) {
            return String.valueOf((long) result);
        } else {
            return String.valueOf(result);
        }
    }

    private void clearAll() {
        currentInput = "0";
        operator = "";
        firstOperand = 0;
        isOperatorPressed = false;
        isEqualsPressed = false;

        updateDisplay();
        textViewHistory.setText("");
    }

    private void clearEntry() {
        currentInput = "0";
        updateDisplay();
    }

    private void backspace() {
        if (currentInput.length() > 1) {
            currentInput = currentInput.substring(0, currentInput.length() - 1);
        } else {
            currentInput = "0";
        }
        updateDisplay();
    }

    private void updateDisplay() {
        textViewDisplay.setText(currentInput);
    }

    private void showError(String message) {
        Toast.makeText(this, message, Toast.LENGTH_SHORT).show();
        clearAll();
    }
}
```

---

## 📝 **STEP 4: CẬP NHẬT AndroidManifest.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">

        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:screenOrientation="portrait">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

    </application>

</manifest>
```

---

## 📝 **STEP 5: CẬP NHẬT strings.xml**

```xml
<resources>
    <string name="app_name">Calculator</string>
    <string name="calculator_display_hint">0</string>
    <string name="error_division_by_zero">Không thể chia cho 0</string>
    <string name="error_invalid_operation">Phép tính không hợp lệ</string>
</resources>
```

---

## 🧪 **STEP 6: TESTING PLAN**

### **6.1. Basic Testing:**

- [ ] App khởi động không crash
- [ ] Tất cả button có thể click
- [ ] Hiển thị số chính xác
- [ ] Phép cộng: 2 + 3 = 5
- [ ] Phép trừ: 5 - 2 = 3
- [ ] Phép nhân: 3 \* 4 = 12
- [ ] Phép chia: 8 / 2 = 4

### **6.2. Edge Cases:**

- [ ] Chia cho 0 → hiển thị lỗi
- [ ] Số thập phân: 1.5 + 2.5 = 4
- [ ] Button C xóa tất cả
- [ ] Button CE xóa số hiện tại
- [ ] Button ← xóa từng ký tự

### **6.3. Advanced Testing:**

- [ ] Chuỗi phép tính: 2 + 3 \* 4 = ?
- [ ] Xoay màn hình → giữ nguyên dữ liệu
- [ ] Số âm: -5 + 3 = -2

---

## 🚀 **NÂNG CẤP (OPTIONAL)**

### **7.1. Thêm History Activity:**

```java
// Tạo HistoryActivity để xem lịch sử tính toán
public class HistoryActivity extends AppCompatActivity {
    // ListView hoặc RecyclerView để hiển thị history
}
```

### **7.2. Thêm chức năng:**

- Memory functions (M+, M-, MR, MC)
- Scientific calculator (sin, cos, sqrt, etc.)
- Copy/Paste results
- Themes (Dark/Light mode)

---

## 🎯 **LEARNING OUTCOMES**

Sau khi hoàn thành bài tập này, bạn sẽ nắm vững:

1. **Layout Design:**

   - GridLayout cho button matrix
   - Styling với custom styles
   - Responsive design

2. **Activity Pattern:**

   - State management
   - Event handling
   - UI updates

3. **Programming Concepts:**

   - Clean code structure
   - Error handling
   - Input validation

4. **Android Specifics:**
   - findViewById pattern
   - OnClickListener
   - Toast messages
   - Screen orientation

---

## 📋 **CHECKLIST HOÀN THÀNH**

- [ ] Project setup thành công
- [ ] Layout hiển thị đúng
- [ ] Tất cả button hoạt động
- [ ] Calculator logic chính xác
- [ ] Error handling hoàn chỉnh
- [ ] Testing tất cả cases
- [ ] Code clean và có comment
- [ ] App không crash

**Bắt đầu với bài tập này và báo cáo tiến độ nhé! 🎉**
