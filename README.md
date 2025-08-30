# Daily Sales Data Processing with Azure

This project demonstrates how to build an **end-to-end automated data pipeline** in Azure to process daily sales CSV files.

## 🚀 Architecture
Blob Storage → Data Factory → Azure Function (validation) → Logic Apps (notification) → Success/Failed folders

![Architecture](https://excalidraw.com/#json=UXFac_-TkvW65F0i2PPr1,Nwz4UiIVLmuhyqv631rHwA)

## 📂 Services Used
- Azure Blob Storage
- Azure Data Factory (ADF)
- Azure Functions (Node.js)
- Azure Logic Apps
- Azure Monitor & Application Insights

## ⚙️ Pipeline Flow
1. Upload CSV file to `incoming/` in Blob Storage.
2. ADF detects new file (event trigger).
3. File copied to `intermediate/`.
4. ADF calls **Azure Function**:
   - Validates headers (TransactionID, ProductName, Amount).
   - Ensures Amount ≥ 0.
5. Based on validation:
   - ✅ Success → File moved to `success/`.
   - ❌ Failure → File moved to `failed/`.
6. ADF calls **Logic App**:
   - Sends success/failure email.
7. Monitoring & retries handled by **Azure Monitor**.

## 🧑‍💻 Function Validation Logic
- Checks required headers
- Ensures `Amount` is not negative
- Returns `"Passed"` or `"Invalid"`

## 📊 Sample Data
