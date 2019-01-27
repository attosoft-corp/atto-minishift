# MiniShift setup on Windows: OpenShift on Windows


[**OpenShift**](https://www.openshift.com/) is a great PaaS platform by **Red Hat** that leverages container technologies such as **[Docker](https://www.docker.com/)** and [**Kubernetes**](https://kubernetes.io/). If you want to try OpenShift but don’t want to **set up a real, full-blown cluster** this solution is for you. Minishift is a great way to **test OpenShift** capabilities without committing hardware to it. By using MiniShift you will set up a **virtual machine** on your hardware, this vm will be your very own **one-machine cluster** and when you’re done you can simply throw it away.  

## Why OpenShift on Windows?

OpenShift, Docker Kubernets are all Linux-based solutions, made for and battle-tested on Linux. Installing **OpenShift on Windows** might seem strange, but it’s not. Well, most of the times OpenShift is installed on Windows just **for testing or proof of concept purposes**

By installing MiniShift you will essentially download and install a Linux virtual machine configured with OpenShift, it is hence **highly discouraged to use it in production**.

## Requirements

*   You need a machine capable of performing [Virtualization].
*   If you want to use **HyperV**, you need a compatible Windows edition (e.g. **Windows 10 Pro**. Windows 10 Home can’t.)
*   At least **4GB** of RAM (suggested).

## MiniShift on Windows: HyperV or VirtualBox

The first thing you will need in order to begin is a **hypervisor** to run the **Minishift virtual machine**, you can either use:

*   [**HyperV**](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)**:** the native Windows hypervisor.
*   **[VirtualBox](https://www.virtualbox.org/wiki/Downloads):** an open source hypervisor by Oracle available on many operating systems.

Although the **suggested hypervisor** is **VirtualBox** you should be able to install it using **HyperV** without major issues, and by default Minishift will try to use the latter. In this tutorial you can use either one, **I will assume you already have your hypervisor installed and running**.

## Getting MiniShift and setting environment

Let’s start!

*   **First:** [download](https://github.com/minishift/minishift/releases/latest) the Minishift executable, pick the one for Windows. The link takes you to the latest version, at the moment of writing this article the latest version was **v1.30.0**.
*   **Second:** **extract** the content of the folder in a subdirectory of **C:\** it’s best to avoid other drives/network drives. I suggest you to extract it in the **C:\minishift** subdirectory.
*   **Third:** add the path you chose to the **PATH** [environment variable](https://msdn.microsoft.com/en-us/library/windows/desktop/ms682653(v=vs.85).aspx). You can do so graphically or using the following **PowerShell** command:
Replace **C:\minishift** with the path you chose during the second step. Now that you have set the environment up, it’s time to **install**!

## Installing MiniShift

With the environment set, you’re just a few steps away from installing and using Minishift. Pick the steps associated with your hypervisor and open an **elevated** [PowerShell prompt](https://docs.microsoft.com/en-us/powershell/scripting/setup/starting-windows-powershell?view=powershell-5.1):

Before you actually do anything you must be part of the **HyperV Administrators group**. If you’re using a different language you will need to **replace Hyper-V Administrators** with the corresponding group in your system’s language.

Next you will need to [create an External switch](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/connect-to-network), your VMs will need it to connect to the internet. Follow [these steps by Microsoft to create the External switch](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/connect-to-network), be sure to pick External as type.

Now you need to **set the environment variable** to tell Minishift which **switch** to use. Replace the value (in this case **External**) with the name you chose for the switch earlier.


Set up **HyperV as default driver**, this will prevent Minishift from using VirtualBox and [breaking your computer](https://www.virtualbox.org/ticket/16801):

`PS> minishfit config set vm-driver hyperv`


Now you can start the installation:


`PS> minishift start`

Image pull complete
OpenShift server started.

The server is accessible via web console at:
    https://10.0.0.240:8443

To login as administrator:
    oc login -u system:admin</pre>

## Enjoy OpenShift with MiniShift

Congratulations! You just installed minishift! You can now type **minishift console**
 to **open the Web UI in your default browser**! Don’t worry about the insecure connection, that’s just because the certificate is **self-signed**.

[![OpenShift Web Login](/content/OpenShift-Web-Login.png)](/content/OpenShift-Web-Login.png)

OpenShift Web Login

</div>

Once logged:

[![OpenShift Web Console](/content/OpenShift-Web-Console.png)](/content/OpenShift-Web-Console.png)

## Accessing OpenShift

Now that you have OpenShift up and running, you can use the **Web UI** as well as the **oc command line utility** to interact with your OpenShift installation. Remember you still have the **minishift** executable that you can use to control the **OpenShift vm**.

### Starting OpenShift

`PS> minishift start`

### Stopping OpenShift

`PS> minishift stop`

### Deleting (erasing completely) OpenShift

`PS> minishift delete`
You are deleting the Minishift VM: 'minishift'. Do you want to continue [y/N]?: y
Deleting the Minishift VM...
Minishift VM deleted.
