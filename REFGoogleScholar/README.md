
### **1. INITIALIZE PROCESS**

-   **./Framework/InitiAllSettings** - Loads configuration data from `Config.xlsx` and Orchestrator Assets.
        
-   **./Framework/GetAppCredential** - Retrieves Google Scholar login credentials (Email/Password) from Orchestrator Assets.
        
-   **./Framework/InitiAllApplications** - Opens the browser (Chrome), navigates to Google Scholar, performs the Login sequence using the retrieved credentials.
        

### **2. GET TRANSACTION DATA**

-   **./Framework/GetTransactionData** - Fetches the next transaction item from the Orchestrator Queue (`REFGoogleScholar`).

### **3. PROCESS TRANSACTION**

-   **Process.xaml** (The Core Logic)
    
    -   **Logic Check:** Inspects the current Transaction Item to determine if it contains paper data (Title, URL, Citations).
        
    -   **Producer Logic (If Data Missing):**
        
        -   If the item is a trigger (no paper data), the bot navigates to the user's profile.
            
        -   Scrapes the full list of publications (Title, Year, Citations) using **Table Extraction**.
            
        -   Uses **Bulk Add Queue Items** to populate the Orchestrator queue with the scraped papers.
            
    -   **Consumer Logic (If Data Exists):**
        
        -   **Access Citation:** Extracts the "Cited By" score directly from the queue item's `SpecificContent` (optimized to avoid unnecessary page navigation).
            
        -   **Data Cleaning:** Parses the raw string (e.g., "Cited by 45") to obtain the integer score.
            
        -   **Reporting:** Logs the Paper Title and the extracted Score for validation.
            
-   **./Framework/SetTransactionStatus**
    
    -   Updates the status of the processed transaction to **Success**, **Business Rule Exception**, or **System Exception**.
        

### **4. END PROCESS**

-   **./Framework/CloseAllApplications** - Logs out and closes applications used throughout the process

### For New Project ###
1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
