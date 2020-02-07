# Linux Basic Command

 ## I also manually reboot using this command
 
  - ``` sudo init 6```
 
 ## Shutdown your pc
 
  - ``` sudo init 0```
 
 ## Time schedule shutdown your pc
 
  - ``` sudo shutdown -P +45 ``` 
 
  That means your pc shutdown after 45 minute
  ## copy file one directory to another
  
  - ``` cp <source> <destination> ```
  
  use -r that  recursive copy file
    
  - ``` cp -r <source> <destination> ```
    
  ## Remove all file
    
  - ``` rm -rf * ```
  ## copy file one pc to another pc
   - ``` scp -r <file or folder name> <pc name>@<pc ip>:<destination directory>```
   
  ## Download file use terminal
  
  ```wget -c --retry-connrefused --waitretry=1 --read-timeout=3600 --timeout=60 -t 0 file_url'```
  
  ## zip your file use terminal 
  
  ```zip mytext.zip text.txt```
  
  ## unzip file
  ```unzip file.zip```
