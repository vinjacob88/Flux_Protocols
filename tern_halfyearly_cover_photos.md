## **TERN SuperSite cover photography and photopoints**
*Daniel Metzen, 2021-05-12*
*Vinod Jacob, 2022-03-10*
***

### **Summary**
Every six months cover photos and images at set photopoints are taken within the TERN Core1ha. Images are uploaded to cloudstore and hie-storage afterwards. Field sheets can be found in the TERN_field_sheets folder. The software required and instructions can be found on the TERN supersites website: [RAW2JPG](https://www.dropbox.com/sh/c0ktztigmfl7hrg/AACNmHdEBR9DzJUjcMPgn1Hwa?dl=0), [DCP_313](https://www.dropbox.com/sh/2zr3lnilp9j3pra/AAB-UvcL2lzFxBg79_jTSi0Fa).

### **Core1ha photopoints**
Images are taken at five photopoints, each corner of the Core1ha plot and the center next to the data logger. We marked trees with blue and white stripes to "aim at" with the lens so images are as consistent as possible. The image number of the corresponding location and viewing direction is recorded in the field sheet. After the field campaign the field sheet is digitalised in Excel and uploaded with the photos to a subfolder named after the campaign date to /data/hiestorage/WorkingData/TERN/PROJECTS/CBLP_SUPERSITE/PHOTOPOINTS/{yyyymmdd} on hie-storage and to cloudstore:Shared/CumberlandPlain/Data/EcoImages/PhotoPoint/core1ha/{yyyymmdd}.

For access to hie-storage get in touch with the HIE data manager or IT. For access to the cloudstore folder get in touch with [Alvin Sebastian](mailto:a.sebastian@uq.edu.au) or [Mirko Karan](mailto:mirko.karan@jcu.edu.au). For more information on the photopoint method see chapter 11 of the [SuperSites Vegetation Monitoring Protocols](https://supersites.tern.org.au/images/resource/SuperSites_Vegetation_Monitoring_Protocols_Ver1.pdf).

### **Core1ha cover photography**
Cover photos are suggested to be taken in a 10 x 10m grid, but we've adapted a different approach to minimise the disturbance of the site due to trampling. Thus, our cover photos are taken next to each quadrant of the Gentry transects using a monopod and spirit level attached to the camera. The camera settings are listed at the top of the field sheet. We also use the bracketing generating two images at each location with a exposure bias of 0 and -1. After taking a picture record the Gentry transect number, the quadrant coordinate and the photo number in the field sheet. If there is only blue sky in the field of view the camera won't take a photo. Take note and add a zero LAI value for that location afterwards. Avoid taking photos directly next to tree trunks as this will cause high LAI values. Move 1m further away from the tree and take the photo. 

After the field campaign the raw images (.NEF) are transferred to the local hard drive in a raw folder. If you want to keep the .JPG files move them somewhere else, otherwise the software will overwrite those. Next, run the RAW2JPG software. Check the adjust gamma tick box and click run. Now, you select the folder you saved the raw images to. It will create .JPG files that ony contain the blue channel. Move those images to a processed folder.

Once .JPG files are created from all .NEF files, open the DCP_313 and click run. Go to the processed folder and select all .JPG files. After the software is done there should be a Summary folder and a Results.xlsx file. Additionally, screen each image in the Summary folder for obvious misclassification (e.g. large cloud classified as foliage, tree trunk classified as sky, etc.). Classified foliage is black and gaps white or grey in the top-left image of each summary file. Next, add the gentry transect number, x and y coordinate on the pegs and the exposure bias to the Results.xlsx file. 
For more information on the cover photography processing see chapter 12 of the [SuperSites Vegetation Monitoring Protocol](
https://supersites.tern.org.au/images/resource/SuperSites_Vegetation_Monitoring_Protocols_Ver1.pdf).

After processing is done, only the raw images (.NEF files) are uploaded to cloudstore:Shared/CumberlandPlain/Data/EcoImages/LAI/core1ha/{yyyymmdd} as TERN processes all images centrally now.
The RAW (.NEF) images and the field data spread sheet are uploaded to /data/hiestorage/WorkingData/TERN/PROJECTS/CBLP_SUPERSITE/VEG_LAI/{yyyymmdd}/raw on hie-storage. The contents of the processed folder are uploaded to /data/hiestorage/WorkingData/TERN/PROJECTS/CBLP_SUPERSITE/VEG_LAI/{yyyymmdd}/processed on hie-storage.
