---
title: メソッドとイベントのサンプル ユーザーモード コード
description: メソッドとイベントのサンプル ユーザーモード コード
ms.assetid: 0d564eb7-8e81-43bd-b539-f1240b3a21de
keywords:
- イベント WDK AVStream
- AVStream イベント WDK
- ユーザーモード Ksk プロキシプラグインサンプル WDK AVStream
- 方法 WDK AVStream
- automation テーブル WDK AVStream
- 通知 WDK AVStream
- Ksk プロキシプラグインサンプル WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 286bd3e0f0c650b74b0b9d733c33d139a75a39fe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827377"
---
# <a name="sample-user-mode-code-for-methods-and-events"></a>メソッドとイベントのサンプル ユーザーモード コード


このセクションのコードは、ユーザーモード KsProxy プラグインのメソッドとイベントを使用する方法を示しています。

カーネルモードミニドライバーでのプロパティ、メソッド、およびイベントをサポートする方法については、「[オートメーションテーブルの定義](defining-automation-tables.md)」を参照してください。

特定のメソッドをサポートするミニドライバーを指定した後、次のコード例に示すように、ユーザーモードのプラグインから[**Ikscontrol:: Ksk メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksmethod)を呼び出すことによって、そのメソッドを呼び出すことができます。

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

カーネルモードで指定したオートメーションテーブルでは、 [**Ksk メソッド\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmethod_item)の**Flags**メンバーを使用して、バッファーが読み取り/書き込み可能かどうか、およびマップまたはコピーする必要があるかどうかを指定できます。

ミニドライバーでサポートされているイベントに登録するには、次のユーザーモードコード例を使用します。

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

上の例では、ミニドライバーがイベントを無効にするまで通知が続行されます。 イベントを無効にする場合は。 [**Ikscontrol:: KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksevent)を呼び出します。 このイベントが初めて発生したときにのみ通知を受け取るようにするには、KSEVENT を設定し、ONESHOT で\_を\_入力**します。**

USB ビデオクラス拡張ユニットを使用したイベントをサポートする場合は、「[拡張機能ユニットを使用した自動更新イベントのサポート](supporting-autoupdate-events-with-extension-units.md)」を参照してください。

 

 




