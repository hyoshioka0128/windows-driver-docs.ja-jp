---
title: 中断イベントのサポートを追加します。
description: 中断イベントのサポートを追加します。
ms.assetid: 74fbaa7c-f058-4b17-b278-3dea0faf4431
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10ab2b05085bac6de7c2f17190bbc46cb1de072e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531793"
---
# <a name="adding-interrupt-event-support"></a>中断イベントのサポートを追加します。





中断イベントを報告するには、WIA ドライバーを正しく設定で、次の手順を実行します。

1.  設定**機能 = 0x31**デバイスの INF ファイルにします。 (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細についてはします)。

2.  レポート STI\_GENCAP\_通知と STI\_USD\_GENCAP\_ネイティブ\_で PUSHSUPPORT、 [ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)メソッド。

3.  サポートされているレポートのすべてのイベント、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

4.  キャッシュと渡されたイベント ハンドルを使用して、 [ **IStiUSD::SetNotificationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff543840)メソッド。 これは、デバイスが通知されるイベント ハンドルまたは WIA ミニドライバーに通知を使用して直接**SetEvent** (Microsoft Windows SDK のドキュメントで説明)。 このメソッドでは、WIA デバイスの待機状態を開始します。

5.  適切なイベント情報の対応を報告、 [ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)メソッド。

次の 2 つの例の実装と割り込みには、デバイスの構成を表示する、 **IWiaMiniDrv::drvGetCapabilities**と**IStiUSD::SetNotificationHandle**メソッド。

**注**  オーバー ラップ I/O 呼び出しを使用して、カーネル モード ドライバーに関連するすべてのアクティビティを使用することが重要です。 これは、ため、適切なタイムアウトおよびデバイスの要求のキャンセルできます。

 

### <a href="" id="explanation-of-the-iwiaminidrv-drvgetcapabilities-implementation"></a>IWiaMiniDrv::drvGetCapabilities 実装の説明

WIA サービスの呼び出し、 **IWiaMiniDrv::drvGetCapabilities** WIA デバイスでサポートされているイベントとコマンドを取得します。 WIA ドライバーは、受信でのはじめ*lFlags*がどの要求を決定するパラメーターが回答する必要があります。

WIA ドライバー (これによって解放および WIA ドライバーによって使用される) にメモリを割り当てる必要がありますの配列を含める[ **WIA\_DEV\_CAP\_DRV** ](https://msdn.microsoft.com/library/windows/hardware/ff550233)構造体。 呼び出しで、 **IWiaMiniDrv::drvGetCapabilities**で、WIA ドライバーに割り当てられたメモリのアドレスを保持するメモリ位置へのポインターを渡す、 *ppCapabilities*パラメーター。

**注**   WIA サービスでは、このメモリは解放されます。 WIA ドライバーが割り当てられたメモリを管理する必要があります。

 

次の例の実装を示しています、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

```cpp
HRESULT _stdcall CWIADevice::drvGetCapabilities(
  BYTE            *pWiasContext,
  LONG            lFlags,
  LONG            *pcelt,
  WIA_DEV_CAP_DRV **ppCapabilities,
  LONG            *plDevErrVal)
{
  //
  // If the caller did not pass in the correct parameters,
  //  then fail the call and return E_INVALIDARG.
  //

  if (!pWiasContext) {

    //
    // The WIA service may pass in a NULL for the pWiasContext. 
    // This is expected because there is a case where no item 
    // was created at the time the event was fired.
    //
  }

  if (!plDevErrVal) {
      return E_INVALIDARG;
  }

  if (!pcelt) {
      return E_INVALIDARG;
  }

  if (!ppCapabilities) {
      return E_INVALIDARG;
  }

  *plDevErrVal = 0;

  HRESULT hr = S_OK;

  LONG lNumberOfCommands = 1;
  LONG lNumberOfEvents   = 2;

  //
  // initialize WIA driver capabilities ARRAY
  // a member WIA_DEV_CAP_DRV m_Capabilities[3] variable
  // This memory should live with the WIA minidriver.
  // A pointer to this structure is given to the WIA service using
  // ppCapabilities.  Do not delete this memory until
  // the WIA minidriver has been unloaded.
  //

  // This ARRAY should only be initialized once.
  // The Descriptions and Names should be read from the proper
  // string resource.  These string values should be localized in
  // multiple languages because an application will be use them to
  // be displayed to the user.
  //

  // Command #1
  m_Capabilities[0].wszDescription =   L"Synchronize Command";
  m_Capabilities[0].wszName = L"Synchronize";
  m_Capabilities[0].guid    = (GUID*)&WIA_CMD_SYNCHRONIZE;
  m_Capabilities[0].lFlags = 0;
  m_Capabilities[0].wszIcon = WIA_ICON_SYNCHRONIZE;

  // Event #1
  m_Capabilities[1].wszDescription = L"Scan Button";
  m_Capabilities[1].wszName = L"Scan";
  m_Capabilities[1].guid    = (GUID*)&WIA_EVENT_SCAN_IMAGE;
  m_Capabilities[1].lFlags = WIA_NOTIFICATION_EVENT | WIA_ACTION_EVENT;
  m_Capabilities[1].wszIcon = WIA_ICON_SCAN_BUTTON_PRESS;

  // Event #2
  m_Capabilities[2].wszDescription = L"Copy Button";
  m_Capabilities[2].wszName = L"Copy";
  m_Capabilities[2].guid    = (GUID*)&WIA_EVENT_SCAN_PRINT_IMAGE;
  m_Capabilities[2].lFlags = WIA_NOTIFICATION_EVENT | WIA_ACTION_EVENT;
  m_Capabilities[2].wszIcon = WIA_ICON_SCAN_BUTTON_PRESS;


  //
  //  Return depends on flags.  Flags specify whether we should return
  //  commands, events, or both.
  //
  //

  switch (lFlags) {
  case WIA_DEVICE_COMMANDS:

    //
    //  report commands only
    //

    *pcelt          = lNumberOfCommands;
    *ppCapabilities = &m_Capabilities[0];
    break;
  case WIA_DEVICE_EVENTS:

    //
    //  report events only
    //

    *pcelt          = lNumberOfEvents;
    *ppCapabilities = &m_Capabilities[1]; // start at the first event in the ARRAY
    break;
  case (WIA_DEVICE_COMMANDS | WIA_DEVICE_EVENTS):

    //
    //  report both events and commands
    //

     *pcelt          = (lNumberOfCommands + lNumberOfEvents);
     *ppCapabilities = &m_Capabilities[0];
     break;
  default:

    //
    //  invalid request
    //
    hr = E_INVALIDARG;
    break;
  }

  return hr;
}
```

[ **IStiUSD::SetNotificationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff543840) WIA サービスによって、またはこのドライバーを開始または停止イベント通知で内部的には、メソッドが呼び出されます。 使用して作成、有効なハンドルが渡される、WIA サービス**CreateEvent** (Microsoft Windows SDK のドキュメントで説明)、WIA ドライバーは、ハードウェアのイベントが発生したときに、このハンドルを通知することを示します。

**NULL**に渡すことができます、 **IStiUSD::SetNotificationHandle**メソッド。 **NULL** WIA ミニドライバーがデバイスのすべてのアクティビティを停止し、そのイベントの待機操作を終了することを示します。

次の例の実装を示しています、 **IStiUSD::SetNotificationHandle**メソッド。

```cpp
STDMETHODIMP CWIADevice::SetNotificationHandle(HANDLE hEvent)
{
  HRESULT hr = S_OK;

  if (hEvent && (hEvent != INVALID_HANDLE_VALUE)) {

    //
    // A valid handle indicates that we are asked to start our "wait"
    // for device interrupt events
    //

    //
    // reset last event GUID to GUID_NULL
    //

    m_guidLastEvent = GUID_NULL;

    //
    // clear EventOverlapped structure
    //

    memset(&m_EventOverlapped,0,sizeof(m_EventOverlapped));

    //
    // fill overlapped hEvent member with the event passed in by 
    // the WIA service. This handle will be automatically signaled
    //  when an event is triggered at the hardware level.
    //

    m_EventOverlapped.hEvent = hEvent;

    //
    // clear event data buffer.  This is the buffer that will be used
    //  to determine what event was signaled from the device.
    //

    memset(m_EventData,0,sizeof(m_EventData));

    //
    // use the following call for interrupt events on your device
    //

    DWORD dwError = 0;
    BOOL bResult = DeviceIoControl( m_hDeviceDataHandle,
                                    IOCTL_WAIT_ON_DEVICE_EVENT,
                                    NULL,
                                    0,
                                    &m_EventData,
                                    sizeof(m_EventData),
                                    &dwError,
                                    &m_EventOverlapped );

    if (bResult) {
        hr = S_OK;
    } else {
        hr = HRESULT_FROM_WIN32(::GetLastError());
    }

  } else {

    //
    // stop any hardware waiting events here, the WIA service has
    // notified us to stop all hardware event waiting
    //

    //
    // Stop hardware interrupt events. This will stop all activity on
    // the device. Since DeviceIOControl was used with OVERLAPPED i/o 
    // functionality the CancelIo() can be used to stop all kernel
    // mode activity.
    //


    if(m_hDeviceDataHandle){
        if(!CancelIo(m_hDeviceDataHandle)){

            //
            // canceling of the IO failed, call GetLastError() here to determine the cause.
            //

            LONG lError = ::GetLastError();

        }
    }
  }
  return hr;
}
```

WIA ミニドライバーまたは WIA デバイスの検出し、イベントの通知が行われると、WIA サービスを呼び出す、 [ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)メソッド。 これは、この WIA ミニドライバーが発生したイベントの詳細を報告するメソッドです。

WIA サービスの呼び出し、 **IStiUSD::GetNotificationData**が通知されたイベントに関する情報を取得します。 **IStiUSD::GetNotificationData**メソッドは、2 つのイベント操作のいずれかの結果として呼び出すことができます。

1.  **IStiUSD::GetStatus** 、STI を設定して保留中のイベントがあったことを報告\_様々\_保留中のフラグ、 [ **STI\_デバイス\_の状態**](https://msdn.microsoft.com/library/windows/hardware/ff548369)構造体。

2.  *HEvent*によってハンドルが渡される**IStiUSD::SetNotificationHandle**ハードウェア、または呼び出すことによってシグナル通知された**SetEvent** (Microsoft Windows SDK で説明します。ドキュメント)。

入力するため、WIA ドライバーは、 [ **STINOTIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff548350)構造体

次の例の実装を示しています、 **IStiUSD::GetNotificationData**メソッド。

```cpp
STDMETHODIMP CWIADevice::GetNotificationData( LPSTINOTIFY pBuffer )
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pBuffer){
      return E_INVALIDARG;
  }
 
  GUID guidEvent = GUID_NULL;
  DWORD dwBytesRet = 0;
  BOOL bResult = GetOverlappedResult(m_hDeviceDataHandle, &m_EventOverlapped, &dwBytesRet, FALSE );
  if (bResult) {
    //
    // read the m_EventData buffer to determine the proper event.
    // set guidEvent to the proper event GUID
    // set guidEvent to GUID_NULL when an event has
    // not happened that you are concerned with
    //

    if(m_EventData[0] == DEVICE_SCAN_BUTTON_PRESSED) {
       guidEvent = WIA_EVENT_SCAN_IMAGE;
    } else {
       guidEvent = GUID_NULL;
    }
  }

  //
  // If the event was triggered, then fill in the STINOTIFY structure
  // with the proper event information
  //

  if (guidEvent != GUID_NULL) {
    memset(pBuffer,0,sizeof(STINOTIFY));
    pBuffer->dwSize               = sizeof(STINOTIFY);
    pBuffer->guidNotificationCode = guidEvent;        
  } else {
    return STIERR_NOEVENTS;
  }

  return S_OK;
}
```

中断イベントを渡すことによって、いつでも停止できる**NULL**イベント ハンドルとして。 ミニドライバーは、ハードウェア デバイスで、待機状態を停止するシグナルとしてこのを解釈する必要があります。

**注**   、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)メソッドは、イベントの待機状態に影響を与える電源管理イベントを受け取ることができます。

 

WIA サービスの呼び出し、 **IWiaMiniDrv::drvNotifyPnpEvent**メソッド作成して送信し、WIA\_イベント\_POWER\_中断イベント、システムがスリープ状態に配置するとします。 この呼び出しが発生した場合、デバイスが、待機状態からに既に可能性があります。 スリープ状態は、このシャット ダウン状態にシステムを許可する任意の待機状態を終了するカーネル モード ドライバーを自動的にトリガーします。 システムのスリープ状態から再開 WIA サービスが送信、WIA\_イベント\_POWER\_再開イベント。 この時点で、WIA ミニドライバーは、割り込みイベントの待機状態を再確立する必要があります。 スリープ状態の詳細については、次を参照してください。[システム電源の状態](https://msdn.microsoft.com/library/windows/hardware/ff564571)と[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)します。

WIA ミニドライバー キャッシュ イベント ハンドル最初に渡されることをお勧めしますが、 [ **IStiUSD::SetNotificationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff543840)システムをスリープ状態から再開したときにその it を再利用できるようにメソッドまたは休止状態。

WIA サービス*しない*呼び出し、 **IStiUSD::SetNotificationHandle**後に、システムが再開されました。 ミニドライバーを呼び出すことをお勧めその**IStiUSD::SetNotificationHandle**メソッド、キャッシュされたイベント ハンドルを渡します。

WIA サービスの呼び出し、 **IWiaMiniDrv::drvNotifyPnpEvent**システム イベントの発生時のメソッド。 WIA ドライバーを確認する必要があります、 *pEventGUID*のどのイベントが処理されているかを決定するパラメーター。

処理する必要があるいくつかの一般的なイベントは次のとおりです。

<a href="" id="wia-event-power-suspend"></a>WIA\_イベント\_POWER\_中断  
システムが中断/スリープ モードになります。

<a href="" id="wia-event-power-resume"></a>WIA\_イベント\_POWER\_再開  
システムは中断/スリープ モードから開始してをいます。

WIA ドライバーは、中断から返された後、イベントの割り込みの待機状態を復元する必要があります。 これにより、イベントは、システムのスリープと機能も。

次の例の実装を示しています、 [ **IWiaMiniDrv::drvNotifyPnpEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff544998)メソッド。

```cpp
HRESULT _stdcall CWIADevice::drvNotifyPnpEvent(
  const GUID *pEventGUID,
  BSTR       bstrDeviceID,
  ULONG      ulReserved)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if ((!pEventGUID)||(!bstrDeviceID)) {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;

  if(*pEventGUID == WIA_EVENT_POWER_SUSPEND) {

    //
    // disable any driver activity to make sure we properly
    // shut down (the driver is not being unloaded, just disabled)
    //

  } else if(*pEventGUID == WIA_EVENT_POWER_RESUME) {

    //
    // reestablish any event notifications to make sure we properly
    // set up any event waiting status using the WIA service supplied
    // event handle
    //

    if(m_EventOverlapped.hEvent) {

      //
      // call ourselves with the cached EVENT handle given to
      // the WIA driver by the WIA service.
      //

        SetNotificationHandle(m_EventOverlapped.hEvent);
    }
  }
  return hr;
}
```

 

 




