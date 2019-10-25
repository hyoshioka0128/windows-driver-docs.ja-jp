---
title: ポーリング イベントのサポートの追加
description: ポーリング イベントのサポートの追加
ms.assetid: 7c7617d4-22d6-48a8-b69c-dd0347f078dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 441bc7ea44230b2b95b70f892695a88ab9a35f68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840906"
---
# <a name="adding-polling-event-support"></a>ポーリング イベントのサポートの追加





ポーリングイベントを報告するように WIA ドライバーを適切に設定するには、次の手順を実行します。

1.  デバイスの INF ファイルに  **Capabilities = 0x33**を設定します。 (詳細については、「 [WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)」を参照してください)。

2.  レポートの\_\_通知と STI\_、米国ドル\_GENCAP\_のネイティブ\_PUSHSUPPORT ( [**I、usd:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)メソッド)。

3.  [**IWiaMiniDrv::D rvgetcapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetcapabilities)メソッドでサポートされているすべてのイベントを報告します。

4.  [**Ib usd:: GetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)メソッドの呼び出しに応答します。 WIA サービスは、INF ファイルで構成できる事前設定された間隔でこのメソッドを呼び出します。 既定の設定は1秒間隔です。

5.  [**Ib usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)メソッドで、適切なイベント情報の応答を報告します。

次の2つの主要な操作については、WIA サービスは**ib usd:: GetStatus**メソッドを呼び出します。

1.  デバイスのオンライン状態を確認しています。

2.  プッシュボタンイベントなどのデバイスイベントのポーリング。

操作要求を決定するには、 [**STI\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)構造体の**statusmask**メンバーをチェックします。 **Statusmask**メンバーは、次の要求のいずれかになります。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態  
この操作要求は、デバイスがオンラインであるかどうかを確認します。また、 **dwOnlinesState**のメンバーをデバイスの\_状態構造\_に設定することによって入力する必要があります。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態  
この操作要求は、デバイスイベントを確認します。 これは、STI\_デバイス\_状態構造体の**dwEventHandlingState**メンバーを設定することによって入力する必要があります。 使用する値は、EVENTHANDLING\_PENDING\_の STI です。 (デバイスには保留中のイベントがあり、WIA サービスへのレポートを待機しています)。

STI\_EVENTHANDLING\_PENDING が設定されている場合、wia サービスは、WIA ドライバーでイベントが発生したことを通知します。 WIA サービスは、 **ib usd:: GetNotificationData**メソッドを呼び出して、イベントに関する詳細情報を取得します。

**I、usd:: GetNotificationData**メソッドは、ポーリングイベントと割り込みイベントに対して呼び出されます。 この方法では、適切なイベント情報を入力して、WIA サービスに返す必要があります。

**注**  デバイスイベントが発生したときに適切に設定されるように、 **dwEventHandlingState**メンバーの [STI\_EVENTHANDLING\_PENDING] フラグを常にオフにします。
この WIA ドライバーでは、イベントが検出されたときに、 *m\_guidLastEvent*クラスのメンバー変数を適切なイベント GUID に設定する必要があります。 後で、WIA サービスが**ib usd:: GetNotificationData**メソッドを呼び出すときに、 *m\_guidlastevent*がチェックされます。 *M\_guidLastEvent*メンバー変数は、最後にシグナル状態になったイベントをキャッシュするために使用される**Cwiadevice**クラス (次のコードスニペット) で定義されています。 このメンバー変数は、WIA サービスによって要求された後、常に GUID\_NULL に設定されます。

 

次の例は、 [**IGetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)メソッドの実装を示しています。

```cpp
STDMETHODIMP CWIADevice::GetStatus(PSTI_DEVICE_STATUS pDevStatus)
{
  //
  // If the caller did not pass in the correct parameters,
  // then fail the call with E_INVALIDARG.
  //

  if(!pDevStatus)
  {
      return E_INVALIDARG;
  }

  HRESULT hr = S_OK;

  //
  // If we are asked, verify state of an event handler 
  //(front panel buttons, user controlled attachments, etc.).
  //
  // If your device requires polling, then this is where you would
  // specify the event result.
  // However, It is not recommended to have polled events.
  // Interrupt events are better for performance, and reliability.
  // See the SetNotificationsHandle method for how to
  // implement interrupt events.
  //

  //
  // clear the dwEventHandlingState field first to make sure we are really setting
  // a pending event.
  //

  pDevStatus->dwEventHandlingState &= ~STI_EVENTHANDLING_PENDING;
  if (pDevStatus->StatusMask & STI_DEVSTATUS_EVENTS_STATE) {

    //
    // set the polled event result here, for the GetNotificationData()
    // method to read and report.
    // (m_guidLastEvent will be read in GetNotificationData)
    //

    LONG lEventResult = 0;
    PollMyDeviceForEvents(&lEventResult)

    if(lEventResult == DEVICE_SCAN_BUTTON_PRESSED) {

        //
        // polled event result was one we know about
        //

        m_guidLastEvent = WIA_EVENT_SCAN_IMAGE;
    } else {

        //
        // nothing happened, so continue
        //

        m_guidLastEvent = GUID_NULL;
    }

    if (m_guidLastEvent != GUID_NULL) {

        //
        // if the event GUID is NOT GUID_NULL, set the
        // STI_EVENTHANDLING_PENDING flag letting the WIA service
        // know that we have an event ready. This will tell the WIA
        // service to call GetNotificationData() for the event
        // specific information.
        //

        pDevStatus->dwEventHandlingState |= STI_EVENTHANDLING_PENDING;
    }
  }
  return S_OK;
}
```

 

 




