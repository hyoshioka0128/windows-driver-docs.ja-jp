---
title: デバイスのインターフェイスを使用します。
description: デバイスのインターフェイスを使用します。
ms.assetid: 98199220-947e-462e-a50c-85d81ca50108
keywords:
- デバイスは、WDK KMDF をインターフェイスします。
- WDK KMDF インターフェイスのデバイスを登録します。
- WDK KMDF を要求するデバイスのインターフェイス アクセス権を受け取る
- デバイスのインターフェイスは、WDK KMDF をクラスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ee21f36a94ac6671e5f6530377bc62c06a610bc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560411"
---
# <a name="using-device-interfaces"></a>デバイスのインターフェイスを使用します。





A*デバイス インターフェイス*プラグ アンド プレイ (PnP) へのシンボリック リンクは、デバイス、デバイスにアクセスするアプリケーションで使用できます。 ユーザー モード アプリケーションは、Microsoft Win32 などの API 要素に、インターフェイスのシンボリック リンクの名前を渡すことができます**CreateFile**関数。 ユーザー モード アプリケーションを呼び出して、デバイス インターフェイスのシンボリック リンクの名前を取得する**SetupDi**関数。 詳細については**SetupDi**関数を参照してください[デバイス インターフェイスの関数を使用して](https://msdn.microsoft.com/library/windows/hardware/ff553567)します。

各デバイスのインターフェイスが属する、*デバイス インターフェイス クラス*します。 たとえば、CD-ROM デバイスのドライバー スタックは、GUID が属しているインターフェイスを提供可能性があります\_DEVINTERFACE\_CDROM クラス。 CD-ROM デバイスのドライバーの 1 つは、GUID のインスタンスを登録\_DEVINTERFACE\_CD-ROM デバイスが使用可能なシステムおよびアプリケーションに通知する CDROM クラス。 デバイスのインターフェイス クラスの詳細については、[デバイス インターフェイスの概要](https://msdn.microsoft.com/library/windows/hardware/ff549460)を参照してください。

### <a name="registering-a-device-interface"></a>デバイスのインターフェイスを登録します。

デバイスのインターフェイス クラスのインスタンスを登録するフレームワーク ベースのドライバーを呼び出すことができます[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)内からその[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 ドライバーでは、インターフェイスの複数のインスタンスをサポートする場合は、各インスタンスに一意の参照文字列を割り当てることができます。

ドライバーを呼び出すことができます、ドライバーがデバイスのインターフェイスを登録すると、 [ **WdfDeviceRetrieveDeviceInterfaceString** ](https://msdn.microsoft.com/library/windows/hardware/ff546842)システムが、デバイス インターフェイスに割り当てられているシンボリック リンクの名前を取得するには.

ドライバーがデバイスのインターフェイスを登録できるその他の方法については、[デバイス インターフェイス クラスを登録する](https://msdn.microsoft.com/library/windows/hardware/ff549810)を参照してください。

### <a name="enabling-and-disabling-a-device-interface"></a>有効にして、デバイスのインターフェイスを無効化

ドライバーを呼び出してから[ **WdfDeviceCreateDeviceInterface**](https://msdn.microsoft.com/library/windows/hardware/ff545935)フレームワークが自動的に有効すべてのデバイスのインターフェイスと、デバイスがその稼働状態になるし、インターフェイスを無効にしますときに、。デバイスの稼働状態のままです。 呼び出されたときに、ドライバーで物理デバイス オブジェクト (PDO) が指定されてかどうか**WdfDeviceCreateDeviceInterface**、無効になっているデバイスが再度有効にする場合に、フレームワークがデバイスのインターフェイスに再度有効にします。

ドライバーでは、無効にでき、必要な場合に、デバイスのインターフェイスを再度有効にすることができます。 たとえば、ドライバーは、そのデバイスが応答を停止したことを判断した場合、ドライバー呼び出すことができます[ **WdfDeviceSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff546878)デバイスのインターフェイスを無効にしてからアプリケーションを禁止します。インターフェイスに新しいハンドルを取得します。 (既存のハンドルをインターフェイスには影響はありません)。ドライバーを呼び出すことができます、デバイスが後で使用可能なになると、 **WdfDeviceSetDeviceInterfaceState**インターフェイスを再度有効にするには、もう一度です。

### <a name="receiving-requests-to-access-a-device-interface"></a>デバイス インターフェイスへのアクセス要求の受信

ドライバーのフレームワーク、アプリケーションまたはカーネル モード コンポーネントは、ドライバーのデバイス インターフェイスへのアクセスを要求するときに[ *EvtDeviceFileCreate* ](https://msdn.microsoft.com/library/windows/hardware/ff540868)コールバック関数。 ドライバーを呼び出すことができます[ **WdfFileObjectGetFileName** ](https://msdn.microsoft.com/library/windows/hardware/ff547310)デバイスやアプリケーションとカーネル モード コンポーネントにアクセスしているファイルの名前を取得します。 オペレーティング システムにはファイルに参照文字列が含まれています、ドライバーで、デバイス インターフェイスが登録されているときに参照文字列を指定する場合、またはデバイス名を**WdfFileObjectGetFileName**を返します。

### <a name="accessing-another-drivers-device-interface"></a>別のドライバーのデバイス インターフェイスへのアクセス

ここでの追加の通知または別のドライバーによって提供されるデバイス インターフェイスの削除用のカーネル モード ドライバー フレームワーク (KMDF) ドライバーまたはユーザー モード ドライバー フレームワーク (UMDF) バージョン 2 のドライバーを登録する方法を示していて、作成、[リモートしました/O ターゲット](general-i-o-targets-in-umdf.md)デバイス インターフェイスによって表されるデバイスと通信します。

バージョン 1 の UMDF ドライバーでこれを行う方法については、[UMDF ドライバーでデバイスのインターフェイスを使用して](using-device-interfaces-in-umdf-drivers.md#accessing-another-drivers-device-interface)を参照してください。

KMDF ドライバーを呼び出してデバイス インターフェイスのイベントの通知に登録する[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)2 の UMDF ドライバーを呼び出す、 [ **CM\_登録\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)します。 どちらの場合から適切なルーチンを呼び出すと、ドライバー、 [ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。

次のコード例では、ローカルの 2 の UMDF ドライバーが通知を登録する方法を示していて、リモートの I/O ターゲットを開きます。

1.  リモートのドライバーを呼び出すことによってデバイス インターフェイスの登録[ **WdfDeviceCreateDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff545935)から[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693).
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

2.  ローカル ドライバー呼び出し[ **CM\_登録\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)から[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)にデバイスのインターフェイスが使用可能な通知に登録します。 デバイスのインターフェイスが使用可能な場合にフレームワークから呼び出される通知コールバック ルーチンへのポインターを提供します。
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

3.  システムでは、指定したデバイスのインターフェイスが到着したかが削除されたたびに、ローカル ドライバーの通知コールバック ルーチンを呼び出します。 コールバック ルーチンを調べることができます、 *EventData*デバイス インターフェイスを決定するパラメーターのお知らせします。 デバイスのインターフェイスを開くの作業項目はキューに可能性があります。
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


4.  ローカル ドライバー作業項目のコールバック関数からを呼び出す[ **WdfIoTargetCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff548591)リモートのターゲットを作成して[ **WdfIoTargetOpen** ](https://msdn.microsoft.com/library/windows/hardware/ff548634)をリモートの I/O ターゲットを開きます。

    呼び出すときに[ **WdfIoTargetOpen**](https://msdn.microsoft.com/library/windows/hardware/ff548634)、必要に応じて、ドライバー、登録、 [ *EvtIoTargetQueryRemove* ](https://msdn.microsoft.com/library/windows/hardware/ff541793)を受信するコールバック関数削除を拒否する機会と共に削除通知します。 ドライバーが提供されていない場合*EvtIoTargetQueryRemove*フレームワークは、デバイスが削除されたときに I/O ターゲットを閉じます。

    まれに、2 の UMDF ドライバーを呼び出すことができます[ **CM\_登録\_通知**](https://msdn.microsoft.com/library/windows/hardware/hh780224)デバイスの削除の通知の登録に、2 番目の時間。 ドライバーを呼び出す場合など、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)デバイス インターフェイスへのハンドルを取得するには、その必要があります通知の登録デバイスの削除の削除の試行をクエリに適切に応答できるようにします。 ほとんどの場合、2 の UMDF ドライバー呼び出し**CM\_登録\_通知**1 回だけ WDF デバイスの削除のサポートに依存しています。

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

[デバイス インターフェイスの到着とデバイスの削除の通知を登録します。](https://msdn.microsoft.com/library/windows/hardware/dn858592)
