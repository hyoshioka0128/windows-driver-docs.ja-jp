---
title: メソッドとイベントのサンプル ユーザーモード コード
description: メソッドとイベントのサンプル ユーザーモード コード
ms.assetid: 0d564eb7-8e81-43bd-b539-f1240b3a21de
keywords:
- WDK AVStream のイベント
- AVStream イベント WDK
- ユーザー モード KsProxy プラグイン サンプル WDK AVStream
- WDK AVStream メソッド
- automation の WDK AVStream テーブルにします。
- WDK AVStream の通知
- KsProxy プラグイン サンプル WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fafacf2c00c2e0fda66e4aecd17d31978df30a84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355921"
---
# <a name="sample-user-mode-code-for-methods-and-events"></a>メソッドとイベントのサンプル ユーザーモード コード


このセクションのコードでは、メソッドおよびユーザー モードの KsProxy プラグインからイベントを使用する方法を示します。

カーネル モード、ミニドライバーでプロパティ、メソッド、およびイベントをサポートする方法については、次を参照してください。 [Automation テーブルを定義する](defining-automation-tables.md)します。

指定されたメソッドをサポートするミニドライバーを指定したら、呼び出すことによってそのメソッドを呼び出すことができます[ **IKsControl::KsMethod** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksmethod)からユーザー モードの次のコード例に示すようにプラグインします。

```cpp
PVOID MethodBuffer; // Your method arguments buffer
ULONG MethodBufferSize; // Your method buffer size

KSMETHOD Method;
ULONG BytesReturned;

Method.Set = KSMETHODSETID_MyMethodSet;
Method.Id = KSMETHOD_MyMethodId;
Method.Flags = KSMETHOD_TYPE_SEND;

HRESULT hr = 
pIKsControl -> KsMethod (
    &Method,
        sizeof (Method),
    MethodBuffer,
    &MethodBufferSize,
    &BytesReturned);
```

カーネル モードで指定した automation のテーブルで使用することができます、**フラグ**のメンバー [ **KSMETHOD\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmethod_item)バッファーは読み取り/書き込みであるかどうかを指定してかどうかにする必要がありますのマップまたはコピーします。

ミニドライバーでサポートされるイベントに登録するには、次のユーザー モードのコード例を使用します。

```cpp
HANDLE EventHandle; // Your event handle.

KSEVENT Event;
KSEVENTDATA EventData;

Event.Set = KSEVENTSETID_MyEventSet;
Event.Id = KSEVENT_MyEventId;
Event.Flags = KSEVENT_TYPE_ENABLE;

EventData.NotificationType = KSEVENTF_EVENT_HANDLE;
EventData.EventHandle.Event = EventHandle;
EventData.EventHandle.Reserved [0] = 0;
EventData.EventHandle.Reserved [1] = 0;

ULONG BytesReturned;

HRESULT hr =
pIKsControl -> KsEvent (
    &Event,
        sizeof (Event),
    &EventData,
        sizeof (EventData),
    &BytesReturned);
```

上記の例では、通知は、ミニドライバーは、イベントを無効にします。 までを続行します。 イベントを無効にします。 呼び出す[ **IKsControl::KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksevent)します。 最初にこのイベントが発生したときにのみ通知する場合は、設定 KSEVENT\_型\_で ONESHOT **Event.Flags**します。

USB ビデオ クラスの拡張機能のユニット数を持つイベントをサポートしている場合は、次を参照してください。[単位の拡張機能で自動更新のイベントをサポートしている](supporting-autoupdate-events-with-extension-units.md)します。

 

 




