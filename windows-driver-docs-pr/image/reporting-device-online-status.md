---
title: デバイスのオンライン状態のレポート
description: デバイスのオンライン状態のレポート
ms.assetid: 59ce747a-bb5e-4e8c-ab4a-d3f4432f17e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 377bb769a4a036f36c5b92bc7d93d3ece8b9835b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840754"
---
# <a name="reporting-device-online-status"></a>デバイスのオンライン状態のレポート





WIA サービスは、 [**Istiusd:: GetStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)メソッドを呼び出すことによって、wia デバイスのオンライン状態をチェックします。 WIA ミニドライバーは、ハードウェアの現在のオンライン状態を確認し、結果を報告する必要があります。

次の2つの主要な操作については、WIA サービスは**ib usd:: GetStatus**メソッドを呼び出します。

-   デバイスのオンライン状態を確認しています。

-   プッシュボタンイベントなどのデバイスイベントのポーリング。

操作要求を決定するには、 [**STI\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status)構造体の**statusmask**メンバーをチェックします。 **Statusmask**メンバーは、次の要求のいずれかになります。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態  
デバイスがオンラインであるかどうかを確認します。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態  
デバイスイベントを確認します。

### <a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態

この操作要求を実行するには、STI\_デバイス\_状態構造体の**dwOnlineState**メンバーを設定します。

### <a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態

この操作要求を実行するには、STI\_デバイス\_状態構造体の**dwEventHandlingState**メンバーを設定します。 使用する値は、EVENTHANDLING\_PENDING\_の STI です。 (デバイスには保留中のイベントがあり、WIA サービスへのレポートを待機しています)。

STI\_EVENTHANDLING\_PENDING が設定されている場合、wia サービスは、WIA ドライバーでイベントが発生したことを通知します。 WIA サービスは、 [**ib usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)メソッドを呼び出して、イベントに関する詳細情報を取得します。

**I、usd:: GetNotificationData**メソッドは、ポーリングイベントと割り込みイベントに対して呼び出されます。 この方法では、適切なイベント情報を入力して、WIA サービスに返す必要があります。

**注**   デバイスイベントが発生したときに適切に設定されるように、 **dwEventHandlingState**メンバーの [STI\_EVENTHANDLING\_PENDING] フラグを常にオフにします。

 

次の例は、 **IGetStatus**メソッドの実装を示しています。

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
  // If we are asked, verify the device is online.
  //

  if (pDevStatus->StatusMask & STI_DEVSTATUS_ONLINE_STATE) {

    //
    // assume the device is OFF-LINE before continuing. This will
    // validate that the online check was successful.
    //

    pDevStatus->dwOnlineState = STI_ONLINESTATE_OFFLINE;

    if(MyDeviceIsOnlineStatus()) {
 
      //
      // device is ON-LINE and operational
      //

      pDevStatus->dwOnlineState |= STI_ONLINESTATE_OPERATIONAL;
    } else {

      //
      // device is OFF-LINE and NOT operational
      //

 }
  }
  return S_OK;
}
```

 

 




