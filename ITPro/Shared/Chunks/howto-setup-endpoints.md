<properties writer="kathydav" editor="tysonn" manager="jeffreyg" />

#How to Set Up Endpoints to a Virtual Machine

All virtual machines that you create in Windows Azure can automatically communicate using a private network channel with other virtual machines in the same cloud service or virtual network. However, other resources on the Internet or other virtual networks require endpoints to handle the inbound network traffic to the virtual machine. 

When you create a virtual machine in the Management Portal, you can create these endpoints, such as for Remote Desktop, Windows PowerShell Remoting, or Secure Shell (SSH). After you create the virtual machine, you can create additional endpoints as needed. 

**Note**: If you want to connect to your virtual machines directly by hostname or set up cross-premises connections, see [Windows Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).

Each endpoint has a public port and a private port:

- The private port is used internally by the virtual machine to listen for traffic on that endpoint.

- The public port is used by the Windows Azure load balancer to communicate with the virtual machine from external resources. After you create an endpoint, you can use a network access control list (ACL) to define rules that help isolate and control the incoming traffic on the public port. For more information, see [About Network Access Control Lists](http://go.microsoft.com/fwlink/p/?LinkId=303816).

Default values for the ports and protocol for these endpoints are provided when the endpoints are created through the Management Portal. For all other endpoints, you specify the ports and protocol when you create the endpoint. Resources can connect to an endpoint by using either the TCP or UDP protocol. The TCP protocol includes HTTP and HTTPS communication.  

###Create an Endpoint###


1. If you have not already done so, sign in to the [Windows Azure Management Portal](http://manage.windowsazure.com).

2. Click **Virtual Machines**, and then select the virtual machine that you want to configure.

3. Click **Endpoints**. The Endpoints page lists all endpoints for the virtual machine.

	![Endpoints] (../media/endpointswindows.png)

4.	Click **Add**.

	The **Add Endpoint** dialog box appears. Choose whether to add the endpoint to a load-balanced set and then click the arrow to continue.
	
6. In **Name**, type a name for the endpoint.

7. In protocol, specify either **TCP** or **UDP**.

8. In **Public Port** and **Private Port**, type port numbers that you want to use. These port numbers can be different. The public port is the entry point for communication from outside of Windows Azure and is used by the Windows Azure load balancer. You can use the private port and firewall rules on the virtual machine to redirect traffic in a way that is appropriate for your application.

9. Click **Create a load-balancing set** if this endpoint will be the first one in a load-balanced set. Then, on the **Configure the load-balanced set** page, specify a name, protocol, and probe details. Load-balanced sets require a probe so the health of the set can be monitored. For more information, see [Load Balancing Virtual Machines](http://www.windowsazure.com/en-us/manage/windows/common-tasks/how-to-load-balance-virtual-machines/).  

10.	Click the check mark to create the endpoint.

	You will now see the endpoint listed on the **Endpoints** page.

	![Endpoint creation successful] (../media/endpointwindowsnew.png)






