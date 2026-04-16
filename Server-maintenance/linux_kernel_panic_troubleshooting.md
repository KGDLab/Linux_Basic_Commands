# 🖥️ Linux 開機失敗（Kernel Panic）排除紀錄

## 📌 問題概述

### 初始狀況
- 螢幕：無畫面
- 主機板顯示碼：AA
- 遠端連線：無法連線

---

## 🔍 問題判斷流程

### 1️⃣ 主機板顯示 AA
- 意義：BIOS 初始化完成（非錯誤）
- 推論：
  - 硬體基本正常
  - 問題可能在顯示或系統層

---

### 2️⃣ 排查顯示問題
- 確認 HDMI/DP 插在顯卡
- 確認螢幕來源

---

### 3️⃣ Clear CMOS 後錯誤

```
KERNEL PANIC!
UFS: Unable to mount root fs on unknown-block(0,0)
```

---

## 🧠 問題本質

Linux kernel / initramfs 損壞或設定錯誤

可能原因：
- 停電異常關機
- kernel 更新失敗
- initramfs 損壞
- BIOS reset

---

## 🔧 解決過程

### Step 1️⃣ 確認 BIOS

```
Boot Option #1 = ubuntu (Samsung SSD)
```

---

### Step 2️⃣ 進入 GRUB
開機按 ESC 或 Shift

---

### Step 3️⃣ 選舊 kernel

```
Ubuntu, with Linux 6.14.x
```

---

### Step 4️⃣ 成功進系統

---

## 🛠️ 修復指令（重要）

請分開執行：

```bash
sudo update-initramfs -u
sudo update-grub
```

或使用一行寫法：

```bash
sudo update-initramfs -u && sudo update-grub
```

---

## 🔁 長期方案

### 移除壞 kernel

```bash
dpkg --list | grep linux-image
sudo apt remove linux-image-6.17.0-20-generic
```

---

### 重新安裝 kernel

```bash
sudo apt update
sudo apt install --reinstall linux-image-generic
```

---

## 📊 總結

- 硬體正常
- kernel 損壞

---

## 💡 結論

使用舊 kernel 開機並修復 initramfs 即可解決問題
