# **Google Sheets with SQL Query - Course Document**

## **1. Basic Google Sheets with SQL**

### **1.1 Introduction to SQL in Google Sheets**

- Using one sheet with **100+ rows**
- Overview of Google Sheets Query Language
- Structuring data efficiently for querying
- 📂 [**Dataset Link**]([https://docs.google.com/spreadsheets/d/your_actual_dataset_link](https://docs.google.com/spreadsheets/d/1FRvmMF5WQWl7wJ4tW9jnKZlCgMu40wYVl6xNymmc0Q4/edit?usp=sharing))

### **1.2 Basic SQL Usage in Google Sheets**

#### **1.2.1 Selecting Data**

- **SELECT**: Extract specific columns from a dataset
  ```excel
  =QUERY(Employees!A1:F101, "SELECT A, B, C", 1)
  ```

#### **1.2.2 Sorting Data**

- **ORDER BY**: Sorting in ascending/descending order
  ```excel
  =QUERY(Employees!A1:F101, "SELECT A, B, C ORDER BY B DESC", 1)
  ```

#### **1.2.3 Filtering Data**

- **WHERE Clause**: Applying conditions
  ```excel
  =QUERY(Employees!A1:F101, "SELECT A, B, C WHERE C > 50", 1)
  ```

#### **1.2.4 Aggregating Data**

- **SUM, COUNT, AVG**
  ```excel
  =QUERY(Employees!A1:F101, "SELECT AVG(C), COUNT(A), E GROUP BY E", 1)
  ```

---

## **2. Advanced Google Sheets with SQL Query**

### **2.1 Using Multiple Sheets and Complex Queries**

- Example dataset with **1000+ rows**
- Organizing data across multiple sheets
- 📂 [**Dataset Link**]([https://docs.google.com/spreadsheets/d/your_actual_dataset_link](https://docs.google.com/spreadsheets/d/1FRvmMF5WQWl7wJ4tW9jnKZlCgMu40wYVl6xNymmc0Q4/edit?usp=sharing))

### **2.2 Advanced SQL Usage**

#### **2.2.1 Joining Data from Multiple Sheets**

- **Using ARRAYFORMULA & VLOOKUP**
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

#### **2.2.2 Filtering with Multiple Conditions**

- **WHERE + AND/OR**
  ```excel
  =QUERY(ARRAYFORMULA(
    {"ID", "Name", "Age", "Email", "Dept";
      Employees!A2:A1001, 
      Employees!B2:B1001, 
      Employees!C2:C1001, 
      Employees!D2:D1001, 
      IFERROR(VLOOKUP(Employees!E2:E1001, Departments!A:B, 2, FALSE), "No Dept")
    }
  ), "SELECT * WHERE Col3 > 30 AND Col5 = 'SALES'", 1)
  ```

#### **2.2.3 Sort, Grouping and Aggregation Per Department**

- **GROUP BY + COUNT & AVG**
  ```excel
  =QUERY(ARRAYFORMULA(
    {"ID", "Name", "Age", "Email", "Dept";
      Employees!A2:A1001, 
      Employees!B2:B1001, 
      Employees!C2:C1001, 
      Employees!D2:D1001, 
      IFERROR(VLOOKUP(Employees!E2:E1001, Departments!A:B, 2, FALSE), "No Dept")
    }
  ), "SELECT Col5, AVG(Col3), COUNT(Col1) GROUP BY Col5 ORDER BY COUNT(Col1) DESC", 1)
  ```

#### **2.2.4 Combining Multiple Sheet (UNION Equivalent)**

```exce 
=ARRAYFORMULA({QUERY(Employees!A:E, "SELECT A, B, C"); QUERY(Employees!A:E, "SELECT A, B, C")})
```

#### **2.2.5 Extracting Employees with the Highest Age (LIMIT Equivalent)**

```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C ORDER BY B DESC LIMIT 1", 1)
```

#### **2.2.6 Finding Employees with Name Containing Specific Letters (LIKE Equivalent Using MATCHES)**

```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE A MATCHES '.*John.*'", 1)
```

#### **2.2.7 Finding Employees by Birth Year**
```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE YEAR(E) = 1990", 1)
```

#### **2.2.8 Finding Employees from a Specific City**
```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE F = 'New York'", 1)
```

#### **2.2.9 Finding Employees with a Specific Nationality**
```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE G = 'Canadian'", 1)
```

#### **2.2.10 Finding Employees with Phone Numbers from a Specific Area Code**
```excel
=QUERY(Employees!A1:F1001, "SELECT A, B, C WHERE H LIKE '415-%'", 1)
```

---

## **3. More Advanced Insights**

### **3.1 Performance Tweaks for Large Datasets**

- **Reduce Data Range (Avoid A:A), use fixed ranges (`A1:A1000`)**
- **Use dynamic ranges instead of full columns**
- **Store query results in a separate sheet to reduce recalculations**

### **3.2 Formula Simplification for Faster Processing**

- **Use Helper Columns Instead of Complex Queries**
- **Use ARRAYFORMULA with Conditions (Instead of QUERY)**
  ```excel
  =ARRAYFORMULA(IF(Employees!A2:A1000<>"", Employees!A2:A1000*2, ""))
  ```
- **Avoid Recalculating the Same Data Multiple Times**
- **Reduce ARRAYFORMULA Size Using IFERROR**
  ```excel
  =ARRAYFORMULA(IFERROR(Employees!A2:A1000/Employees!B2:B1000, ""))
  ```
- **Convert Large Formulas to Static Values** (Ctrl + Shift + V)

### **3.3 Using Google Apps Script for Complex Queries**

- **Example: Using Apps Script to join large datasets efficiently**
  ```javascript
  function joinSheets() {
    var ss = SpreadsheetApp.getActiveSpreadsheet();
    var employees = ss.getSheetByName("Employees").getDataRange().getValues();
    var departments = ss.getSheetByName("Departments").getDataRange().getValues();
    
    var departmentMap = {};
    for (var i = 1; i < departments.length; i++) {
      departmentMap[departments[i][0]] = departments[i][1];
    }
    
    var output = [["Employee_ID", "Name", "Age", "Department_Name", "Nationality"]];
    for (var j = 1; j < employees.length; j++) {
      var deptName = departmentMap[employees[j][3]];
      var nationality = employees[j][5]; // Ensure nationality aligns with address
      output.push([employees[j][0], employees[j][1], employees[j][2], deptName, nationality]);
    }
    
    var newSheet = ss.getSheetByName("JoinedData") || ss.insertSheet("JoinedData");
    newSheet.clear();
    newSheet.getRange(1, 1, output.length, output[0].length).setValues(output);
  }
  ```

---

## **4. Practice Datasets & Exercises**

📂 [**Dataset Link**]([https://docs.google.com/spreadsheets/d/your_actual_dataset_link](https://docs.google.com/spreadsheets/d/1FRvmMF5WQWl7wJ4tW9jnKZlCgMu40wYVl6xNymmc0Q4/edit?usp=sharing))

