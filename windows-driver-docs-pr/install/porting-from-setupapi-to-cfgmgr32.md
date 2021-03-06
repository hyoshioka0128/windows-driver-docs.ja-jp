---
title: SetupApi から CfgMgr32 へのコードの移植
description: このトピックでは、Cfgmgr32.dll を代わりに使用する Setupapi.dll 機能を使用するコードを移植する方法を示すコード例を提供します。
ms.assetid: 36668A17-EA56-464C-A38B-C75BE2359412
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 349a5675d3ad904338599745032041a5f0f0675c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385019"
---
# <a name="porting-code-from-setupapi-to-cfgmgr32"></a>SetupApi から CfgMgr32 へのコードの移植


このトピックでは、Cfgmgr32.dll を代わりに使用する Setupapi.dll 機能を使用するコードを移植する方法を示すコード例を提供します。 コードの移植で、ユニバーサル Windows プラットフォーム (UWP)、SetupApi をサポートしていないコードを実行することができます。 UWP の CfgMgr32 のサブセットがサポートされている、を通じて公開される機能では具体的には、 `api-ms-win-devices-config-l1-1-0.dll` API (Windows 8 以降) を設定または`api-ms-win-devices-config-l1-1-1.dll`API (Windows 8.1 以降) を設定します。 Windows 10 以降では、単にリンクする`onecore.lib`します。

上記の API のセット内の関数の一覧についてを参照してください[Windows API のセット](https://docs.microsoft.com/windows/desktop/apiindex/windows-apisets)または[Onecore.lib:Api api-ms-win-devices-config-l1-1-1.dll から](https://docs.microsoft.com/windows/desktop/apiindex/umbrella-lib-onecore#_api-ms-win-devices-config-l1-1-1.dll)します。

次のセクションでには、通常、アプリケーションを使用したコード例が含まれます。

-   [存在するデバイスの一覧を取得し、各デバイスのプロパティを取得](#get-a-list-of-present-devices-and-retrieve-a-property-for-each-device)
-   [インターフェイスの一覧を取得、デバイスが、各インターフェイスを公開して、デバイスからプロパティを取得します。](#get-a-list-of-interfaces-get-the-device-exposing-each-interface-and-get-a-property-from-the-device)
-   [特定のデバイスからプロパティを取得します。](#get-a-property-from-a-specific-device)
-   [デバイスを無効にします。](#disable-device)
-   [デバイスを有効にします。](#enable-device)
-   [デバイスを再起動します。](#restart-device)

## <a name="get-a-list-of-present-devices-and-retrieve-a-property-for-each-device"></a>存在するデバイスの一覧を取得し、各デバイスのプロパティを取得


この例を使用して存在するすべてのデバイスの一覧を取得します。 [ **SetupDiGetClassDevs** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)反復を各デバイスのデバイスの説明を取得できます。

```ManagedCPlusPlus
VOID
GetDevicePropertiesSetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVINFO_DATA DeviceInfoData;
    DWORD Index;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiGetClassDevs(NULL,
                                        NULL,
                                        NULL,
                                        DIGCF_ALLCLASSES | DIGCF_PRESENT);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
    DeviceInfoData.cbSize = sizeof(DeviceInfoData);

    for (Index = 0;
         SetupDiEnumDeviceInfo(DeviceInfoSet,
                               Index,
                               &DeviceInfoData);
         Index++)
    {
        // Query a property on the device.  For example, the device description.
        if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                      &DeviceInfoData,
                                      &DEVPKEY_Device_DeviceDesc,
                                      &PropertyType,
                                      (PBYTE)DeviceDesc,
                                      sizeof(DeviceDesc),
                                      NULL,
                                      0))
        {
            // The error can be retrieved with GetLastError();
            continue;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            continue;
        }
    }

    if (GetLastError() != ERROR_NO_MORE_ITEMS)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

この例を使用して存在するすべてのデバイスの一覧を取得します。 [ **CM_Get_Device_ID_List** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista)反復を各デバイスのデバイスの説明を取得できます。

```ManagedCPlusPlus
VOID
GetDevicePropertiesCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    PWSTR DeviceList = NULL;
    ULONG DeviceListLength = 0;
    PWSTR CurrentDevice;
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;
    DWORD Index = 0;

    cr = CM_Get_Device_ID_List_Size(&DeviceListLength,
                                    NULL,
                                    CM_GETIDLIST_FILTER_PRESENT);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    DeviceList = (PWSTR)HeapAlloc(GetProcessHeap(),
                                  HEAP_ZERO_MEMORY,
                                  DeviceListLength * sizeof(WCHAR));

    if (DeviceList == NULL) {
        goto Exit;
    }

    cr = CM_Get_Device_ID_List(NULL,
                               DeviceList,
                               DeviceListLength,
                               CM_GETIDLIST_FILTER_PRESENT);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    for (CurrentDevice = DeviceList;
         *CurrentDevice;
         CurrentDevice += wcslen(CurrentDevice) + 1)
    {

        // If the list of devices also includes non-present devices,
        // CM_LOCATE_DEVNODE_PHANTOM should be used in place of
        // CM_LOCATE_DEVNODE_NORMAL.
        cr = CM_Locate_DevNode(&Devinst,
                               CurrentDevice,
                               CM_LOCATE_DEVNODE_NORMAL);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        PropertySize = sizeof(DeviceDesc);
        cr = CM_Get_DevNode_Property(Devinst,
                                     &DEVPKEY_Device_DeviceDesc,
                                     &PropertyType,
                                     (PBYTE)DeviceDesc,
                                     &PropertySize,
                                     0);

        if (cr != CR_SUCCESS)
        {
            Index++;
            continue;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            Index++;
            continue;
        }

        Index++;
    }

  Exit:

    if (DeviceList != NULL)
    {
        HeapFree(GetProcessHeap(),
                 0,
                 DeviceList);
    }

    return;
}
```

## <a name="get-a-list-of-interfaces-get-the-device-exposing-each-interface-and-get-a-property-from-the-device"></a>インターフェイスの一覧を取得、デバイスが、各インターフェイスを公開して、デバイスからプロパティを取得します。


この例は、GUID_DEVINTERFACE_VOLUME を使用してクラスのすべてのインターフェイスの一覧を取得します。 [ **SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)します。 インターフェイスごとには、インターフェイスを公開するデバイスを取得し、そのデバイスのプロパティを取得します。

```ManagedCPlusPlus
VOID
GetInterfacesAndDevicePropertySetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVICE_INTERFACE_DATA DeviceInterfaceData;
    SP_DEVINFO_DATA DeviceInfoData;
    DWORD Index;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiGetClassDevs(&GUID_DEVINTERFACE_VOLUME,
                                        NULL,
                                        NULL,
                                        DIGCF_DEVICEINTERFACE);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInterfaceData, sizeof(DeviceInterfaceData));
    DeviceInterfaceData.cbSize = sizeof(DeviceInterfaceData);

    for (Index = 0;
         SetupDiEnumDeviceInterfaces(DeviceInfoSet,
                                     NULL,
                                     &GUID_DEVINTERFACE_VOLUME,
                                     Index,
                                     &DeviceInterfaceData);
         Index++)
    {

        ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
        DeviceInfoData.cbSize = sizeof(DeviceInfoData);

        if ((!SetupDiGetDeviceInterfaceDetail(DeviceInfoSet,
                                              &DeviceInterfaceData,
                                              NULL,
                                              0,
                                              NULL,
                                              &DeviceInfoData)) &&
            (GetLastError() != ERROR_INSUFFICIENT_BUFFER))
        {
            // The error can be retrieved with GetLastError();
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                      &DeviceInfoData,
                                      &DEVPKEY_Device_DeviceDesc,
                                      &PropertyType,
                                      (PBYTE)DeviceDesc,
                                      sizeof(DeviceDesc),
                                      NULL,
                                      0))
        {
            // The error can be retrieved with GetLastError();
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }
    }

    if (GetLastError() != ERROR_NO_MORE_ITEMS)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

この例は、GUID_DEVINTERFACE_VOLUME を使用してクラスのすべてのインターフェイスの一覧を取得します。 [ **CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)します。 インターフェイスごとには、インターフェイスを公開するデバイスを取得し、そのデバイスのプロパティを取得します。

```ManagedCPlusPlus
VOID
GetInterfacesAndDevicePropertyCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    PWSTR DeviceInterfaceList = NULL;
    ULONG DeviceInterfaceListLength = 0;
    PWSTR CurrentInterface;
    WCHAR CurrentDevice[MAX_DEVICE_ID_LEN];
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;
    DWORD Index = 0;

    do {
        cr = CM_Get_Device_Interface_List_Size(&DeviceInterfaceListLength,
                                               (LPGUID)&GUID_DEVINTERFACE_VOLUME,
                                               NULL,
                                               CM_GET_DEVICE_INTERFACE_LIST_ALL_DEVICES);

        if (cr != CR_SUCCESS)
        {
            break;
        }

        if (DeviceInterfaceList != NULL) {
            HeapFree(GetProcessHeap(),
                     0,
                     DeviceInterfaceList);
        }

        DeviceInterfaceList = (PWSTR)HeapAlloc(GetProcessHeap(),
                                               HEAP_ZERO_MEMORY,
                                               DeviceInterfaceListLength * sizeof(WCHAR));

        if (DeviceInterfaceList == NULL)
        {
            cr = CR_OUT_OF_MEMORY;
            break;
        }

        cr = CM_Get_Device_Interface_List((LPGUID)&GUID_DEVINTERFACE_VOLUME,
                                          NULL,
                                          DeviceInterfaceList,
                                          DeviceInterfaceListLength,
                                          CM_GET_DEVICE_INTERFACE_LIST_ALL_DEVICES);
    } while (cr == CR_BUFFER_SMALL);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    for (CurrentInterface = DeviceInterfaceList;
         *CurrentInterface;
         CurrentInterface += wcslen(CurrentInterface) + 1)
    {

        PropertySize = sizeof(CurrentDevice);
        cr = CM_Get_Device_Interface_Property(CurrentInterface,
                                              &DEVPKEY_Device_InstanceId,
                                              &PropertyType,
                                              (PBYTE)CurrentDevice,
                                              &PropertySize,
                                              0);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }

        // Since the list of interfaces includes all interfaces, enabled or not, the
        // device that exposed that interface may currently be non-present, so
        // CM_LOCATE_DEVNODE_PHANTOM should be used.
        cr = CM_Locate_DevNode(&Devinst,
                               CurrentDevice,
                               CM_LOCATE_DEVNODE_PHANTOM);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        // Query a property on the device.  For example, the device description.
        PropertySize = sizeof(DeviceDesc);
        cr = CM_Get_DevNode_Property(Devinst,
                                     &DEVPKEY_Device_DeviceDesc,
                                     &PropertyType,
                                     (PBYTE)DeviceDesc,
                                     &PropertySize,
                                     0);

        if (cr != CR_SUCCESS)
        {
            goto Exit;
        }

        if (PropertyType != DEVPROP_TYPE_STRING)
        {
            goto Exit;
        }

        Index++;
    }

  Exit:

    if (DeviceInterfaceList != NULL)
    {
        HeapFree(GetProcessHeap(),
                 0,
                 DeviceInterfaceList);
    }

    return;
}
```

## <a name="get-a-property-from-a-specific-device"></a>特定のデバイスからプロパティを取得します。


この例では、特定のデバイスのデバイス インスタンス パスを受け取り、を使用してから、プロパティを取得[ **SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)します。

```ManagedCPlusPlus
VOID
GetDevicePropertySpecificDeviceSetupapi(
    VOID
    )
{
    HDEVINFO DeviceInfoSet = INVALID_HANDLE_VALUE;
    SP_DEVINFO_DATA DeviceInfoData;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;

    DeviceInfoSet = SetupDiCreateDeviceInfoList(NULL, NULL);

    if (DeviceInfoSet == INVALID_HANDLE_VALUE)
    {
        goto Exit;
    }

    ZeroMemory(&DeviceInfoData, sizeof(DeviceInfoData));
    DeviceInfoData.cbSize = sizeof(DeviceInfoData);

    if (!SetupDiOpenDeviceInfo(DeviceInfoSet,
                               MY_DEVICE,
                               NULL,
                               0,
                               &DeviceInfoData))
    {
        // The error can be retrieved with GetLastError();
        goto Exit;
    }

    // Query a property on the device.  For example, the device description.
    if (!SetupDiGetDeviceProperty(DeviceInfoSet,
                                  &DeviceInfoData,
                                  &DEVPKEY_Device_DeviceDesc,
                                  &PropertyType,
                                  (PBYTE)DeviceDesc,
                                  sizeof(DeviceDesc),
                                  NULL,
                                  0)) {
        // The error can be retrieved with GetLastError();
        goto Exit;
    }

    if (PropertyType != DEVPROP_TYPE_STRING)
    {
        goto Exit;
    }

  Exit:

    if (DeviceInfoSet != INVALID_HANDLE_VALUE)
    {
        SetupDiDestroyDeviceInfoList(DeviceInfoSet);
    }

    return;
}
```

この例では、特定のデバイスのデバイス インスタンス パスを受け取り、を使用してから、プロパティを取得[ **CM_Get_DevNode_Property**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_propertyw)します。

```ManagedCPlusPlus
void
GetDevicePropertySpecificDeviceCfgmgr32(
    VOID
    )
{
    CONFIGRET cr = CR_SUCCESS;
    DEVINST Devinst;
    WCHAR DeviceDesc[2048];
    DEVPROPTYPE PropertyType;
    ULONG PropertySize;

    // If MY_DEVICE could be a non-present device, CM_LOCATE_DEVNODE_PHANTOM
    // should be used in place of CM_LOCATE_DEVNODE_NORMAL.
    cr = CM_Locate_DevNode(&Devinst,
                           MY_DEVICE,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    // Query a property on the device.  For example, the device description.
    PropertySize = sizeof(DeviceDesc);
    cr = CM_Get_DevNode_Property(Devinst,
                                 &DEVPKEY_Device_DeviceDesc,
                                 &PropertyType,
                                 (PBYTE)DeviceDesc,
                                 &PropertySize,
                                 0);

    if (cr != CR_SUCCESS)
    {
        goto Exit;
    }

    if (PropertyType != DEVPROP_TYPE_STRING)
    {
        goto Exit;
    }

  Exit:

    return;
}
```

## <a name="disable-device"></a>デバイスを無効にします。


この例では、CfgMgr32 を使用してデバイスを無効にする方法を示します。 これには、SetupApi には使用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)で*InstallFunction*の**DIF_PROPERTYCHANGE**、指定する**DICS_DISABLE**します。

**注**既定では、呼び出す[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)再起動後に無効になっているデバイスの状態になります。 呼び出すときに、再起動後にデバイスを無効にする[ **CM_Disable_DevNode**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_disable_devnode)を指定する必要があります、 **CM_DISABLE_PERSIST**フラグ。



```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Disable_DevNode(devinst, 0);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```

## <a name="enable-device"></a>デバイスを有効にします。


この例では、CfgMgr32 を使用してデバイスを有効にする方法を示します。 これには、SetupApi には使用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)で*InstallFunction*の**DIF_PROPERTYCHANGE**、指定する**DICS_ENABLE**します。

```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Enable_DevNode(devinst, 0);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```

## <a name="restart-device"></a>デバイスを再起動します。


この例では、CfgMgr32 を使用してデバイスを再起動する方法を示します。 これには、SetupApi には使用[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)で*InstallFunction*の**DIF_PROPERTYCHANGE**、指定する**DICS_PROPCHANGE**します。

```ManagedCPlusPlus
    cr = CM_Locate_DevNode(&devinst,
                           (DEVINSTID_W)DeviceInstanceId,
                           CM_LOCATE_DEVNODE_NORMAL);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Query_And_Remove_SubTree(devinst,
                                     NULL,
                                     NULL,
                                     0,
                                     CM_REMOVE_NO_RESTART);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }

    cr = CM_Setup_DevNode(devinst,
                          CM_SETUP_DEVNODE_READY);

    if (cr != CR_SUCCESS) {
        goto Exit;
    }
```









