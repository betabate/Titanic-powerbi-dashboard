# 📊 Titanic Survival & Demographic Analysis Dashboard (Power BI)

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query_ETL-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)

## 📌 Project Overview
โปรเจกต์การวิเคราะห์ข้อมูลเชิงลึกและสร้าง Interactive Dashboard ด้วย **Microsoft Power BI** เพื่อศึกษาปัจจัยทางประชากรศาสตร์และเศรษฐกิจสังคม (เพศ, ช่วงอายุ, และระดับชั้นตั๋วโดยสาร) ที่ส่งผลต่ออัตราการรอดชีวิตของผู้โดยสารบนเรือไททานิคจำนวน 891 รายการ

---

## 🖥️ Dashboard Preview
*(ภาพตัวอย่างหน้าตา Dashboard และการโต้ตอบผ่านตัวกรองข้อมูล)*

![Dashboard Overview](titanic_report.pdf)

<!-- หากมีไฟล์ GIF ให้ลบเครื่องหมายคอมเมนต์ด้านล่างออก -->
<!-- ![Interactive Demo](assets/demo_interaction.gif) -->

---

## 🛠️ Data Preparation & Technical Workflow
1. **Data Cleaning & ETL (Power Query):**
   * จัดการค่าว่าง (Missing Values) เพื่อรักษาความสมบูรณ์ของจำนวนประชากรทั้งหมด (891 records) โดยไม่เกิด Data Bias
   * แปลงรหัสตัวแปรเชิงหมวดหมู่ (`Pclass` และ `Status`) ให้สื่อความหมายชัดเจนสำหรับผู้ใช้งาน
   * ทำ **Feature Binning** แบ่งกลุ่มช่วงอายุ (`Age (bins)`) ช่วงละ 10 ปี เพื่อวิเคราะห์การกระจายตัวของประชากรแต่ละวัย
2. **DAX Measures & Calculations:**
   พัฒนาสูตรคำนวณแบบไดนามิกด้วย DAX เพื่อใช้ใน KPI Cards และกราฟเปรียบเทียบ:
   ```dax
   // จำนวนผู้โดยสารทั้งหมด
   Total Passengers = COUNTROWS('train')

   // จำนวนผู้รอดชีวิตและเสียชีวิต
   Total Survived = SUM('train'[Survived])
   Total Died = [Total Passengers] - [Total Survived]

   // อัตราการรอดชีวิต (%)
   Survival Rate % = DIVIDE([Total Survived], [Total Passengers], 0)
   ```

---

## 💡 Key Insights
* **Overall Survival Rate:** จากผู้โดยสารทั้งหมด **891 คน** มีผู้รอดชีวิต **342 คน (38.38%)** และเสียชีวิต **549 คน (61.62%)**
* **Gender Disparity ("Women and Children First"):** ผู้โดยสารเพศหญิงมีสัดส่วนการรอดชีวิตสูงกว่าเพศชายอย่างมีนัยสำคัญในทุกช่วงอายุ ขณะที่เพศชายในช่วงอายุ 20–30 ปี เป็นกลุ่มที่มีจำนวนผู้เสียชีวิตสูงที่สุด
* **Infant & Child Priority:** ในกลุ่มผู้โดยสารเพศชาย มีเพียงกลุ่มเด็กเล็ก (**ช่วงอายุ 0–10 ปี**) เท่านั้นที่มีจำนวนผู้รอดชีวิตมากกว่าผู้เสียชีวิต
* **Socio-Economic Impact:** ผู้โดยสารชั้น 1 (`Class 1`) มีอัตราการรอดชีวิตสูงถึง **62.96%** เทียบกับผู้โดยสารชั้น 3 (`Class 3`) ที่มีอัตราการรอดชีวิตเพียงประมาณ **24%**

---

## 📂 Repository Structure
* `titanic_report.pbix` - ไฟล์ต้นฉบับ Power BI Desktop (สามารถดาวน์โหลดไปเปิดใช้งานได้ทันที)
* `titanic_report.pdf` - ไฟล์รายงานรูปแบบ PDF
* `dataset.csv` - ชุดข้อมูลต้นฉบับที่ใช้ในการวิเคราะห์
