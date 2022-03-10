## **Yarramundi Control (YarCon) and Yarramundi Irrigated (YarIrr) paddock data**
*Daniel Metzen, 2021-05-10*
*Vinod Jacob, 2022-03-10*
***
### **Summary**
Data from the YarIrr flux tower is downloaded manually due to unreliable radio coverage, and then uploaded to hie-storage. Get in touch with the HIE data manager or IT to get access to the hie-storage folders.

### **Logger data**
The following tables are downloaded from the CR3000s using **LoggerNet Connect** on the FLUXSITE toughbook (password: Pa$$w0rd):
- **slow_core**
- **slow_flux**
- **soil_vars**
  
### **Downloading data manually from YarIRR**

1. Connect cable to rs232 port on logger and then connect to toughbook

2. Open loggernet

3. Click *Main* then *connect*

4. Choose FluxIRR then *connect*

5. Ensure clock is correct

5. Click drop down menu and choose *public*

6. Click Custom button on top

7. File mode creates new file in ascii format

8. Double-check the tickboxes of *slow_flux, slow_core and soil_vars* boxes are selected in the menu further down.

9. Check file names

10. Make sure only data since the last collection is downloaded (otherwise this will cause errors during HIEv upload)

11. Click start collection

12 Check the data files

The default local path is **C:\Campbellsci\LoggerNet\Data** and the files are then uploaded to the corresponding hie-storage folder **/data/hiestorage/WorkingData/TERN/PROJECTS/FLUX_TOWER/{Paddock_Con | Paddock_Irr}/slow/**.

13. Click DISCONNECT on loggernet 

14. Make sure equipment is clean 


### **Swapping CF cards for fast data from both paddocks**

The CF cards are swapped with an empty CF card.

1. Hit white **Initiate Removal** button on the **NL116 module**, status light should then turn solid green.
2. Remove data card and replace with blank card *INSERT SILVER SIDE UP*
3. Status light should start flickering red 

The data is uploaded into a subfolder named after the download date to **/data/hiestorage/WorkingData/TERN/PROJECTS/FLUX_TOWER/{Paddock_Con | Paddock_Irr}/fast/{yyyymmdd}/** on hie-storage.

Make sure you delete the old files on the card after uploading or before you head out to swap cards.

### **Changing SD Card from phenocams from both paddocks**

1. Undo clamps on each side and remove body
2. Check if the right amount of pictures have been taken (roughly 8 per day)
3. Unscrew screw on bottom and remove SD card
4. Replace SD card and check if there's space 


Phenocam data is uploaded into a subfolder named after the download date to **/data/hiestorage/WorkingData/TERN/PROJECTS/FLUX_TOWER/Phenocams/{Paddock_Con | Paddock_Irr}/{yyyymmdd}/** on hie-storage.