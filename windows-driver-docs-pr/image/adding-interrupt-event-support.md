---
title: 割り込みイベントのサポートの追加
description: 割り込みイベントのサポートの追加
ms.assetid: 74fbaa7c-f058-4b17-b278-3dea0faf4431
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc71847b137e63962a8cc047c2e4dd6ef093d478
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840908"
---
# <a name="adding-interrupt-event-support"></a>割り込みイベントのサポートの追加





割り込みイベントを報告するように WIA ドライバーを適切に設定するには、次の手順を実行します。

1.  デバイスの INF ファイルで**機能 = 0x31**を設定します。 (詳細については、「 [WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)」を参照してください)。

2.  レポートの\_\_通知と STI\_、米国ドル\_GENCAP\_のネイティブ\_PUSHSUPPORT ( [**I、usd:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)メソッド)。

3.  [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドでサポートされているすべてのイベントを報告します。

4.  [**Ib usd:: SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)メソッドで渡されるイベントハンドルをキャッシュして使用します。 これは、デバイスが通知するイベントハンドルであるか、または WIA ミニドライバーが**SetEvent** (Microsoft Windows SDK のドキュメントで説明されている) を直接使用してシグナルを送ります。 この方法では、WIA デバイスの待機状態を開始します。

5.  [**Ib usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)メソッドで、適切なイベント情報の応答を報告します。

次の2つの例は、 **IWiaMiniDrv::D rvgetcapabilities**メソッドと**i:: setnotificationhandle**メソッドの実装を使用して、割り込み用にデバイスを構成する方法を示しています。

**注**   カーネルモードドライバーに関連するすべてのアクティビティで、重複した i/o 呼び出しを使用することが重要です。 これにより、適切なタイムアウトとデバイス要求のキャンセルが可能になります。

 

### <a href="" id="explanation-of-the-iwiaminidrv-drvgetcapabilities-implementation"></a>IWiaMiniDrv::d rvGetCapabilities の実装の説明

WIA サービスは**IWiaMiniDrv::D rvgetcapabilities**メソッドを呼び出して、wia デバイスでサポートされているイベントとコマンドを取得します。 WIA ドライバーでは、最初に受信した*Lflags*パラメーターを確認して、応答する必要がある要求を判断する必要があります。

Wia ドライバーは、wia [ **\_DEV\_CAP\_DRV**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/ns-wiamindr_lh-_wia_dev_cap_drv)構造体の配列を格納するために、(wia ドライバーによって使用され、それによって解放される) メモリを割り当てる必要があります。 **IWiaMiniDrv::D rvgetcapabilities**の呼び出しで、 *ppcapabilities*パラメーターで、WIA ドライバーで割り当てられたメモリのアドレスを保持しているメモリ位置へのポインターを渡します。

この  、WIA サービスではこのメモリを解放できない**ことに注意**してください。 WIA ドライバーでは、割り当てられたメモリを管理することが重要です。

 

[**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドの実装例を次に示します。

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

[**I、usd:: SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)メソッドは、イベント通知を開始または停止するために、WIA サービスまたはこのドライバーによって内部的に呼び出されます。 WIA サービスは、 **CreateEvent** (Microsoft Windows SDK のドキュメントで説明) を使用して作成された有効なハンドルを渡します。これは、ハードウェアでイベントが発生したときに、wia ドライバーがこのハンドルに信号を送信することを示します。

**Ib usd:: SetNotificationHandle**メソッドに**NULL**を渡すことができます。 **NULL**は、WIA ミニドライバーがすべてのデバイスアクティビティを停止し、イベント待機操作を終了することを示します。

次の例は、 **Istiusd:: SetNotificationHandle**メソッドの実装を示しています。

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

WIA ミニドライバーまたは WIA デバイスが検出され、イベントが通知されると、WIA サービスは[**ib usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)メソッドを呼び出します。 この方法では、WIA ミニドライバーが発生したイベントの詳細を報告する必要があります。

WIA サービスは、 **ib usd:: GetNotificationData**メソッドを呼び出して、通知されたばかりのイベントに関する情報を取得します。 2つのイベント操作のいずれかの結果として、 **Iの usd:: GetNotificationData**メソッドを呼び出すことができます。

1.  **IEVENTHANDLING:: GetStatus**は、STI [ **\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)構造で、STI\_\_pending フラグを設定することによって保留中のイベントがあることを報告しました。

2.  **Istiusd:: SetNotificationHandle**によって渡された*hevent*ハンドルは、ハードウェアによって通知されたか、または**SetEvent** (Microsoft Windows SDK のドキュメントで説明されています) を呼び出して発生しました。

WIA ドライバーは、 [**STINOTIFY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_stinotify)構造体の入力を行います。

次の例は、 **I、usd:: GetNotificationData**メソッドの実装を示しています。

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

割り込みイベントは、イベントハンドルとして**NULL**を渡すことによっていつでも停止できます。 ミニドライバーは、ハードウェアデバイスで待機状態を停止する信号としてこれを解釈する必要があります。

[**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドは、イベント待機状態に影響する電源管理イベントを**受け取ることが   ます**。

 

WIA サービスは**IWiaMiniDrv::D rvnotifypnpevent**メソッドを呼び出し、システムがスリープ状態になったときに、POWER\_SUSPEND イベント\_WIA\_イベントを送信します。 この呼び出しが発生した場合、デバイスは既に待機状態になっている可能性があります。 スリープ状態では、カーネルモードドライバーが自動的にトリガーされ、待機状態が終了し、システムはこの電源をオンにした状態になることがあります。 システムがスリープ状態から再開すると、WIA サービスによって、WIA\_イベント\_POWER\_RESUME イベントが送信されます。 現時点では、WIA ミニドライバーは割り込みイベントの待機状態を再確立する必要があります。 スリープ状態の詳細については、「[システムの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-states)と[デバイスの電源状態](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)」を参照してください。

WIA ミニドライバーは、システムがスリープ状態または休止状態から復帰したときに再利用できるように、最初は[**Isystem.servicemodel usd:: SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)メソッドに渡されるイベントハンドルをキャッシュすることをお勧めします。

システムが再開された後、WIA サービスは**Isystem.servicemodel usd:: SetNotificationHandle**メソッドを呼び出し*ません*。 ミニドライバーが**Ib usd:: SetNotificationHandle**メソッドを呼び出し、キャッシュされたイベントハンドルを渡すことをお勧めします。

システムイベントが発生すると、WIA サービスは**IWiaMiniDrv::D rvnotifypnpevent**メソッドを呼び出します。 WIA ドライバーは、 *Peventguid*パラメーターをチェックして、どのイベントが処理されているかを判断する必要があります。

処理する必要がある一般的なイベントは次のとおりです。

<a href="" id="wia-event-power-suspend"></a>WIA\_イベント\_電源\_中断  
システムは中断/スリープモードに移行します。

<a href="" id="wia-event-power-resume"></a>WIA\_イベント\_電源\_再開  
システムが中断/スリープモードからウェイクアップしています。

WIA ドライバーは、中断から制御が戻った後に、イベント割り込み待機状態を復元する必要があります。 これにより、システムの起動時にイベントが引き続き機能するようになります。

[**IWiaMiniDrv::D rvnotifypnpevent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvnotifypnpevent)メソッドの実装例を次に示します。

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

 

 




