---
title: デバイス インターフェイスの使用
description: デバイス インターフェイスの使用
ms.assetid: 98199220-947e-462e-a50c-85d81ca50108
keywords:
- デバイスインターフェイス WDK KMDF
- デバイスインターフェイス WDK KMDF の登録
- デバイスインターフェイスアクセス要求の受信 (WDK KMDF)
- デバイスインターフェイスクラス WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1187deb89c8e665b4a44e67dbb184589b5784419
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843089"
---
# <a name="using-device-interfaces"></a>デバイス インターフェイスの使用





*デバイスインターフェイス*は、アプリケーションがデバイスにアクセスするために使用できるプラグアンドプレイ (PnP) デバイスへのシンボリックリンクです。 ユーザーモードアプリケーションは、インターフェイスのシンボリックリンク名を API 要素 (Microsoft Win32 **CreateFile**関数など) に渡すことができます。 デバイスインターフェイスのシンボリックリンク名を取得するために、ユーザーモードアプリケーションは**Setupdi**関数を呼び出すことができます。 **Setupdi**関数の詳細については、「[デバイスインターフェイス関数の使用](https://docs.microsoft.com/windows-hardware/drivers/install/using-device-installation-functions)」を参照してください。

各デバイスインターフェイスは、*デバイスインターフェイスクラス*に属しています。 たとえば、CD-ROM デバイスのドライバースタックは、GUID\_DEVINTERFACE\_CDROM クラスに属するインターフェイスを提供する場合があります。 CD-ROM デバイスのドライバーの1つで、GUID のインスタンス\_DEVINTERFACE\_CDROM クラスが登録され、CD-ROM デバイスが使用可能であることをシステムとアプリケーションに通知します。 デバイスインターフェイスクラスの詳細については、「[デバイスインターフェイスの概要](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)」を参照してください。

### <a name="registering-a-device-interface"></a>デバイスインターフェイスの登録

デバイスインターフェイスクラスのインスタンスを登録するために、フレームワークベースのドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数内から[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出すことができます。 ドライバーがインターフェイスの複数のインスタンスをサポートしている場合は、一意の参照文字列を各インスタンスに割り当てることができます。

ドライバーがデバイスインターフェイスを登録した後、ドライバーは[**WdfDeviceRetrieveDeviceInterfaceString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedeviceinterfacestring)を呼び出して、システムがデバイスインターフェイスに割り当てたシンボリックリンク名を取得できます。

ドライバーによるデバイスインターフェイスの登録方法の詳細については、「[デバイスインターフェイスクラスの登録](https://docs.microsoft.com/windows-hardware/drivers/install/registering-a-device-interface-class)」を参照してください。

### <a name="enabling-and-disabling-a-device-interface"></a>デバイスインターフェイスを有効または無効にする

ドライバーが[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出した後、デバイスが動作状態になると、フレームワークはデバイスのすべてのインターフェイスを自動的に有効にし、デバイスが動作状態のままになったときにインターフェイスを無効にします。 ドライバーが**WdfDeviceCreateDeviceInterface**を呼び出したときに物理デバイスオブジェクト (PDO) を指定した場合、無効になっているデバイスが再度有効にされた場合、フレームワークによってデバイスのインターフェイスが再度有効になります。

ドライバーは、必要に応じて、デバイスインターフェイスを無効にしてから再度有効にすることができます。 たとえば、ドライバーがデバイスの応答を停止したと判断した場合、ドライバーは[**Wdfdevicesetdeviceinterfacestate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestate)を呼び出してデバイスのインターフェイスを無効にし、アプリケーションがインターフェイスに新しいハンドルを取得できないようにします。 (インターフェイスに対する既存のハンドルは影響を受けません)。後でデバイスが使用可能になった場合、ドライバーは**Wdfdevicesetdeviceinterfacestate**を再度呼び出して、インターフェイスを再び有効にすることができます。

### <a name="receiving-requests-to-access-a-device-interface"></a>デバイスインターフェイスへのアクセス要求を受信する

アプリケーションまたはカーネルモードのコンポーネントがドライバーのデバイスインターフェイスへのアクセスを要求すると、フレームワークはドライバーの[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) callback 関数を呼び出します。 ドライバーは、 [**Wdffileobjectgetfilename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)を呼び出して、アプリケーションまたはカーネルモードコンポーネントがアクセスしているデバイスまたはファイルの名前を取得できます。 ドライバーがデバイスインターフェイスを登録するときに参照文字列を指定した場合、オペレーティングシステムには、 **Wdffileobjectgetfilename**から返されるファイル名またはデバイス名に参照文字列が含まれます。

### <a name="accessing-another-drivers-device-interface"></a>別のドライバーのデバイスインターフェイスへのアクセス

このセクションでは、カーネルモードドライバーフレームワーク (KMDF) ドライバーまたはユーザーモードドライバーフレームワーク (UMDF) バージョン2ドライバーが、別のドライバーによって提供されるデバイスインターフェイスの到着または削除の通知を登録し、[リモート i/o ターゲットを作成する方法について説明します。](general-i-o-targets-in-umdf.md)デバイスインターフェイスによって表されるデバイスと通信する。

UMDF バージョン1のドライバーでこれを行う方法については、「 [Umdf ドライバーでのデバイスインターフェイスの使用](using-device-interfaces-in-umdf-drivers.md#accessing-another-drivers-device-interface)」を参照してください。

デバイスインターフェイスイベントの通知を登録するために、KMDF ドライバーは[**IoRegisterPlugPlayNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)を呼び出しますが、UMDF 2 ドライバーは\_CM を呼び出して[ **\_通知を登録**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)します。 どちらの場合も、ドライバーは[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数から適切なルーチンを呼び出します。

次のコード例は、ローカルの UMDF 2 ドライバーが通知を登録してから、リモート i/o ターゲットを開く方法を示しています。

1.  リモートドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)から[**WdfDeviceCreateDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)を呼び出すことによって、デバイスインターフェイスを登録します。
    ```cpp
        UNICODE_STRING ref;
        RtlInitUnicodeString(&ref, MY_HID_FILTER_REFERENCE_STRING);
        status = WdfDeviceCreateDeviceInterface(
                     hDevice,
                     (LPGUID) &GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER,
                     &ref // ReferenceString
                 );

        if (!NT_SUCCESS (status)) {
            MyKdPrint( ("WdfDeviceCreateDeviceInterface failed 0x%x\n", status));
            return status;
        }

    ```

2.  ローカルドライバーは CM を呼び出して、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)からの[ **\_通知を登録**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)して、デバイスインターフェイスが使用可能な場合に通知を受け取るように\_します。 デバイスインターフェイスが使用可能な場合にフレームワークが呼び出す通知コールバックルーチンへのポインターを提供します。
    ```cpp
    DWORD cmRet;
        CM_NOTIFY_FILTER cmFilter;

        ZeroMemory(&cmFilter, sizeof(cmFilter));
        cmFilter.cbSize = sizeof(cmFilter);
        cmFilter.FilterType = CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE;
        cmFilter.u.DeviceInterface.ClassGuid = GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER;

        cmRet = CM_Register_Notification(
                    &cmFilter,                     // PCM_NOTIFY_FILTER pFilter,
                    (PVOID) hDevice,               // PVOID pContext,
                    MyCmInterfaceNotification,    // PCM_NOTIFY_CALLBACK pCallback,
                    &fdoData->CmNotificationHandle // PHCMNOTIFICATION pNotifyContext
                    );
        if (cmRet != CR_SUCCESS) {
            MyKdPrint( ("CM_Register_Notification failed, error %d\n", cmRet));
            status = STATUS_UNSUCCESSFUL;
            return status;
        }   
    ```

3.  システムは、指定されたデバイスインターフェイスが到着するか削除されるたびに、ローカルドライバーの通知コールバックルーチンを呼び出します。 コールバックルーチンは、 *EventData*パラメーターを調べて、どのデバイスインターフェイスに到達したかを判断できます。 その後、作業項目をキューに置いて、デバイスインターフェイスを開くことができます。
    ```cpp
    DWORD 
    MyCmInterfaceNotification(
        _In_ HCMNOTIFICATION       hNotify,
        _In_opt_ PVOID             Context,
        _In_ CM_NOTIFY_ACTION      Action,
        _In_reads_bytes_(EventDataSize) PCM_NOTIFY_EVENT_DATA EventData,
        _In_ DWORD                 EventDataSize
        )
    {
        PFDO_DATA fdoData;
        UNICODE_STRING name;
        WDFDEVICE device;
        NTSTATUS status;
        WDFWORKITEM workitem;

        UNREFERENCED_PARAMETER(hNotify);
        UNREFERENCED_PARAMETER(EventDataSize);

        device = (WDFDEVICE) Context;
        fdoData = ToasterFdoGetData(device);

        switch(Action) {
        case CM_NOTIFY_ACTION_DEVICEINTERFACEARRIVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: Arrival of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));

            //
            // Enqueue a work item to open target
            //

            break;
        case CM_NOTIFY_ACTION_DEVICEINTERFACEREMOVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: removal of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));
            break;
        default:
            MyKdPrint( ("MyCmInterfaceNotification: Arrival unknown action\n"));
            break;
        }

        return 0;
    }
    ```


4.  ローカルドライバーは、作業項目のコールバック関数から、 [**Wdfiotargetcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate)を呼び出してリモートターゲットを作成し、 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出してリモート i/o ターゲットを開きます。

    [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)を呼び出す場合、ドライバーは必要に応じて、削除通知を受け取るために[*Evtiotargetqueryremove*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove)コールバック関数を登録し、削除を拒否する機会を提供します。 ドライバーで*Evtiotargetqueryremove*が提供されていない場合、デバイスが削除されると、フレームワークは i/o ターゲットを閉じます。

    まれに、UMDF 2 ドライバーが CM を呼び出して、デバイスの削除通知を登録するために2回目の[ **\_通知を\_登録**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)できる場合があります。 たとえば、ドライバーが[**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出してデバイスインターフェイスへのハンドルを取得する場合、デバイスの削除の通知に登録して、クエリの削除試行に適切に応答できるようにする必要があります。 ほとんどの場合、UMDF 2 ドライバーは CM を呼び出し **\_\_通知**を1回だけ登録し、デバイスの削除に WDF サポートを利用します。

    ```cpp
    VOID 
    EvtWorkItem(
        _In_ WDFWORKITEM WorkItem
    )
    {
        // 
        // create and open remote target
        //

        return;
    }
    ```

## <a name="related-topics"></a>関連トピック

[デバイス インターフェイスの到着とデバイスの削除の通知の登録](https://docs.microsoft.com/windows-hardware/drivers/install/registering-for-notification-of-device-interface-arrival-and-device-removal)
