---
title: 拡張ユニットによる自動更新イベントのサポート
description: 拡張ユニットによる自動更新イベントのサポート
ms.assetid: 3dc75f48-adc7-4443-8090-2e61b3306798
keywords:
- 自動更新イベント WDK USB ビデオ クラス
- 自動更新イベント WDK USB ビデオ クラスの拡張ユニット
- WDK USB ビデオ クラスのイベント
- イベント WDK USB ビデオ クラスの拡張単位での自動更新
- 拡張機能ユニット WDK USB ビデオ クラスのサンプル
- サンプル コード WDK USB ビデオ クラス、自動更新イベント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 904f7662fe10907f6dc2e11a250abf3e7a48b2c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378517"
---
# <a name="supporting-autoupdate-events-with-extension-units"></a>拡張ユニットによる自動更新イベントのサポート


このトピックには、自動更新イベントをサポートする方法を示すサンプル コードが含まれています。

任意 TestApp.cpp という名前のアプリケーションのソースで、次のコードを含めます。

```cpp
hEvent = CreateEvent(NULL, FALSE, FALSE, NULL);
if (!hEvent)
{
    printf("CreateEvent failed\n");
    goto errExit;
}
Event.Set = KSEVENTSETID_VIDCAPNotify;
Event.Id = KSEVENT_VIDCAP_AUTO_UPDATE;
Event.Flags = KSEVENT_TYPE_ENABLE;

EventData.NotificationType = KSEVENTF_EVENT_HANDLE;
EventData.EventHandle.Event = hEvent;
EventData.EventHandle.Reserved[0] = 0;
EventData.EventHandle.Reserved[1] = 0;

// register for autoupdate events
hr = m_pKsControl->KsEvent(
    &Event, 
 sizeof(KSEVENT), 
    &EventData, 
 sizeof(KSEVENTDATA), 
    &ulBytesReturned);
if (FAILED(hr))
{
    printf("Failed to register for auto-update event : %x\n", hr);
 goto errExit;
}

// Wait for event for 5 seconds 
dwError = WaitForSingleObject(hEvent, 5000);

// cancel further notifications
hr = m_pKsControl->KsEvent(
    NULL, 
    0, 
    &EventData, 
 sizeof(KSEVENTDATA), 
    &ulBytesReturned);
if (FAILED(hr))  printf("Cancel event returns : %x\n", hr);

if ((dwError == WAIT_FAILED) || 
   (dwError == WAIT_ABANDONED) ||
   (dwError == WAIT_TIMEOUT))
{
    printf("Wait failed : %d\n", dwError);
 goto errExit;
} 
printf("Wait returned : %d\n", dwError);

// handle the autoupdate event..
```

 

 




