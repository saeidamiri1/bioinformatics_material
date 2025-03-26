---
date: 2024-11-16
description: Managing Account in DRAC
categories:
  - DRAC
authors:
  - saeidamiri1
---

# Managing Account in DRAC
## How to create an account 
1. Register for account with the [Digital Research Alliance of Canada](https://ccdb.alliancecan.ca/account_application) (DRAC).  
2. For sponsored roles, you will need your **supervisor’s CCI**. The sponsor will need to confirm the request before you can access the resources. 

   1. The information to fill in the form should look as follows:

      - Institution: Calcul Québec: McGill University
      - Department: Human Genetics (see NOTE below)
      - Position. Master’s Student (choose appropriate option)
      - Sponsor : **supervisor’s CCI**
      - Make this role primary? Yes
      - Disable old roles? No

   NOTE: your department affiliation can also be Neurology, Medicine, etc. If 			you’re unsure, put “Neurology”

   2. You can add new roles to an existing account by logging in to your account, then going to **My Account \> Apply for a New Role**. Enter the required information as listed above, and enter the new CCI.  
        
3. Wait until you receive mail confirmation that your account is now active. If you are unsure, send a message to neurobioinfo@mcgill.ca

4. Log in to your DRAC account to find your username

   -  Top of page: “Account for First\_Name Last\_Name (CCI: abc-123, **Username: user**)”  
        
5. The address for a particular resource, along with its specs, can be found on the [DRAC Wiki](https://docs.alliancecan.ca/wiki/Technical_documentation) (left menu, under ‘Resources’).  
     
   - Beluga: **beluga.computecanada.ca**

6. To access the resources, you will need an SSH client.

   1. Windows: Download PuTTY. Insert the relevant info into the GUI.  
      1. Hostname: **beluga.computecanada.ca**  
      2. port: 22

   2. Linux / Mac:

      1. Open a terminal (Ctrl \+ alt \+ T, or **⌘**\+T).

      2. ssh **beluga.computecanada.ca**

7. As of April 2024, all DRAC (i.e. Compute Canada) servers require multifactor authentication. See [the official documentation](https://docs.alliancecan.ca/wiki/Multifactor_authentication) for how to set that up. 

## AFTER YOUR ACCOUNT HAS BEEN ACTIVATED

8. Default user profiles, software environment and common links:

   1. Common links: 

      1. We have created links to several key shared directories, containing such things as common software, data and analysis directories.   
      2. You can copy them to your own home directory for ease of access.  
           
   2. Default user profiles:  
      1. We have created several default configuration files. These are used to set environment variables, create common aliases and functions, and set other parameters which will help you work more safely and easily in our shared software environment.   
      2. You can copy them to your own home directory and they will be loaded automatically at each subsequent login.  
      3. Pro tip: you can create your own environment variables, command aliases and custom functions by adding them to your linux shell config files, e.g. \~/.bash\_profile or \~/.bashrc  
           
   3. Default software environment:   
      1. We have installed a large number of libraries, standalone programs, as well as modules and packages for standard programs such as R, python and perl.   
      2. If you copy the configuration files and links from the previous steps, you should be able to access all the common software, starting from the \~/soft (/home/$USER/soft) directory  
           
   4. **Simple command to copy all default config files and links**  
   ```{verbatim}
      1. cp \-a /lustre03/project/6001220/COMMON/{.\[a-z\]\*,\*} \~/
      ```
      2. Run this command in your terminal, after you have connected to beluga

9. Common DOs and DON’Ts

   1. DO

      1. Create your own subfolder in the shared \~/runs folder  
         1. Use this folder to store your commands, logs and analysis final results  
         2. It will make it easier later for others to access your analyses, while ensuring that they are safe from accidental deletion

      2. Store large temporary input files for your analyses in your `$SCRATCH` folder (`/scratch/$USER`)  
         1. Our group has limited /project space; it should be used for semi-permanent storage only, i.e. the duration of a project

      3. Copy your raw data from its source on the `/nearline` filesystem, to your destination on the /project or /scratch (preferred) filesystems

   2. DON’T

      1. Use the `/nearline` filesystem for any file operations, except as a source from which to copy raw data  
         1. Do not use `/nearline` files directly as inputs for any program. This filesystem is intended only for long-term data archiving

## Some guidelines onn the use of shared space 

1-  /project space is for medium-term storage of final results, or key files for long-term ongoing projects. Your raw inputs and intermediary files should all be
on the /scratch filesystem, where they will be automatically deleted after 60 days of disuse. All your analyses should be run on /scratch. 

2-  For the files you will store on /project, please create your own subfolder in the shared ~/runs folder (absolute path: /project/rrg-grouleau-ac/COMMON/runs).
Use this folder to store your commands, logs and analysis final results. It will make it easier later for others to access your analyses, while ensuring that they are safe from accidental deletion. 

3- The command disksuage_explorer is a great way to search through your files to find what’s using the most space. If your /project data is stored in ~/runs as suggested in point #2, try the following command:
 /project/rrg-grouleau-ac/COMMON/runs/[your folder] 
This will sort your folders by size with largest on top; you can interactively navigate to quickly see what is using so much space

4-  For any projects which have already been completed/published, there should be virtually nothing left in /project space - certainly no large files. If your publication
 mandates data sharing, make sure that the files to share a) have already been deposited in whatever online depository is required, and/or b) are all archived on
 /nearline. If a project is complete, consider compressing all long-term files into an indexed archive file . Not only will this save /project space, but it will also make it
easy to archive to /nearline and restore should someone want it later.

5- When cleaning up your /project space, don't just blindly copy all your files en masse to /nearline; we're very limited in space there too!


6-  Often the biggest space-eaters are alignments (bam/cram files) and raw read
 data (fastq/bam). There is almost never a good reason to keep these files on
 /project - if you’re analyzing them, they should be on /scratch. If you’re done with
 them, they should either be archived on /nearline, or just plain deleted!


7-  If you have any large files you want to keep, make sure they are in a compressed format. i.e. any large vcf files you are using should absolutely be compressed
 (gzip/bzip etc.).

8- Any large intermediate files should be deleted. For e.g. if you're running plink/SKAT and you have tons of genotype files or vcf files from intermediate 
cleanup + imputation steps, delete them! In fact, intermediate files should only exist on /scratch because that’s where you should be running our analyses!

