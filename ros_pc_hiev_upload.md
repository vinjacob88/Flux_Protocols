## **Automatic HIEv uploads from ROS PC**
*Daniel Metzen, 2021-05-06*
*Vinod Jacob, 2022-03-10*
***

### **Summary**
The ROS PC is set up to automatically upload data to HIEv each night. Generally, LoggerNet (and a FTP server for Smartflux) collects the logger data and stores it locally. From there, a Ruby on Rails script parses the metadata and uploads the data to HIEv.

### **Accounts and Passwords**
- **ROS PC account**: username: **ROS**, password: **Pa$$w0rd**
- **Smartflux2 account**: username: **licor**, password: **licor**
### **General folder structure**
The ROS PC has three hard drives, one SSD (C:\) and two HDDs (E:\ & F:\). Software is generally installed on C:\, while data, logger programs and scripts to wrangle data are usually stored in a subfolder for each research facility on E:\ . Once data has been upload to HIEv it is automatically moved to F:\ . Backup files are stored on F:\ as well. 

### **HIEv upload workflow**
#### **1. LoggerNet**
Data from all Campbell Scientific data loggers is collected using LoggerNet every few hour and saved to the corresponding subfolder on E:\ . The LoggerNet setup is backed up at **F:\LoggerNer.bkp**.

#### **2. Smartflux**
Since the conversion of CUP to Smartflux2 in August 2018, the 10Hz raw data is processed in situ on the logger and send to a FTP server running on the ROS PC.

#### **2.1. client-side setup**
The **LI-7x00 tool** can be used to remotely connect to the IRGA installed at CUP. The static IP addresses of the IRGAs can be found at **//ad.uws.edu.au/dfshare/HIEFBR/Field Facilities/IPaddresses.xlsx**. Normally, the 7500RS is installed and it's IP address is **137.154.36.37**. 

The metadata required for processing the flux data by Smartflux2 is specified in the **Site Setup** tab once connected to the IRGA. The settings can be exported and imported using the **Config Files** dropdown at the top. The current config file is saved at **E:\CUP\logger_programs\AU-Cum_7500_site_config.l7x**. A usb drive has to be inserted into the LI-7550 unit to store the raw and processed data. Make sure the data is being logged. If it is not being logged, click the **Start** button on left hand side of panel.

Smartflux2 can run EddyPro in Express Mode out of the box. Running Smartflux2 in advanced mode has to be set up using EddyPro. It's easiest to use one of the .ghg files on HIEv to extract and set the site metadata in EddyPro. The generated *.smartflux file can then be uploaded in the **SmartFlux > EddyPro** tab by clicking **Advanced Mode ...** once connected to the IRGA using the **LI-7x00 tool**. The current file is saved at **E:\CUP\logger_programs\AU-Cum_smartflux_20200512.smartflux**. More information on the differences between Express and Advanced Mode can be found in the [EddyPro manual](https://www.licor.com/documents/1ium2zmwm6hl36yz9bu4). For more information on how to set up advanced processing see section 7 of the [LI-7500RS manual](https://licor.app.boxenterprise.net/s/c7tyf0czqn9ezkq1ki3b).

Finally, the data transfer is set up in the **SmartFlux > Data Repository** tab using the following settings:
- tick **Transfer data to a remote repository**
- server url: **ftp://137.154.36.81:32156/$(filename)**
- username: **licor**
- password: **licor**
- under **File types** tick **LI-COR Raw Data (.ghg) files** and **Daily EddyPro Summaries** 
- under **Transfer Options** tick **Post files to server every half hour after processing** 
- click **Apply Repository Settings**

#### **2.2. server-side setup**
The FTP server on the ROS PC to receive the data is set up using FileZilla Server with the following settings:
- under **Edit > Settings > General settings** set **Listen on these ports** to **32156**
- under **Edit > Settings > General settings > IP Filter** enter * in the top box and **137.154.36.68**, the static IP of SmartFlux2 in the lower box 
- under **Edit > Settings > General settings > Admin Interface Settings** set the port to **14147**
- make sure both these ports are opened by IT
- add a user under **Edit > Users > General** with the username **licor** and the password **licor**
- under **Edit > Users > Shared folders** add **E:\CUP\smartflux\raw_data** and click **Set as home dir**

#### **2.3 Data wrangling**
Scripts to convert data into the TOA5 format and zip up all raw data files into daily chunks are executed using the Task Scheduler and the **bundle_smartflux_data.bat**. Make sure there are no daily summary files without data  in **E:\CUP\smartflux\raw_data**. This will cause the **make_it_toa5_monthly.R** script to fall over. The scripts to prepare the Smartflux2 data stream for HIEv upload can be found at **E:\CUP\smartflux\scripts**.

### **3. Ruby on Rails scripts**
The configuration files for the Ruby on Rails script that uploads to HIEv are located at **C:\DC21-v2.1.02\scripts**. Briefly, the script uploads files from **F:\DC21-Data\Data\UploadPending** to HIEv and once uploaded moves the files to **F:\DC21-Data\Data\Transferred**. Then, new data is moved from the facility raw data subfolder on E:\ to **F:\DC21-Data\Data\UploadPending**. These files are then uploaded and appended to the TOA5 files on HIEv. At the end of the month a new file is created and a new monthly chunk initiated.

The wrapper config file (**C:\DC21-v2.1.02\scripts\wrapper_config.yml**) specifies source and destination paths for moving files, the regular expression filename pattern to look for and the chunking interval.

The transfer config file (**C:\DC21-v2.1.02\scripts\wrapper_config.yml**) specifies the source path and filename for the file to be uploaded, the local path to move the file to after being uploaded and the HIEv metadata associated with the uploaded file.

The Ruby on Rails script is executed by running **C:\DC21-v2.1.02\scripts\windows_api_lod.bat** via the Task Scheduler.

Daily log files are written to **C:\DC21-v2.1.02\scripts\restful-api-uploader-2.1.02\log** and can be helpful in case of trouble shooting. The error messages are fairly misleading though. From experience, the most likely source of error are inconsistent indentations in the .yml files or missing files in folders where the script expects files. 

For more information see the [DC21-doc on github](https://github.com/IntersectAustralia/dc21-doc).

### **4. Email QA scripts**
Most facilities have scripts set up that email pdfs with plots containing the last weeks data. They are usually in the email_scripts subfolder of each facility on E:\ and have an associated .bat file that is executed in the task scheduler.

### **5. Troubleshooting**
- Files not going up to HIEv?
  - Has ROS PC been down?
  - Has HIEv been down?
  - Are files saved locally? 
  - Issues with the wrapper.yml or transfer.yml file? Check logfile.
  - Flux data not uploaded?
    - Filezilla server running and receiving data?
    - Check for empty daily summary files in E:\CUP\smartflux\raw_data.
- Email script not running?
  - Has ROS PC been down?
  - Has HIEv been down?
  - Check script for syntax errors etc.
