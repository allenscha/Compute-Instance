## Compute > Instance > Overview


An instance is a virtual server that consists of a virtual CPU, memory, and underlying disk. Install customer services or applications on this server and use a combination of various services provided by NHN Cloud.

## Instance Components

The elements that make up the instance are:

- **Image**: The virtual disk containing the instance's operating system
- **Flavor**: Virtual hardware performance of the instance
- **Availability zone**(AZ): The physical location where the instance will be created
- ****key-pair: A key used as a means of accessing the instance.
- **Security group**: Set up instance network security
- **Network**: The virtual network to which the instance will be connected.

This information changes the properties of the instance and how it is used. Of this information, except for images and Availability Zones, settings can be changed after instance creation, but some instance types (flavors) cannot be changed after instance creation. For a detailed description of changing the instance type, [see Changing](./console-guide/#_15)the Instance Type in the Console User Guide.

### image

An image is a virtual disk that contains an operating system. NHN Cloud currently supports CentOS, Debian, Ubuntu, Rocky, and Windows. For detailed supported operating system versions [please refer to NHN Cloud Service Introduction](https://toast.com/service/compute/instance).

All images are set to run optimally on the virtual hardware of the instance, and they have undergone security verification by NHN Cloud, so they can be used safely. For a detailed description of the images, [see Image overview](/Compute/Image/ko/overview/).

### Instance flavor

NHN Cloud provides various instance types to suit your needs. Depending on the characteristics of the service or application to be operated, you can create an instance of the appropriate type. You can also easily change the type of an instance that has already been created in the web console.

| type    | explanation |
| ------- | -------------------------------------------------|
| m2 | This type balances CPU and memory. Use when the performance requirements of a service or application are not clear. |
| c2 | This is an instance type that sets the CPU performance high. Use for web application servers or analytics systems that require high-performance computational power. |
| r2 | It can be used when memory is used more than other resources. It is typically used for in-memory databases or cache servers. |
| t2 | It's a low-cost instance. Use for servers that do not have high workloads. |
| u2 | This is the cheapest instance. Use on servers that do not have high workloads.<br>Because it uses local disks, it is relatively less reliable than other instances, but it is available at a lower price.<br>Instances of this type do not guarantee I/O performance. |
| x1 | It is a type that supports high-end CPU and memory. Use for services or applications that require high performance. |


### Availability zone

NHN Cloud has divided the entire system into multiple availability zones to prepare for failures caused by physical hardware problems. Each of these availability zones has separate storage systems, network switches, surfaces, and power devices. Failures within one availability zone do not affect other availability zones, increasing the availability of the service as a whole. If you deploy instances across multiple availability zones, you can make your service more available.

Between the different availability zones, there are the following characteristics:

- Instances created across multiple availability zones can communicate with each other and are not charged for network usage.
- Block storage can be shared between instances created in the same availability zone, but block storage cannot be shared between different Availability Zones.
- You can share floating IPs across different availability zones. If one availability zone fails, you can quickly move the floating IP to another availability zone to minimize the time of failure.


### Key-pair

A keypair is an SSH public key and private key pair based on a public key infrastructure ([PKI](https://ko.wikipedia.org/wiki/%EA%B3%B5%EA%B0%9C_%ED%82%A4_%EA%B8%B0%EB%B0%98_%EA%B5%AC%EC%A1%B0), ). To access an instance created by NHN Cloud, you must use a keypair instead of ID/password authentication with keyboard input methods that are vulnerable to security. Users can use Keypair's private key to encode login information and send it to the instance to authenticate access to the instance, and then securely access the instance. For information on how to access an instance using a keypair, [see How](#_5)to Access an Instance.

Keypairs can be created in the NHN Cloud console when creating instances, or customers can register and use keypairs created by themselves. For information on how to register keypairs, [see Importing](./console-guide/#_16)Keypairs in the Console Guide.

> [Caution]
When you create a new keypair, you download the keypair's private key. The private key will not be issued twice, so please keep the downloaded private key on a secure disk or USB drive. If the private key is leaked to the outside, anyone can access the instance with the leaked private key and must be managed carefully.

### Security group

A security group is a virtual firewall that determines the network traffic that passes to your instances. For a detailed description of security groups, [see VPC overview](/Network/VPC/ko/overview/).

> [Note]
The default security group is designed to ignore all inbound network traffic from outside. When you connect to an instance by SSH, set the SSH port to open in the security group to which the instance belongs, and then connect to the instance.

### network

For your instance to communicate externally, it must be connected to at least one of the networks defined in your VPC. You cannot access instances that are not connected to the network. To create or change a new network, [see VPC overview](/Network/VPC/ko/overview/).

## billing

Instance billing is as follows:

* Instances are billed from the moment they are created.
* Instance base disks are billed separately from instances on a block storage basis.
* When an instance is stopped, we apply a 90% discount on the price of the site for 90 days. If the suspension status exceeds 90 days, it will transition to normal rates while remaining suspended.

For more information on billing, please refer to the service-specific [pricing page](https://www.toast.com/kr/service/compute/instance#price).

## How to access the instance

### How to Connect to a Linux Instance

To connect to a Linux instance, use an SSH client. If the instance's security group does not have an SSH access port (default 22) open, you cannot connect to it. For information on how to allow SSH access, see VPC Overview. If the instance does not have a floating IP assigned, it cannot be accessed from outside NHN Cloud. For information on how to assign a floating IP, [see VPC Overview](/Network/VPC/ko/overview/)](/Network/VPC/ko/overview/). [

#### How to connect to a Linux instance with an SSH client on Mac or Linux

Mac and Linux usually have an SSH client installed by default. Connect from an SSH client using the private key of the key pair as shown below.

CentOS Instances

	$ssh -i my_private_key.pem centos@<IPs of the instance>

Ubuntu Instances

	$ssh -i my_private_key.pem ubuntu@<IPs of the instance>

Debian Instances

	$ ssh -i my_private_key.pem debian@<IPs of the instance>

Rocky Instances

	$ssh -i my_private_key.pem rocky@<IPs of the instance>

#### How to connect to a Linux instance with the PuTTY SSH client on Windows

The PuTTY SSH client is a popular SSH client program on Windows. [Install PuTTY or iPuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) ](https://github.com/iPuTTY/iPuTTY/releases/tag/l0.70i)with [the Korean patch.

Connecting to a Linux instance with the PuTTY SSH client on Windows involves three steps.

* Change the private key of a keypair to the private key for PuTTY
* Registering a private key for PuTTY with PuTTY
* Connect to your instance with PuTTY


##### 1\. Change the private key of the keypair to the private key for PuTTY

PuTTY requires you to replace the keypair private key with PuTTY's private key format. Key translation uses puttygen, which is installed with PuTTY.

![Image1](http://static.toastoven.net/prod_instance/putty001.png)

**In the PuTTY Key Generator** dialog box, under the parameters**select RSA as the key format to generate, **and enter the key**bits to generate as the ** **default '2048' bits**. **** **Under Actions**  **** click the Load** button next to **Import Private Key File and load the private key file of the key pair.

![Image2](http://static.toastoven.net/prod_instance/putty002.png)

**Under Actions**  **** click the Save Private Key button next to Save** Generated Key to **save the converted keypair private key for PuTTY. If you save the private key with the key phrase blank, you are prompted to **Do you want to save this key without protecting it with the cipherphrase?** To store the converted private key more securely, set the cipher phrase**to save it. **

> [Caution]
To set up automatic login to your instance, you must not use a passphrase. If you use a passphrase, you must manually enter the password for the private key when you log in.

##### 2\. Register the private key for PuTTY with PuTTY

The private key for PuTTY can be registered and used in two ways.

* How to register and use an authentication private key file in PuTTY
* How to register and use the authentication private key file with pageant (PuTTY Authentication Agent)

**A. How to register and use an authentication private key file in PuTTY**


Launch PuTTY, and select **Connect > SSH > Auth**from the left ****category. Register the private key for PuTTY in the authentication private key file under Authentication ****  **parameters on the right.**

![Image3](http://static.toastoven.net/prod_instance/putty005.png)

If you save the access information after registering the private key, you do not need to re-register the private key file every time. For how to save access information, refer to the connection method below.


**B. How to register and use the authentication private key file with pageant (PuTTY Authentication Agent)**


When you run pageant, which is installed with PuTTY, an icon appears in the Windows tray as shown below. Right-click the pageant icon and **click the Add** Key menu to add a private key for PuTTY.

![Image4](http://static.toastoven.net/prod_instance/putty006.png)

To verify that the private key has been added, select View**Keys. If the key was added **successfully, you should see the added key as shown below.

![Image5](http://static.toastoven.net/prod_instance/putty008.png)

Once a pageant is executed, it remains in the Windows tray and runs, so you don't have to run it again every time you connect to the instance. However, if you have a fresh start of Windows, you must run it again.

##### 3\. Connect to your instance with PuTTY

If the converted private key for PuTTY is successfully registered, run PuTTY.

![Image6](http://static.toastoven.net/prod_instance/putty009.png)

Use the host name**of the basic access information **as follows.

CentOS

	centos@<IPs of the instance>

Ubuntu

	ubuntu@<IP of the instance>

Debian

	IP of the debian@< instance>

Rocky

	rocky@<IPs of the instance>

**Specify the SSH**default port of 22 for the port and SSH for the **connection** ****type.

If all the information is correct, save the session. Under Load, Save, Delete**Saved Session, write the name of the session you want to save in the field under the Saved section, and click the Save button to save the session. If you do not save the session, the private key settings registered in 2-A are also not retained. ** **** 

**Now **click Open to connect to the instance.


### How to connect to a Windows instance

To connect to a Windows server, select the Windows instance you want to access from the NHN Cloud console. On the Connection Information** tab of the instance details screen, click the Get Password button to confirm the password set for the **Windows server.**  **

The private key of the keypair entered in Confirm**Password is not sent to the server, and is only used to decrypt the password in the browser.**

Click the Connect** button next to Confirm Password to receive and run the .rdp file that stores the remote desktop access settings to **connect to the Windows server.** **The ID of the Windows server is Administrator`and the password is `the password confirmed in the NHN Cloud console.
