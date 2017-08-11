Steps To Implement Above Solution
1) Import the Cab file “Local Group And Users.cab”
•	In your ConfigMgr Current Branch Or ConfigMgr 2012 console, on Assets and Compliance -> Compliance Settings
•	Right-click on "Configuration Baseline" and Import this cab file (http://technet.microsoft.com/en-us/library/hh691016.aspx  )
•	Once done deploy the baseline to the collection of machines from which you need. (http://technet.microsoft.com/en-us/library/hh219289.aspx  )
2) Import the MOF file so that hardware inventory class is updated in ConfigMgr.  This is how you do
•	On the SCCM console, Administration -> Client Settings. 
•	Right-click “Default Client Settings” and go to properties.
•	Select Hardware Inventory, then on the right "Set Classes”.
•	Click Import and browse to the LocalGroupAndUsers.mof file you saved.
  Content of MOF file 
========================================
[ SMS_Report (TRUE),
  SMS_Group_Name ("UserInLocalGroup"),
  SMS_Class_ID ("MICROSOFT|UserInLocalGroup|1.0"),
  Namespace ("root\\\\cimv2") ]
class WIN32_UserInLocalGroup : SMS_Class_Template
{
    [SMS_Report (TRUE), key ] string Account;
    [SMS_Report (TRUE)      ] string Domain;
    [SMS_Report (TRUE), key ] string Name;
   [SMS_Report (TRUE), key ] string Group;
    [SMS_Report (TRUE)      ] string Type; 
};
====================================================
3) Import the report files (*.rdl) into SCCM reporting service website. 
•	Access to SCCM reporting service website (http://<your SCCM site server>/reports) . 
•	Go to “ConfigMgr_<sitecode>”. Create a folder to store custom reports, e.g. “Customised Reports”. 
•	Click “Upload File” to upload above .rdl files. 
•	Select “Show Details” to list all the reports under Customised Reports directory. 
•	Select the newly imported report file. Click Edit button. Go to Data Sources. And then click Browse button to choose ConfigMgr data source (/Home/ConfigMgr_<sitecode>/{xxxxxxx-xxxxx-xxxxxx}. Scroll down to the bottom and click OK to save changes. 
