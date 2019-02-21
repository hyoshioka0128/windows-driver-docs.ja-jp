---
title: ポーリングのイベントのサポートを追加します。
description: ポーリングのイベントのサポートを追加します。
ms.assetid: 7c7617d4-22d6-48a8-b69c-dd0347f078dd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d8b29e300f68146ad7daee89cff4eeb37094915
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550271"
---
# <a name="adding-polling-event-support"></a>ポーリングのイベントのサポートを追加します。





レポートのイベントのポーリングはを WIA ドライバーを正しく設定するには、次の操作を行います。

1.  設定**機能 = 0x33**デバイスの INF ファイルにします。 (を参照してください[WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)詳細についてはします)。

2.  レポート STI\_GENCAP\_通知と STI\_USD\_GENCAP\_ネイティブ\_で PUSHSUPPORT、 [ **IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)メソッド。

3.  サポートされているレポートのすべてのイベント、 [ **IWiaMiniDrv::drvGetCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff543977)メソッド。

4.  呼び出しに応答、 [ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)メソッド。 WIA サービスは、INF ファイルで構成可能な事前設定された間隔で、このメソッドを呼び出します。 既定の設定は、1 秒間隔です。

5.  適切なイベント情報の対応を報告、 [ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)メソッド。

WIA サービスの呼び出し、 **IStiUSD::GetStatus**メソッドの 2 つの主要な操作。

1.  デバイスのオンライン状態を確認しています。

2.  プッシュ ボタンのイベントなどのデバイス イベントのポーリングを行います。

操作要求を決定することができるようチェック、 **StatusMask**のメンバー、 [ **STI\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff548369)構造体。 **StatusMask**メンバーには、次の要求のいずれかを指定できます。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態  
この操作の要求は、デバイスがオンラインであり、設定を入力する必要があるかどうかを確認します。、 **dwOnlinesState** 、STI のメンバー\_デバイス\_ステータス構造体。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態  
この操作の要求は、デバイスのイベントを確認します。 設定して指定する必要があります、 **dwEventHandlingState** 、STI のメンバー\_デバイス\_ステータス構造体。 使用する必要がある値は STI\_様々\_保留します。 (デバイスが保留中のイベントを待機している、WIA サービスに報告します。)

STI\_様々\_PENDING に設定されている、WIA サービスが WIA ドライバーでイベントが発生したことを通知します。 WIA サービスの呼び出し、 **IStiUSD::GetNotificationData**イベントに関する詳細を取得します。

**IStiUSD::GetNotificationData**ポーリングされたイベントと割り込みイベント メソッドが呼び出されます。 WIA サービスに戻るに適切なイベント情報を入力する必要がありますが、このメソッドになります。

**注**  * * *、STI を常にオフ\_様々\_保留中のフラグ、 **dwEventHandlingState**デバイス イベントの発生時に正しく設定されていることを確認するにはメンバー。
この WIA ドライバーを設定する必要があります、 *m\_guidLastEvent*クラス メンバー変数を適切なイベントのイベントが検出されたときに GUID をします。 *M\_guidLastEvent* WIA サービスを呼び出すと、後でオンになって、 **IStiUSD::GetNotificationData**メソッド。 *M\_guidLastEvent*でメンバー変数が定義されている、 **CWIADevice**シグナル状態に (次のコード スニペット)、クラスが、最後のイベントをキャッシュするために使用します。 GUID に常に設定されている、WIA サービスでこのメンバー変数を要求すると、\_NULL。

 

次の例の実装を示しています、 [ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)メソッド。

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

 

 




