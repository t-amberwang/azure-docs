---
title: 'VPN client for OpenVPN protocol P2S connections: Azure AD authentication'
titleSuffix: Azure Virtual WAN
description: Learn how to use P2S VPN to connect to your VNet using Azure AD authentication.
services: virtual-wan
author: cherylmc

ms.service: virtual-wan
ms.topic: how-to
ms.date: 06/30/2022
ms.author: cherylmc

---
# Configure a VPN client for P2S OpenVPN protocol connections: Azure AD authentication

This article helps you configure a VPN client to connect using point-to-site VPN and Azure Active Directory authentication. Before you can connect and authenticate using Azure AD, you must first configure your Azure AD tenant. For more information, see [Configure an Azure AD tenant](openvpn-azure-ad-tenant.md).

> [!NOTE]
> Azure AD authentication is supported only for OpenVPN® protocol connections.
>

## <a name="profile"></a>Working with client profiles

For every computer that wants to connect to the VNet via the VPN client, you need to download the Azure VPN Client for the computer, and also configure a VPN client profile. If you want to configure multiple computers, you can create a client profile on one computer, export it, and then import it to other computers.

### To download the Azure VPN client

[!INCLUDE [Download Azure VPN client](../../includes/vpn-gateway-download-vpn-client.md)]

### <a name="cert"></a>To create a certificate-based client profile

When working with a certificate-based profile, make sure that the appropriate certificates are installed on the client computer. You can install and specify more than one certificate when using the Azure VPN client version 2.1963.44.0 or higher. For more information about certificates, see [Install client certificates](certificates-point-to-site.md).

![Screenshot showing certificates certificate authentication.](./media/openvpn-azure-ad-client/create/create-cert1.jpg)

### <a name="radius"></a>To create a RADIUS client profile

![Screenshot shows RADIUS connection client information.](./media/openvpn-azure-ad-client/create/create-radius1.jpg)
  
> [!NOTE]
> The Server Secret can be exported in the P2S VPN client profile. To export a client profile, see [User VPN client profiles](about-vpn-profile-download.md).
>

### <a name="export"></a>To export and distribute a client profile

Once you have a working profile and need to distribute it to other users, you can export it using the following steps:

1. Highlight the VPN client profile that you want to export, select the **...**, then select **Export**.

    ![Screenshot shows Export selected from the menu.](./media/openvpn-azure-ad-client/export/export1.jpg)

2. Select the location that you want to save this profile to, leave the file name as is, then select **Save** to save the xml file.

    ![Screenshot shows a Save As dialog box where you can enter a file name.](./media/openvpn-azure-ad-client/export/export2.jpg)

### <a name="import"></a>To import a client profile

1. On the page, select **Import**.

    ![Screenshot shows Import selected from the plus menu.](./media/openvpn-azure-ad-client/import/import1.jpg)

2. Browse to the profile xml file and select it. With the file selected, select **Open**.

    ![Screenshot shows an Open dialog box where you can select a file.](./media/openvpn-azure-ad-client/import/import2.jpg)

3. Specify the name of the profile and select **Save**.

    ![Screenshot shows the Connection Name added and the Save button selected.](./media/openvpn-azure-ad-client/import/import3.jpg)

4. Select **Connect** to connect to the VPN.

    ![Screenshot shows the Connect button for the for the connection you just created.](./media/openvpn-azure-ad-client/import/import4.jpg)

5. Once connected, the icon will turn green and say **Connected**.

    ![Screenshot shows the connection in a Connected status with the option to disconnect.](./media/openvpn-azure-ad-client/import/import5.jpg)

### <a name="delete"></a>To delete a client profile

1. Select the ellipses next to the client profile that you want to delete. Then, select **Remove**.

    ![Screenshot shows Remove selected from the menu.](./media/openvpn-azure-ad-client/delete/delete1.jpg)

2. Select **Remove** to delete.

    ![Screenshot shows a confirmation dialog box with the option to Remove or Cancel.](./media/openvpn-azure-ad-client/delete/delete2.jpg)

## <a name="connection"></a>Create a connection

1. On the page, select **+**, then **+ Add**.

    ![Screenshot shows Add selected from the plus menu.](./media/openvpn-azure-ad-client/create/create1.jpg)

2. Fill out the connection information. If you are unsure of the values, contact your administrator. After filling out the values, select **Save**.

    ![Screenshot shows pane where you can enter the required values.](./media/openvpn-azure-ad-client/create/create2.jpg)

3. Select **Connect** to connect to the VPN.

    ![Screenshot shows the Connect button for your connection.](./media/openvpn-azure-ad-client/create/create3.jpg)

4. Select the proper credentials, then select **Continue**.

    ![Screenshot shows the Sign in dialog box.](./media/openvpn-azure-ad-client/create/create4.jpg)

5. Once successfully connected, the icon will turn green and say **Connected**.

    ![Screenshot shows the connection in a Connected status.](./media/openvpn-azure-ad-client/create/create5.jpg)

### <a name="autoconnect"></a>To connect automatically

These steps help you configure your connection to connect automatically with Always-on.

1. On the home page for your VPN client, select **VPN Settings**.

    ![Screenshot shows V P N Connections where you can select V P N Settings.](./media/openvpn-azure-ad-client/auto/auto1.jpg)

2. Select **Yes** on the switch apps dialogue box.

    ![Screenshot shows a verification message about switching apps.](./media/openvpn-azure-ad-client/auto/auto2.jpg)

3. Make sure the connection that you want to set is not already connected, then highlight the profile and check the **Connect automatically** check box.

    ![Screenshot shows a Settings dialog box where you can select Connect automatically.](./media/openvpn-azure-ad-client/auto/auto3.jpg)

4. Select **Connect** to initiate the VPN connection.

    ![Screenshot shows the Connect button.](./media/openvpn-azure-ad-client/auto/auto4.jpg)

## <a name="diagnose"></a>Diagnose connection issues

1. To diagnose connection issues, you can use the **Diagnose** tool. Select the **...** next to the VPN connection that you want to diagnose to reveal the menu. Then select **Diagnose**.

    ![Screenshot shows Diagnose selected from the menu.](./media/openvpn-azure-ad-client/diagnose/diagnose1.jpg)

2. On the **Connection Properties** page, select **Run Diagnosis**.

    ![Screenshot shows the Run Diagnosis button for a connection.](./media/openvpn-azure-ad-client/diagnose/diagnose2.jpg)

3. Sign in with your credentials.

    ![Screenshot shows the Sign in dialog box for this action.](./media/openvpn-azure-ad-client/diagnose/diagnose3.jpg)

4. View the diagnosis results.

    ![Screenshot shows the results of the diagnosis.](./media/openvpn-azure-ad-client/diagnose/diagnose4.jpg)

## FAQ

### <a name="add-suffix"></a>How do I add DNS suffixes to the VPN client?

You can modify the downloaded profile XML file and add the **\<dnssuffixes>\<dnssufix> \</dnssufix>\</dnssuffixes>** tags.

```xml
<azvpnprofile>
<clientconfig>

    <dnssuffixes>
          <dnssuffix>.mycorp.com</dnssuffix>
          <dnssuffix>.xyz.com</dnssuffix>
          <dnssuffix>.etc.net</dnssuffix>
    </dnssuffixes>
    
</clientconfig>
</azvpnprofile>
```

### <a name="custom-dns"></a>How do I add custom DNS servers to the VPN client?

You can modify the downloaded profile XML file and add the **\<dnsservers>\<dnsserver> \</dnsserver>\</dnsservers>** tags.

```xml
<azvpnprofile>
<clientconfig>

	<dnsservers>
		<dnsserver>x.x.x.x</dnsserver>
        <dnsserver>y.y.y.y</dnsserver>
	</dnsservers>
    
</clientconfig>
</azvpnprofile>
```

> [!NOTE]
> The OpenVPN Azure AD client utilizes DNS Name Resolution Policy Table (NRPT) entries, which means DNS servers will not be listed under the output of `ipconfig /all`. To confirm your in-use DNS settings, please consult [Get-DnsClientNrptPolicy](/powershell/module/dnsclient/get-dnsclientnrptpolicy) in PowerShell.
>

### <a name="multi-cert"></a>Can I specify multiple certificates for the VPN client?

If you have 2 hubs for your virtual WAN that are each configured for P2S User VPN and use the same VPN configuration, and that configuration is configured to use multiple certificates, you can now configure the VPN clients for multiple certificates. This means that if one certificate can't be used for any reason, the other certificate can still be used for authentication. Previously, you couldn't configure the client with the settings for both certificates.

To configure, go to the Virtual WAN -> User VPN configurations page. Select the User VPN configuration used by both hubs, then select **Download virtual WAN user VPN profile** to download the global user VPN profile (rather than the hub profile). The files you download contain the root end certificates. You can configure multiple certificate support on the client side by either using the Azure VPN Client interface (version 2.1963.44.0 or higher), or by modifying the xml profile to include multiple certificate tags.

Example:

```xml
  </protocolconfig>
  <serverlist>
    <ServerEntry>
      <displayname
        i:nil="true" />
      <fqdn>wan.kycyz81dpw483xnf3fg62v24f.vpn.azure.com</fqdn>
    </ServerEntry>
  </serverlist>
  <servervalidation>
    <cert>
      <hash>A8985D3A65E5E5C4B2D7D66D40C6DD2FB19C5436</hash>
      <issuer
        i:nil="true" />
    </cert>
    <cert>
      <hash>59470697201baejC4B2D7D66D40C6DD2FB19C5436</hash>
      <issuer
        i:nil="true" />
    </cert>
    <cert>
      <hash>cab20a7f63f00f2bae76202gdfe36db3a03a9cb9</hash>
      <issuer
        i:nil="true" />
    </cert>
```

### <a name="custom-routes"></a>How do I add custom routes to the VPN client?

You can modify the downloaded profile XML file and add the **\<includeroutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</includeroutes>** tags.

```xml
<azvpnprofile>
<clientconfig>

	<includeroutes>
		<route>
			<destination>x.x.x.x</destination><mask>24</mask>
		</route>
	</includeroutes>
    
</clientconfig>
</azvpnprofile>
```

### <a name="force-tunneling"></a>How do I direct all traffic to the VPN tunnel (force tunnel)?

You can modify the downloaded profile XML file and add the **\<includeroutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</includeroutes>** tags.

```xml
<azvpnprofile>
<clientconfig>

	<includeroutes>
		<route>
			<destination>0.0.0.0</destination><mask>1</mask>
		</route>
		<route>
			<destination>128.0.0.0</destination><mask>1</mask>
		</route>
	</includeroutes>
    
</clientconfig>
</azvpnprofile>
```

### <a name="exclude-routes"></a>How do I block (exclude) routes from the VPN client?

You can modify the downloaded profile XML file and add the **\<excluderoutes>\<route>\<destination>\<mask> \</destination>\</mask>\</route>\</excluderoutes>** tags.

```xml
<azvpnprofile>
<clientconfig>

	<excluderoutes>
		<route>
			<destination>x.x.x.x</destination><mask>24</mask>
		</route>
	</excluderoutes>
    
</clientconfig>
</azvpnprofile>
```

### <a name="import-profile"></a>Can I import the profile from a command-line prompt?

You can import the profile from a command-line prompt by placing the downloaded **azurevpnconfig.xml** file in the **%userprofile%\AppData\Local\Packages\Microsoft.AzureVpn_8wekyb3d8bbwe\LocalState** folder and running the following command:

```xml
azurevpn -i azurevpnconfig.xml 
```
To force the import, use the **-f** switch.


## Next steps

For more information, see [Create an Azure Active Directory tenant for P2S Open VPN connections that use Azure AD authentication](openvpn-azure-ad-tenant.md).
