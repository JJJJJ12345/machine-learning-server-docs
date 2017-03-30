---

# required metadata
title: "Offline install for Microsoft R Server 9.x for Linux"
description: "How to install R Server on Linux without an internet connection"
keywords: ""
author: "HeidiSteen"
manager: "jhubbard"
ms.date: "03/29/2017"
ms.topic: "article"
ms.prod: "microsoft-r"
ms.service: ""
ms.assetid: ""

# optional metadata
ROBOTS: ""
audience: ""
ms.devlang: ""
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.technology: "r-server"
ms.custom: ""

---

# Offline installation instructions for R Server 9.x for Linux

By default, installers connect to Microsoft download sites to get required and updated components. If firewall restrictions or limits on internet access prevent the installer from reaching these sites, you can download individual components on a computer that has internet access, copy the files to another computer behind the firewall, manually install prerequisites and packages, and then run setup.

> [!NOTE]
> If you have problems with these instructions, please use the feedback button to provide details.

<a name="download"><a/>
## Download setup prerequisites

Using an internet-connected computer, download .NET Core. The R Server installer for **mrsdeploy** is built on .NET Core. Unless you edit the install script to exclude an **mrsdeploy** installation, you will need .NET Core to run Setup.

The file names are `dotnet-dev-centos-x64.1.0.0-preview2-003131.tar.gz` and TBD.

| Component | Version | Download Link |
|-----------|---------|--------|
| Microsoft .NET Core | 1.0.1 | https://go.microsoft.com/fwlink/?linkid=827529 |
| Visual Studio C++ | TBD | TBD tag.gz file |

## Download packages

R Server has package dependencies for various platforms. The list of required packages can be found at [Package dependencies for Microsoft R Server 9.x](rserver-install-linux-hadoop-packages.md).

## Download R Open installer

You can get Microsoft R Open (MRO) 3.3.2 from the [MRAN web site](https://mran.microsoft.com/download/), choosing the distribution for your Linux operating system. 

The filename is `microsoft-r-open-3.3.2.tar.gz`.

<a name="download"><a/>
## Download R Server installer

You can get Microsoft R Server (MRS) 9.x for Linux from one of the following download sites. 

The filename is `en_r_server_910_for_linux_x64_9648602.gz`. 

| Site | Edition | Details |
|------|---------|---------|
| [Visual Studio Dev Essentials](http://go.microsoft.com/fwlink/?LinkId=717968&clcid=0x409) | Developer (free) | This option provides a zipped file, free when you sign up for Visual Studio Dev Essentials. Developer edition has the same features as Enterprise, except it is licensed for development scenarios. <br/><br/>1. Click **Join or Access Now** and enter your account information.<br/>2. Make sure you're in the right place: *my.visualstudio.com*.<br/>3. Click **Downloads**, and then search for *Microsoft R*. |
|[Volume Licensing Service Center (VLSC)](http://go.microsoft.com/fwlink/?LinkId=717966&clcid=0x409) | Enterprise | Sign in, search for "SQL Server 2016 Enterprise edition", and then choose a per-core or CAL licensing option. A selection for **R Server for Windows 9.1.0** is provided on this site. |
| [MSDN subscription downloads](https://msdn.microsoft.com/subscriptions/downloads/hh442898.aspx) | Developer or Enterprise | Subscribers can download software at given subscription levels. Depending on your subscription, you can get either edition. |

## Transfer files

Use a flash drive or another mechanism to transfer downloaded files to a writable directory, such as **/tmp**, on your disconnected server. To summarize, should be transferring the following files:

+ `dotnet-dev-centos-x64.1.0.0-preview2-003131.tar.gz`
+ `microsoft-r-open-3.3.2.tar.gz`
+ `en_r_server_910_for_linux_x64_9648602.gz`
+ packages from the dependency list

## Install package dependencies

On the target system which is disconnected from the internet, run `rpm -qi <package-name>` to install any packages that are missing from your system.

## Unpack distributions

Next, unpack the distributions for prerequisites, MRO, and MRS.

1. Log in as root or a user with sudo privileges.

2. Switch to the **/tmp** directory (assuming it's the download location).

3. Unpack the .NET Core redistribution:

  `[tmp] $ tar zxvf dotnet-dev-centos-x64.1.0.0-preview2-003131.tar.gz`
  
4. Unpack the Visual Studio C++ redistribution:

  `[tmp] $ tar zxvf XXXXXX.tar.gz`

5. Unpack the MRO gzipped file:

  `[tmp] $ tar zxvf microsoft-r-open-3.3.2.tar.gz`

6. Unpack the MRS gzipped file:

  `[tmp] $ tar zxvf en_r_server_901_for_linux_x64_9648602.gz`

## Check files

Files are unpacked into child folders: **microsoft-r-open** and  **MRS90Linux**. If you list the contents, you will see licensing documents, subfolders, and an install script (install.sh)

## Install .NET Core

TBD.

## Install Visual Studio C++ redistributable

TBD.

## Run the MRO install script

R Open is deployed by running the install script with no parameters.


## Run the MRO install script

R Open is deployed by running the install script with no parameters.

1. Log in as root or a user with sudo privileges (`sudo su`). The following instructions assume user privileges with the sudo override.

2. Verify system repositories are up to date:

  `[username] $ sudo yum clean all`

3. Change to the directory to which you downloaded the rpm (for example, **/tmp**):

  `[username] $ cd /tmp`

4. Change to the `microsoft-r-open` directory containing the installation script:

  `[tmp] $ cd microsoft-r-open`

5. Run the script.

  `[microsoft-r-open] $ sudo bash install.sh`

6. When prompted to accept the license terms for Microsoft R Open, click Enter to read the EULA, click **q** when you are finished reading, and then click **y** to accept the terms.

7. Repeat to accept license terms for the Intel MKL libraries, and to start the installation.

When finished, the installer output shows the packages and location of the log file.

## Run the MRS install script

R Server for Linux is deployed by running the install script with no parameters.

1. Change to the `MRS90LINUX` directory containing the installation script:

  `[tmp] $ cd ..\MRS90LINUX`

2. Run the script.

   `[MRS90LINUX] $ sudo bash install.sh`

3. When prompted to accept the license terms for Microsoft R Server, click Enter to read the EULA, click **q** when you are finished reading, and then click **y** to accept the terms.

4. Installer output shows the packages and location of the log file.

## Verify installation

1. List installed packages and get package names:

   `[MRS90LINUX] $ yum list \*microsoft\*`

   `[MRS90LINUX] $ yum list \*deployr\*`

2. Check the version of Microsoft R Open using `rpm -qi`:

   `[MRS90LINUX] $ rpm -qi microsoft-r-open-mro-3.3.x86_64`

3. Check the version of Microsoft R Server:

   `[MRS90LINUX] $ rpm -qi microsoft-r-server-packages-9.0.x86_64`

4. Partial output is as follows (note version 9.0.1):

	 Name        : microsoft-r-server-packages-9.0     Relocations: /usr/lib64
	 Version     : 9.0.1                               Vendor: Microsoft
	 . . .

## Start Revo64

As a verification step, run the Revo64 program.

1. Switch to the directory containing the executable:

   `$ cd MRS90LINUX`

2. Start the program:

   `$ Revo64`

3. Run an R function, such as **rxSummary** on a dataset. Many sample datasets, such as the iris dataset, are ready to use because they are installed with the software:

   `> rxSummary(~., iris)`

  Output from the iris dataset should look similar to the following:

~~~~
  Rows Read: 150, Total Rows Processed: 150, Total Chunk Time: 0.001 seconds
  Computation time: 0.005 seconds.
  Call:
  rxSummary(formula = ~., data = iris)

  Summary Statistics Results for: ~.
  Data: iris
  Number of valid observations: 150

  Name         Mean     StdDev    Min Max ValidObs MissingObs
  Sepal.Length 5.843333 0.8280661 4.3 7.9 150      0
  Sepal.Width  3.057333 0.4358663 2.0 4.4 150      0
  Petal.Length 3.758000 1.7652982 1.0 6.9 150      0
  Petal.Width  1.199333 0.7622377 0.1 2.5 150      0

  Category Counts for Species
  Number of categories: 3
  Number of valid observations: 150
  Number of missing observations: 0

  Species    Counts
  setosa     50
  versicolor 50
  virginica  50
~~~~

To quit the program, type `q()` at the command line with no arguments.

## Configure R Server to operationalize your analytics

The server can be used as-is if you install and use an R IDE on the same box, but to benefit from the deployment and consumption of web services with Microsoft R Server, then you must configure R Server after installation to act as a deployment server and host analytic web services. Possible configurations are a [one-box setup](operationalize/configuration-initial.md) or an [enterprise setup](operationalize/configure-enterprise.md). Doing so also enables remote execution, allowing you to connect to R Server from an R Client workstation and execute code on the server.

## See Also

[Run R Server for Windows](rserver-install-windows.md)

[Supported platforms](rserver-install-supported-platforms.md)

[What's new in R Server](notes/r-server-notes.md)

[Microsoft R Getting Started Guide](microsoft-r-getting-started.md)

[Configure R Server to operationalize analytics](operationalize/configuration-initial.md)