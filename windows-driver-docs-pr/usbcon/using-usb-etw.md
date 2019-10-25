---
Description: このトピックでは、アクティビティ ID Guid に関する情報を提供し、これらの Guid をイベントトレースプロバイダーに追加する方法、およびそれらを Netmon で表示する方法について説明します。
title: USB ETW トレースでのアクティビティ ID Guid の使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2ea499f338b893c1ccb8ca2057663dd874c8ade
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838776"
---
# <a name="using-activity-id-guids-in-usb-etw-traces"></a>USB ETW トレースでのアクティビティ ID Guid の使用


このトピックでは、アクティビティ ID Guid に関する情報を提供し、これらの Guid をイベントトレースプロバイダーに追加する方法、およびそれらを Netmon で表示する方法について説明します。

[USB ドライバースタック](usb-3-0-driver-stack-architecture.md)内のドライバー (2.0 と3.0 の両方) は、ETW イベントトレースプロバイダーです。 Windows 7 では、USB ドライバースタックからイベントトレースをキャプチャするときに、他のドライバーやアプリケーションなどの他のプロバイダーからトレースをキャプチャできます。 その後、結合されたログを読み取ることができます (プロバイダーのイベントトレース用の Netmon パーサーを作成済みであることを前提としています)。

Windows 8 以降では、*アクティビティ ID guid*を使用して、プロバイダー間で (アプリケーション、クライアントドライバー、および USB ドライバースタックから) イベントを関連付けることができます。 複数のプロバイダーからのイベントは、イベントが同じアクティビティ ID GUID を持つ場合に、Netmon に関連付けることができます。 これらの Guid に基づいて、Netmon は、上位層でインストルメント化されたアクティビティによって発生した一連の USB イベントを表示できます。

Netmon の他のプロバイダーからのイベントトレースを結合して表示しながら、アプリケーションからイベントを右クリックし、[メッセージ**交換の検索-&gt; NetEvent** ] を選択して、関連付けられているドライバーイベントを確認します。

このイメージは、アプリケーション、UMDF ドライバー、および Ucx01000 (USB ドライバースタック内のドライバーの1つ) からの関連イベントを示しています。これらのイベントのアクティビティ ID GUID は同じです。

![microsoft ネットワークモニター](images/netmon-activity.png)

-   [アプリケーションにアクティビティ ID GUID を追加する方法](#how-to-add-an-activity-id-guid-in-an-application)
-   [UMDF ドライバーでアクティビティ ID GUID を設定する方法](#how-to-set-the-activity-id-guid-in-a-umdf-driver)
-   [カーネルモードドライバーにアクティビティ ID GUID を追加する方法](#how-to-add-activity-id-guid-in-a-kernel-mode-driver)

## <a name="how-to-add-an-activity-id-guid-in-an-application"></a>アプリケーションにアクティビティ ID GUID を追加する方法


アプリケーションでは、 [**Eventactivityidcontrol**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)を呼び出すことによってアクティビティ ID guid を含めることができます。 詳細については、「[イベントトレース関数](https://docs.microsoft.com/windows/desktop/ETW/event-tracing-functions)」を参照してください。

このコード例は、アプリケーションでアクティビティ ID GUID を設定し、ETW プロバイダー (UMDF ドライバー) に送信する方法を示しています。

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

前の例では、アプリケーションは[**Eventactivityidcontrol**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)を呼び出して、アクティビティ ID (イベント\_アクティビティ\_CTRL\_作成\_ID) を作成し、設定します (イベント\_アクティビティ\_CTRL\_set\_現在のスレッドの ID)。 アプリケーションでは、ドライバーによって定義された IOCTL (次のセクションで説明します) を送信することによって、ユーザーモードドライバーなどの ETW イベントプロバイダーにアクティビティ GUID を指定します。

イベントプロバイダーは、インストルメンテーションマニフェストファイル () を発行する必要があります。MAN ファイル)。 [**メッセージコンパイラ (Mc)** ](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)を実行すると、イベントプロバイダー、イベント属性、チャネル、およびイベントの定義を含むヘッダーファイルが生成されます。 この例では、アプリケーションは、生成されたヘッダーファイルで定義されている EventWriteReadFail を呼び出して、エラーが発生した場合にトレースイベントメッセージを書き込みます。

## <a name="how-to-set-the-activity-id-guid-in-a-umdf-driver"></a>UMDF ドライバーでアクティビティ ID GUID を設定する方法


ユーザーモードドライバーは、 [**Eventactivityidcontrol**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)を呼び出すことによってアクティビティ ID guid を作成および設定します。呼び出しは、前のセクションで説明したように、アプリケーションが呼び出す方法に似ています。 これらの呼び出しは、アクティビティ ID GUID を現在のスレッドに追加します。このアクティビティ ID GUID は、スレッドがイベントをログに記録するたびに使用されます。 詳細については、「[アクティビティ識別子の使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-activity-identifiers)」を参照してください。

このコード例は、アプリケーションによって作成され、IOCTL によって指定されたアクティビティ ID GUID を、UMDF ドライバーがどのように設定するかを示しています。

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

アプリケーションによって作成されたアクティビティ ID GUID が[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/debugger/user-mode-driver-framework-debugging)(UMDF) クライアントドライバーに関連付けられていることを確認してみましょう。 ドライバーは、アプリケーションから IOCTL 要求を受信すると、プライベートメンバーに GUID をコピーします。 ある時点で、アプリケーションは、 [**ReadFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)を呼び出して読み取り操作を実行します。 フレームワークは、要求を作成し、ドライバーのハンドラー ForwardFormattedRequest を呼び出します。 ハンドラーでは、イベントメッセージをトレースするために[**Eventactivityidcontrol**](https://docs.microsoft.com/windows/desktop/api/evntprov/nf-evntprov-eventactivityidcontrol)と EventWriteReadFail を呼び出して、以前に格納されていたアクティビティ ID GUID をスレッドに設定します。

**メモ** また、UMDF ドライバーには、インストルメンテーションマニフェストファイルによって生成されるヘッダーファイルも含まれている必要があります。 ヘッダーファイルは、トレースメッセージを書き込む EventWriteReadFail などのマクロを定義します。



## <a name="how-to-add-activity-id-guid-in-a-kernel-mode-driver"></a>カーネルモードドライバーにアクティビティ ID GUID を追加する方法


カーネルモードでは、ドライバーは、ユーザーモードまたはドライバーによって作成されたスレッドで発生したスレッドのメッセージをトレースできます。 どちらの場合も、ドライバーはスレッドのアクティビティ ID GUID を必要とします。

メッセージをトレースするには、ドライバーが登録ハンドルをイベントプロバイダーとして取得する必要があります (「 [**Etwregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwregister)」を参照)。次に、GUID とイベントメッセージを指定して[**etwregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite)を呼び出します。 詳細については、「[カーネルモードドライバーへのイベントトレースの追加](https://docs.microsoft.com/windows-hardware/drivers/devtest/adding-event-tracing-to-kernel-mode-drivers)」を参照してください。

カーネルモードドライバーが、アプリケーションまたはユーザーモードドライバーによって作成された要求を処理する場合、カーネルモードドライバーはアクティビティ ID GUID を作成して設定しません。 代わりに、i/o マネージャーがアクティビティ ID の伝達のほとんどを処理します。 ユーザーモードスレッドによって要求が開始されると、i/o マネージャーは要求に対して IRP を作成し、現在のスレッドのアクティビティ ID GUID を新しい IRP に自動的にコピーします。 カーネルモードドライバーがそのスレッドでイベントをトレースする場合は、 [**IoGetActivityIdIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iogetactivityidirp)を呼び出して GUID を取得し、 [**etwwrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite)を呼び出す必要があります。

カーネルモードドライバーがアクティビティ ID GUID を持つ IRP を作成した場合、ドライバーは EVENT\_アクティビティを使用して[**Etwactivityidcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwactivityidcontrol)を呼び出し、CTRL\_\_を作成し、新しい GUID を生成するために\_ID を設定\_ます。 ドライバーは、 [**Iosetactivityidirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetactivityidirp)を呼び出して新しい GUID を IRP に関連付けてから、 [**etwwrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-etwwrite)を呼び出すことができます。

アクティビティ ID GUID は、IRP と共に次の下位のドライバーに渡されます。 下位のドライバーは、トレースメッセージをスレッドに追加できます。

## <a name="related-topics"></a>関連トピック
[USB Windows イベントトレーシング](usb-event-tracing-for-windows.md)  



