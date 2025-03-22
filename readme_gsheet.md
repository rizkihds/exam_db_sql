# **📊 Google Sheets with SQL Queries - Presentation Outline** ✨📑💻

---

## **📢 Slide 1: Title**
**🏷️ Topic:** Google Sheets with SQL Queries  
**📖 Overview:** A Simple Guide to Using SQL in Google Sheets  
**🎤 Presented by:** RF 🏆🎓💡

---

## **📌 Slide 2: Introduction**
### **❓ Why Use SQL in Google Sheets?**  
- 📊 Helps analyze large datasets quickly
- ⚡ Allows filtering, sorting, and organizing data efficiently
- 🔍 Enables advanced searches without manual effort

---

## **📖 Slide 3: SQL Basics**
### **🧑‍💻 Understanding SQL in Google Sheets**  
- 📝 Uses the `QUERY` function to retrieve data
- 💾 Works similarly to a database
- 🔢 Helps structure and manage spreadsheet data

---

## **📜 Slide 4: Selecting Data**
### **🎯 Using the SELECT Statement**  
```excel
=QUERY(Employees!A1:F101, "SELECT A, B, C", 1)
```
**📋 Extracts specific columns from a sheet** ✅

---

## **🔽 Slide 5: Sorting Data**
### **📂 Using ORDER BY**  
```excel
=QUERY(Employees!A1:F101, "SELECT A, B, C ORDER BY B DESC", 1)
```
**📊 Sorts results in descending order** ⬇️

---

## **🔎 Slide 6: Filtering Data**
### **🎚️ Using WHERE to Filter Data**  
```excel
=QUERY(Employees!A1:F101, "SELECT A, B, C WHERE C > 50", 1)
```
**🚀 Retrieves only rows where column C is greater than 50**

---

## **📉 Slide 7: Summarizing Data**
### **➕ GROUP BY, SUM, COUNT, and AVG**  
```excel
=QUERY(Employees!A1:F101, "SELECT AVG(C), COUNT(A), E GROUP BY E", 1)
```
**🧮 Groups data and calculates averages, totals, and counts**

---

## **🔗 Slide 8: Advanced Queries**
### **📄 Combining Data from Multiple Sheets**  
- 🏗️ Use `ARRAYFORMULA` and `VLOOKUP`  
```excel
=ARRAYFORMULA(
    {"ID", "Name", "Age", "Email", "Dept";
      Employees!A2:A1001,
      Employees!B2:B1001,
      Employees!C2:C1001,
      Employees!D2:D1001,
      IFERROR(VLOOKUP(Employees!E2:E1001, Departments!A:B, 2, FALSE), "No Dept")
    }
)
```

---

## **🔍 Slide 9: More Advanced Filtering**
### **🎭 Searching for Specific Values**  
```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE A MATCHES '.*John.*'", 1)
```
**📋 Finds employees whose names include 'John'**

---

## **⚡ Slide 10: Optimizing Performance**
### **🚀 How to Make Queries Run Faster**  
- 🚫 Avoid selecting entire columns (e.g., `A:A`)
- ⏩ Use fixed ranges (e.g., `A1:A1000`)
- 📊 Store query results in a separate sheet
- 🛠️ Reduce the size of `ARRAYFORMULA` calculations

---

## **🖥️ Slide 11: Using Apps Script**
### **🤖 Automating SQL Queries with Apps Script**  
```javascript
function joinSheets() {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var employees = ss.getSheetByName("Employees").getDataRange().getValues();
  var departments = ss.getSheetByName("Departments").getDataRange().getValues();
  
  var departmentMap = {};
  for (var i = 1; i < departments.length; i++) {
    departmentMap[departments[i][0]] = departments[i][1];
  }
  
  var output = [["Employee_ID", "Name", "Age", "Department_Name"]];
  for (var j = 1; j < employees.length; j++) {
    var deptName = departmentMap[employees[j][3]];
    output.push([employees[j][0], employees[j][1], employees[j][2], deptName]);
  }
  
  var newSheet = ss.getSheetByName("JoinedData") || ss.insertSheet("JoinedData");
  newSheet.clear();
  newSheet.getRange(1, 1, output.length, output[0].length).setValues(output);
}
```
📜🤖🔄 Automates data merging

---

## **🏋️‍♂️ Slide 12: Practice**
### **📊 Try These SQL Queries**  
- ✍️ Write your own queries
- 🔧 Modify existing ones to see different results
- ✅ [Practice Here](https://docs.google.com/spreadsheets/d/1FRvmMF5WQWl7wJ4tW9jnKZlCgMu40wYVl6xNymmc0Q4/edit?usp=sharing)

---

## **🏆 Slide 13: Summary & Next Steps**
### **📌 Key Takeaways**  
- 🎯 SQL makes working with large spreadsheets easier
- 🛠️ Learn to optimize queries for speed
- 🤖 Explore Google Apps Script for automation
- 🚀 Keep practicing to improve your skills

