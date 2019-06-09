There are two jupyter-notebook files used to create the input data for the model and to create output images for the report.


read_dicom4.ipynb
- this script maps out the data set folders from Heidi's group, based upon the different phases
- The user selects one of two main folders to process, either the rcc data or onco data (user selectable flag). This was done to make debugging easier and to quickly remake input data
- for each lesion type chosen, it will get every patient id (the folder name) and select all the phase folders underneath for processing
- it locates the MHA file containing the segmentation parameters (there should only be one MHA, but a few cases had more than one, but the last one was used)
- The MHA is opened with the ITK toolbox and the xy parameters and slice info recorded
- The pydicom toolbox is used to open each dicom file (of the series) and read the pixel array data and a few sample tags. The slice location tag is used to order the slices, in case the file ordering is incorrect (a few cases needed this)
- The MHA data is used to filter out only the slices that contain lesion margins
- The middle slice of the lesion is determined and the center of that lesion becomes the center of a new image, sized 128x128 (variable)
- The new subimage is saved as a grayscale JPG image to an output folder matching the input folder name (easier to debug)
- This processing occurs for every folder underneath the clear cell or onco main folders until all folders have been processed (a full set can be completed in 40 minutes with USB mounted data)
- To run the other type of lesion data, change the flag and run




plot_report_data.ipynb
- This utilizes some of the same functionality as read_dicom4, but instead of subimages for the model, it will produce some report plots (a set of these for every slice that would be used in the model)
- a histogram for each slice, across the center row of the annotation margin
- a data slice across it
- a raw dicom image of the slice with the subimage bounding box and an overlay of the lesion
- a subset image (same as what the model would be using)
- !!The matplotlib routine will consume a lot of memory as it runs, so a full set of data will consume 8GB of leaked memory (even with garbage collection added int) within an hour. Opening a plot and closing then running garbage collection still left some memory lost, but the method to create the overlays did not work well when reusing the figure handle. The easiest solution is to run until memory is exhausted and run in debug starting at the last folder completed.
To run, change the lesion folder flag (as above) and run. A full set of data(rcc or onco) can  

*the number of slices available per patient varies, as the annotations might exist for one slice or many.
