---
title: デバイスのオンライン状態のレポート
description: デバイスのオンライン状態のレポート
ms.assetid: 59ce747a-bb5e-4e8c-ab4a-d3f4432f17e6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 214f4fc6fdf73cb1eddb8c9fda3c6c3c1b217c5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577807"
---
# <a name="reporting-device-online-status"></a>デバイスのオンライン状態のレポート





WIA サービスが呼び出すことによって、WIA デバイスのオンライン状態を確認、 [ **IStiUSD::GetStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543823)メソッド。 WIA ミニドライバーは、ハードウェアの現在オンライン状態を確認し、結果を報告する必要があります。

WIA サービスの呼び出し、 **IStiUSD::GetStatus**メソッドの 2 つの主要な操作。

-   デバイスのオンライン状態を確認しています。

-   プッシュ ボタンのイベントなどのデバイス イベントのポーリングを行います。

操作要求を決定することができるようチェック、 **StatusMask**のメンバー、 [ **STI\_デバイス\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff548369)構造体。 **StatusMask**メンバーには、次の要求のいずれかを指定できます。

<a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態  
デバイスがオンラインかどうかを確認します。

<a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態  
デバイスのイベントを確認します。

### <a href="" id="sti-devstatus-online-state"></a>STI\_DEVSTATUS\_オンライン\_状態

この操作の要求を設定して実行する必要があります、 **dwOnlineState** 、STI のメンバー\_デバイス\_ステータス構造体。

### <a href="" id="sti-devstatus-events-state"></a>STI\_DEVSTATUS\_イベント\_状態

この操作の要求を設定して実行する必要があります、 **dwEventHandlingState** 、STI のメンバー\_デバイス\_ステータス構造体。 使用する必要がある値は STI\_様々\_保留します。 (デバイスが保留中のイベントを待機している、WIA サービスに報告します。)

STI\_様々\_PENDING に設定されている、WIA サービスが WIA ドライバーでイベントが発生したことを通知します。 WIA サービスの呼び出し、 [ **IStiUSD::GetNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543821)イベントに関する詳細を取得します。

**IStiUSD::GetNotificationData**ポーリングされたイベントと割り込みイベント メソッドが呼び出されます。 WIA サービスに戻るに適切なイベント情報を入力する必要がありますが、このメソッドになります。

**注**   、STI を常にオフ\_様々\_保留中のフラグ、 **dwEventHandlingState**デバイス イベントの発生時に正しく設定されていることを確認するにはメンバー。

 

次の例の実装を示しています、 **IStiUSD::GetStatus**メソッド。

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

 

 




