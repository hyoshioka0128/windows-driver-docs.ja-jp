---
Description: このトピックでは、情報を提供します。 イベントのこれらの Guid を追加する方法については、アクティビティ ID の Guid トレース プロバイダー、と Netmon で表示します。
title: USB ETW トレースでのアクティビティ ID GUID の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d784286dc1c314af739b7c7faefb535c87d8a0e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356557"
---
# <a name="using-activity-id-guids-in-usb-etw-traces"></a>USB ETW トレースでのアクティビティ ID GUID の使用


このトピックでは、情報を提供します。 イベントのこれらの Guid を追加する方法については、アクティビティ ID の Guid トレース プロバイダー、と Netmon で表示します。

内のドライバー、 [USB ドライバー スタック](usb-3-0-driver-stack-architecture.md)(2.0 と 3.0 の両方) は ETW イベント トレース プロバイダー。 USB ドライバー スタックからのイベント トレースをキャプチャ中に Windows 7 では、他のドライバーやアプリケーションなどの他のプロバイダーからのトレースをキャプチャできます。 (プロバイダーのイベント トレース Netmon パーサーを作成したと仮定)、結合されたログを確認できます。

Windows 8 以降、関連付けることができますイベント プロバイダー (アプリケーション、クライアント ドライバー、および USB ドライバー スタック) から全体を使用して*アクティビティ ID Guid*します。 イベントが同じアクティビティ ID の GUID がある場合、Netmon で複数のプロバイダーからのイベントを関連付けできます。 これらの Guid に基づき、ネットワーク モニターに表示できます上位のレイヤーでインストルメント化されたアクティビティの結果として生じた USB イベントのセット。

Netmon で他のプロバイダーから結合されたイベントのトレースを表示中に、アプリケーションからのイベントを右クリックし、**メッセージ交換の検索 -&gt; NetEvent**関連するドライバーのイベントを表示します。

このイメージは、アプリケーション、UMDF ドライバー、および Ucx01000.sys (USB ドライバー スタック内のドライバーのいずれか) から関連するイベントを示します。これらのイベントでは、同じアクティビティ ID の GUID があります。

![microsoft ネットワーク モニター](images/netmon-activity.png)

-   [アプリケーションでアクティビティ ID の GUID を追加する方法](#how-to-add-an-activity-id-guid-in-an-application)
-   [UMDF ドライバーでアクティビティ ID の GUID を設定する方法](#how-to-set-the-activity-id-guid-in-a-umdf-driver)
-   [カーネル モード ドライバーでアクティビティ ID の GUID を追加する方法](#how-to-add-activity-id-guid-in-a-kernel-mode-driver)

## <a name="how-to-add-an-activity-id-guid-in-an-application"></a>アプリケーションでアクティビティ ID の GUID を追加する方法


アプリケーションが呼び出すことによってアクティビティ ID の Guid を含めることができます[ **EventActivityIdControl**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)します。 詳細については、次を参照してください。[イベント トレース関数](https://docs.microsoft.com/windows/desktop/ETW/event-tracing-functions)します。

このコード例は、アプリケーションでアクティビティ ID の GUID を設定し、ETW プロバイダー UMDF ドライバーに送信方法を示します。

```cpp
EventActivityIdControl(EVENT_ACTIVITY_CTRL_CREATE_ID, &activityIdStruct.ActivityId); 
EventActivityIdControl(EVENT_ACTIVITY_CTRL_SET_ID,    &activityIdStruct.ActivityId); 

if (!DeviceIoControl(hRead,
                     IOCTL_OSRUSBFX2_SET_ACTIVITY_ID,
                     &activityIdStruct,         // Ptr to InBuffer
                     sizeof(activityIdStruct),  // Length of InBuffer
                     NULL,                      // Ptr to OutBuffer
                     0,                         // Length of OutBuffer
                     NULL,                      // BytesReturned
                     0))                        // Ptr to Overlapped structure
{         

          wprintf(L"Failed to set activity ID - error %d\n", GetLastError());
}

...

success = ReadFile(hRead, pinBuf, G_ReadLen, (PULONG) &nBytesRead, NULL);

if(success == 0) 
{
          wprintf(L"ReadFile failed - error %d\n", GetLastError());

          EventWriteReadFail(0, GetLastError());

          ...


}
```

アプリケーションを呼び出す前の例では、 [ **EventActivityIdControl** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)アクティビティ ID を作成する (イベント\_アクティビティ\_CTRL\_作成\_ID) に設定し、(イベント\_アクティビティ\_CTRL\_設定\_ID)、現在のスレッド。 アプリケーションでは、(次のセクションで説明) ドライバーの定義済みの IOCTL を送信することによって、ユーザー モード ドライバーなど、ETW イベント プロバイダーにそのアクティビティ GUID を指定します。

イベント プロバイダーは、インストルメンテーション マニフェスト ファイルを発行する必要があります (します。マニュアル ファイルの場合)。 実行して、 [**メッセージ コンパイラ (Mc.exe)** ](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)、イベント プロバイダー、イベント属性、チャネル、およびイベントの定義を含むヘッダー ファイルが生成されます。 この例では、アプリケーションは、メッセージを書き込むトレース イベント、エラーが発生した場合、生成されるヘッダー ファイルで定義されている EventWriteReadFail で呼び出します。

## <a name="how-to-set-the-activity-id-guid-in-a-umdf-driver"></a>UMDF ドライバーでアクティビティ ID の GUID を設定する方法


ユーザー モード ドライバーを作成し、呼び出すことによってアクティビティ ID の Guid を設定[ **EventActivityIdControl** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)呼び出しに似ていますが、アプリケーションを呼び出す方法は、前のセクションで説明されているとします。 これらの呼び出しでは、スレッド、イベント ログに記録されるたびに、現在のスレッドをそのアクティビティ ID の GUID ID の GUID が使用されるアクティビティを追加します。 詳細については、次を参照してください。[アクティビティ識別子を使用して](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-activity-identifiers)します。

このコード例では、UMDF ドライバーが、アクティビティが作成され、IOCTL 経由でアプリケーションによって指定された ID の GUID を設定する方法を示します。

```cpp
VOID
STDMETHODCALLTYPE
CMyControlQueue::OnDeviceIoControl(
    _In_ IWDFIoQueue *FxQueue,
    _In_ IWDFIoRequest *FxRequest,
    _In_ ULONG ControlCode,
    _In_ SIZE_T InputBufferSizeInBytes,
    _In_ SIZE_T OutputBufferSizeInBytes
    )
/*++

Routine Description:


    DeviceIoControl dispatch routine

Aruments:

    FxQueue - Framework Queue instance
    FxRequest - Framework Request  instance
    ControlCode - IO Control Code
    InputBufferSizeInBytes - Lenth of input buffer
    OutputBufferSizeInBytes - Lenth of output buffer

    Always succeeds DeviceIoIoctl
Return Value:

    VOID

--*/
{
    ...

    switch (ControlCode)
    {

        ....

        case IOCTL_OSRUSBFX2_SET_ACTIVITY_ID:
        {
            if (InputBufferSizeInBytes < sizeof(UMDF_ACTIVITY_ID))
            {
                hr = HRESULT_FROM_WIN32(ERROR_INSUFFICIENT_BUFFER);
            }
            else
            {
                FxRequest->GetInputMemory(&memory );
            }

            if (SUCCEEDED(hr)) 
            {
                buffer = memory->GetDataBuffer(&bigBufferCb);
                memory->Release();

                m_Device->SetActivityId(&((PUMDF_ACTIVITY_ID)buffer)->ActivityId);
                hr = S_OK;
            }

            break;
        }
    } 
}

VOID
 SetActivityId(
        LPCGUID ActivityId
        )
    {
        CopyMemory(&m_ActivityId, ActivityId, sizeof(m_ActivityId));
    }



void
CMyReadWriteQueue::ForwardFormattedRequest(
    _In_ IWDFIoRequest*                         pRequest,
    _In_ IWDFIoTarget*                          pIoTarget
    )
{
...
    pRequest->SetCompletionCallback(
        pCompletionCallback,
        NULL
        );

...
    hrSend = pRequest->Send(pIoTarget,
                            0,  //flags
                            0); //timeout

...
    if (FAILED(hrSend))
    {
        contextHr = pRequest->RetrieveContext((void**)&pRequestContext);

        if (SUCCEEDED(contextHr)) {

            EventActivityIdControl(EVENT_ACTIVITY_CTRL_SET_ID, &pRequestContext->ActivityId);

            if (pRequestContext->RequestType == RequestTypeRead)
            {
                EventWriteReadFail(m_Device, hrSend);
            }

            delete pRequestContext;
        }

        pRequest->CompleteWithInformation(hrSend, 0);
    }

    return;
}
```

アクティビティが、アプリケーションによって作成された ID の GUID を取得する方法に関連付けられたを見て、[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-debugging)(UMDF) クライアント ドライバー。 ドライバーでは、IOCTL 要求を受け取るアプリケーションから、プライベート メンバーの GUID をコピーします。 ある時点で、アプリケーションを呼び出す[ **ReadFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)読み取り操作を実行します。 フレームワークは、要求を作成し、ForwardFormattedRequest、ドライバーのハンドラーを呼び出します。 ハンドラーで、ドライバー設定、以前に保存されたアクティビティ ID の GUID、スレッドで呼び出すことによって[ **EventActivityIdControl** ](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)と EventWriteReadFail トレース イベント メッセージにします。

**注**The UMDF ドライバーがインストルメンテーション マニフェスト ファイルによって生成されるヘッダー ファイルを含める必要がありますもします。 ヘッダー ファイルでは、トレース メッセージを書き込む EventWriteReadFail などのマクロを定義します。



## <a name="how-to-add-activity-id-guid-in-a-kernel-mode-driver"></a>カーネル モード ドライバーでアクティビティ ID の GUID を追加する方法


カーネル モード ドライバーはユーザー モードで生成されたスレッドまたはドライバーを作成したスレッドでメッセージをトレースできます。 これら両方の場合は、ドライバーには、アクティビティのスレッドの ID の GUID が必要です。

トレースのメッセージに、ドライバーは、イベント プロバイダーとして登録ハンドルを取得する必要があります (を参照してください[ **EtwRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwregister)) を呼び出して[ **EtwWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwwrite)GUID と、イベント メッセージを指定しています。 詳細については、次を参照してください。[カーネル モード ドライバーへのイベント トレースの追加](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-event-tracing-to-kernel-mode-drivers)します。

カーネル モード ドライバーでは、アプリケーションまたはユーザー モード ドライバーによって作成された要求を処理する場合、カーネル モード ドライバーはいないを作成し、アクティビティ ID の GUID を設定します。 代わりに、I/O マネージャーは、アクティビティ ID の伝達のほとんどを処理します。 ユーザー モード スレッドを開始すると、要求を I/O マネージャーは要求の IRP を作成し、自動的に新しい IRP に現在のスレッドのアクティビティ ID の GUID をコピーします。 呼び出すことで、GUID を取得する必要があります、カーネル モード ドライバーは、そのスレッドでイベントをトレースする場合、 [ **IoGetActivityIdIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iogetactivityidirp)を呼び出して[ **EtwWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwwrite).

アクティビティ ID の GUID を使用して、カーネル モード ドライバーが IRP を作成する場合、ドライバーを呼び出すことができます[ **EtwActivityIdControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwactivityidcontrol)イベント\_アクティビティ\_CTRL\_を作成します。\_設定\_新しい GUID を生成する ID。 呼び出して IRP に新しい GUID がけたできます[ **IoSetActivityIdIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iosetactivityidirp)を呼び出して[ **EtwWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-etwwrite)します。

アクティビティ ID の GUID が、IRP と共に [次へ] の下のドライバーに渡されます。 下位のドライバーでは、スレッド、トレース メッセージを追加できます。

## <a name="related-topics"></a>関連トピック
[Windows のイベント トレースは USB](usb-event-tracing-for-windows.md)  



