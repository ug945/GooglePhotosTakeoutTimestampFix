# GooglePhotosTakeoutTimestampFix

# !! CMD DO NOT WORK ON VIDEO !!

https://exiftool.org/

https://takeout.google.com/

only select google photos then download the zip file, unzip the file 


In PowerShell
```
# change HH:MM to your local timezone
exiftool -OffsetTimeOriginal='+HH:MM' -OffsetTimeDigitized='+HH:MM' -OffsetTime='+HH:MM' -tagsfromfile "%d%f.%e.supplemental-metadata.json" "-DateTimeOriginal<photoTakenTimeTimestamp" "-CreateDate<photoTakenTimeTimestamp" "-ModifyDate<photoTakenTimeTimestamp" "-FileCreateDate<photoTakenTimeTimestamp" "-FileModifyDate<photoTakenTimeTimestamp" -d %s -overwrite_original "<THE_FOLDER_CONTAINS_IMAGE_AND_JSON>"

# if "Error: Not a valid PNG" show up, Execute the following lines and then execute the line above again.
cd <THE_FOLDER_CONTAINS_IMAGE_AND_JSON>
exiftool -if '$FileType =~ /JPEG/' -p '$BASENAME.PNG.supplemental-metadata.json' *.png | Rename-Item -NewName  { $_ -replace 'png','jpg' }
exiftool -if '$FileType =~ /JPEG/' -p '$Directory/$FileName' *.png | ForEach-Object { Rename-Item -LiteralPath $_ -NewName ([io.path]::ChangeExtension($_, ".jpg")) }


```

