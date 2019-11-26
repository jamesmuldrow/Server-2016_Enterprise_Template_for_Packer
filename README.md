# Windows Server 2016 Standard Template for Packer

### Introduction 

This repository contains Windows Server 2016 Standard Template that can be used to create boxes for VMWare using Packer ([Website](http://www.packer.io)) ([Github](http://github.com/jamesmuldrow/packer)).

### Windows Editions

This repo currently tested to support the following Windows Editions:

- Windows Server 2016 Stadard version x64 

### Requirements

- Mac running VMWare Fusion 
- Packer installed
- en_windows_server_2016_x64_dvd_9327751.iso or compatible ISO.
    - If using an iso other than the one listed above, you will be required to adjust the iso_name and iso_checksum values in the variables.json file. 

### Getting Started

1. Clone and change directory into this repo
````bash
git clone https://github.com/jamesmuldrow/Server-2016_Template_for_Packer.git
cd Server-2016_Template_for_Packer
````
2. Copy .variables.example.json to variables.json
````bash
cp .variables.example.json variables.json
````
3. Modify lines 88, 89 & 109, 110 in the autounnattend.xml file.
    - 92, 93 & 113, 114 both look like this:  
````xml
<Value>TQBhAHIAaQBuAGUAcwAxAFAAYQBzAHMAdwBvAHIAZAA=</Value>
<PlainText>false</PlainText>

````
Change them to
````xml
<Value>Your Plain Text Password Goes Here</Value>
<PlainText>true</PlainText>
````
4. Change the License Key on line 30
````xml
 <Key>KEY-GOES-HERE</Key>
````
5. Modify the "ssh_password" field in variables.json to reflect user password we modified in step 3.
6. Place downloaded iso file in ./iso folder
7. Run the following command:
````bash
packer build -var-file=variables.json server2016.json
````

Once complete, your resulting VM will be stored in the ./output-vmware-iso directory

Successful completion will look like this: 
````output
==> Builds finished. The artifacts of successful builds are:
--> vmware-iso: VM files in directory: output-vmware-iso
````
### Contributing

Pull requests welcomed.

### References

This repo references code from ([Joe Fitzgerald's Github](https://github.com/joefitzgerald/packer-windows)) & ([Christophe Calvet's Github](https://github.com/christophecalvet/Windows-Server-unattended-plus-VMware-Tools))