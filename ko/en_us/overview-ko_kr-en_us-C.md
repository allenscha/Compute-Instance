## Compute > Instance > Overview


An instance is a virtual server composed of virtual CPUs, memory, and basic disks. The customer's service or application is installed on this server and various services provided by NHN Cloud are used in combination.

## instance components

The elements that make up an instance are as follows:

- **Image**: A virtual disk containing the instance's operating system
- **Type** (flavor): The instance's virtual hardware performance
- **Availability zone** (AZ, availability zone): The physical location where the instance will be created
- **Key-pair: A key used as a means of connecting to an instance**
- **security group**: Network security settings for the instance
- **Network**: The virtual network that the instance will connect to

Depending on this information, the instance's properties and usage will change. Of this information, settings other than the image and availability zone can be changed even after the instance is created, but some instance types (flavors) cannot be changed after the instance has been created. For details on changing the instance type, see [Changing the Instance Type in the Console User Guide](./console-guide/#_15).

### images

An image is a virtual disk containing an operating system. NHN Cloud currently supports CentOS, Debian, Ubuntu, Rocky, and Windows. For more supported operating system versions[, see NHN Cloud (NHN Cloud) Service Overview](https://toast.com/service/compute/instance).

All images are set to run optimally on the instance's virtual hardware, and are safe to use because they have been verified for security by NHN Cloud. For a detailed description of the [image, see the image overview](/Compute/Image/ko/overview/).

### Instance flavor

NHN Cloud provides a variety of instance types to suit the customer's usage. You can create an instance of the appropriate type according to the characteristics of the service or application to be operated. The type of an instance that has already been created can also be easily changed in the web console.

| type    | illustrative |
| ------- | -------------------------------------------------|
| m2 | It is a type with balanced settings for CPU and memory. It is used when the performance requirements of a service or application are unclear. |
| c2 | This is an instance type with the CPU performance set to high. It is used for web application servers or analytics systems that require high computational performance. |
| r2 | It can be used when memory usage is high compared to other resources. It is usually used for memory databases or cache servers. |
| t2 | This is a low cost instance. It is used on servers that do not have a high workload. |
| u2 | This is the least expensive instance. It is used on servers that do not have a high workload.<br>Because it uses a local disk, it's relatively less reliable than other instances, but it's affordable.<br>This type of instance does not guarantee I/O performance. |
| x1 | It is a type that supports high-specification CPUs and memory. It is used for services or applications that require high performance. |


### Availability zone

NHN Cloud divided the entire system into multiple availability zones to prepare for failures caused by physical hardware issues. Storage systems, network switches, surfaces, and power devices are all configured separately for each of these availability zones. Failures within one availability zone do not affect other availability zones, increasing the availability of the service as a whole. You can further increase the availability of services by deploying instances in multiple availability zones.

The following characteristics exist between the different availability zones:

- Network communication is possible between instances created by being scattered across multiple availability zones, and network usage costs incurred at this time are not charged.
- Block storage can be shared between instances created in the same availability zone, but block storage cannot be shared between different availability zones.
- Floating IPs can be shared across different availability zones. If a failure occurs in one availability zone, floating IPs can be quickly moved to another availability zone to minimize failure time.


### Key-pair (key-pair)

A keypair is an SSH public key and private key pair based on public key infrastructure ([PKI](https://ko.wikipedia.org/wiki/%EA%B3%B5%EA%B0%9C_%ED%82%A4_%EA%B8%B0%EB%B0%98_%EA%B5%AC%EC%A1%B0), public key infrastructure). To connect to an instance created by NHN Cloud, you must use a keypair instead of ID/password authentication using a keyboard input method that is weak in security. Users can securely connect to the instance after receiving connection authentication by encoding login information using the keypair's private key and sending it to the instance. For how to connect to an instance using a [keypair, see How to](#_5) connect to an instance.

When creating an instance, a new keypair can be created on the NHN Cloud console, or a customer can register and use a keypair created by themselves. For how to register a keypair, see [Importing a keypair in the console guide](./console-guide/#_16).

> [Attention]
When you create a new keypair, you download the keypair's private key. The private key will not be issued twice, so please keep the downloaded private key on a secure disk or USB drive. If a private key is leaked to the outside world, anyone can access the instance with the leaked private key, so care must be taken.

### Security group (Security group)

A security group is a virtual firewall that determines the network traffic that is delivered to an instance. For a detailed description of security groups, see [VPC Overview](/Network/VPC/ko/overview/).

> [Note]
The default security group is designed to ignore all inbound (inbound) network traffic from outside. When connecting to an instance via SSH, set the security group to which the instance belongs to open an SSH port, and then connect to the instance.

### networks

For an instance to communicate with the outside world, it must be connected to at least one of the networks defined in the VPC. You can't access instances that aren't connected to a network. To create a new network or make changes to it, see [VPC Overview](/Network/VPC/ko/overview/).

## Billing

The instance billing method is as follows:

* You are billed the moment you create an instance.
* Instance basic disks are billed separately from the instance on a block storage basis.
* When an instance is stopped, a 90% discount on the homepage rate is applied for 90 days. If the suspension status exceeds 90 days, it will remain suspended and revert to normal rates.

For more details on billing, see the service-specific [pricing page](https://www.toast.com/kr/service/compute/instance#price).

## How to connect to an instance

### How to connect to a Linux instance

Use an SSH client to connect to the Linux instance. If the instance's security group doesn't have an SSH access port open (default value 22), you won't be able to connect. See [VPC Overview](/Network/VPC/ko/overview/) for information on how to allow SSH access. If the instance does not have a floating IP assigned to it, it cannot be reached from outside of NHN Cloud. See [VPC Overview](/Network/VPC/ko/overview/) for how to allocate floating IPs.

#### How to connect to a Linux instance using an SSH client on Mac or Linux

Macs and Linux usually have an SSH client installed by default. In an SSH client, connect using the keypair's private key as shown below.

CentOS instance

	$ssh -i my_private_key.pem centos@<인스턴스의 IP>

Ubuntu instance

	$ssh -i my_private_key.pem ubuntu@<인스턴스의 IP>

Debian instance

	$ssh -i my_private_key.pem debian@<인스턴스의 IP>

Rocky instance

	$ssh -i my_private_key.pem rocky@<인스턴스의 IP>

#### How to connect to a Linux instance with the PuTTY SSH client on Windows

PuTTY SSH Client is a popular SSH client program for Windows. Install [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) or [iPutty](https://github.com/iPuTTY/iPuTTY/releases/tag/l0.70i) with the Hangul patch.

To connect to a Linux instance with the PuTTY SSH client on Windows, there are three steps.

* Change the keypair's private key to a private key for PuTTY
* Register your private key for PuTTY in PuTTY
* Connect to an instance with PuTTY


##### 1\. Change the keypair's private key to a private key for PuTTY

PuTTY requires you to use the keypair private key in PuTTY's private key format. Key conversion uses puttygen, which is installed with PuTTY.

![image 1](http://static.toastoven.net/prod_instance/putty001.png)

In the **parameters** at the bottom of the **PuTTY Key Generator** dialog box, select **RSA** as the **key format** to be **generated, and enter the key bits** to be generated using the default '2048' bits. Click the **Load button next to Import Private Key File** under **Actions** to **load** the private key file for the key pair.

![image 2](http://static.toastoven.net/prod_instance/putty002.png)

**Save the converted keypair **private key for PuTTY by clicking the Save** private key button next to Save the generated** key under **Actions**. If you **save a** private key with the key passphrase blank, do you want to save this key without protecting the**passphrase? The message** appears. To store the converted private key more securely, set a passphrase and save it.

> [Attention]
If you want to set up automatic login to the instance, you must not use a passphrase. If you use a passphrase, you must manually enter the password for the private key when you log in.

##### 2\. Register your private key for PuTTY in PuTTY

The private key for PuTTY created in this way can be registered and used in 2 ways.

* How to register and use an authentication private key file in PuTTY
* How to register and use an authentication private key file with pageant (PuTTY authentication agent)

**A. How to register and use an authentication private key file in PuTTY**


Launch PuTTY and select **Connect > SSH > Auth** from the left **category**. Register the private key for PuTTY in the **authentication private key file** under the authentication **parameters** on the right.

![image 3](http://static.toastoven.net/prod_instance/putty005.png)

After registering a private key, if you save the connection information, there is no need to re-register the private key file each time. For how to save connection information, see the following connection method.


**B. How to register and use an authentication private key file with pageant (PuTTY authentication agent)**


When you run pageant, which is installed with PuTTY, an icon appears in the Windows tray as shown below. Right-click the pageant icon and click the **Add Key** menu to add a private key for PuTTY.

![image 4](http://static.toastoven.net/prod_instance/putty006.png)

To confirm that the private **key has been added, select View key**. If the key was successfully added, you'll see the added key as shown in the image below.

![image 5](http://static.toastoven.net/prod_instance/putty008.png)

Once you run pageant, it stays running in the Windows tray, so you don't need to run it again every time you connect to the instance. However, if you start Windows from scratch, you will need to run it again.

##### 3\. Connect to an instance with PuTTY

If the private key converted for PuTTY has been successfully registered, run PuTTY.

![image 6](http://static.toastoven.net/prod_instance/putty009.png)

The **host name** in the basic connection information is used as follows:

CentOS

	centos@<인스턴스의 IP>

Ubuntu

	ubuntu@<인스턴스의 IP>

Debian

	debian@<인스턴스의 IP>

Rocky

	rocky@<인스턴스의 IP>

The **port** is set to 22, which is the default SSH port, and the **connection type** is set to **SSH**.

If all information is correct, save the session. Under **Load, Save, Delete Saved Sessions**, write the name of the session you want to save in the field under the Saved section, and click the **Save** button to save the session. If the session is not saved, the private key settings registered in 2-A will not be retained.

Now click **Open** to connect to the instance.


### How to connect to a Windows instance

To connect to a Windows server, select the Windows instance you want to connect to from the NHN Cloud console. Click the **Confirm Password** button on the **Connection Information** tab of the instance details screen to check the password set on the Windows server.

The private key in the keypair entered in **Confirm Password** is not sent to the server; it is only used to decrypt the password in the browser.

Click the **Connect** button next to **Confirm Password** to get the.rdp file containing the remote desktop connection settings and run it to connect to the Windows server. The ID of the Windows server is `Administrator`, and the password confirmed on the NHN Cloud console is used.
