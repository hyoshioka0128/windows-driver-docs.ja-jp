---
title: サービスのシンクとサービスのグループ オブジェクト
description: サービスのシンクとサービスのグループ オブジェクト
ms.assetid: 00e17e01-8889-4fae-a0ff-e110d7a9b21e
keywords:
- ヘルパー オブジェクト WDK オーディオ、サービス シンク オブジェクト
- ヘルパー オブジェクト WDK オーディオ、サービス グループ オブジェクト
- サービス シンク オブジェクトの WDK オーディオ
- サービス グループ オブジェクトの WDK オーディオ
- IServiceSink インターフェイス
- IServiceGroup インターフェイス
- 割り込み通知 WDK オーディオを配布します。
- 通知の WDK オーディオ
- 割り込み通知 WDK オーディオ
- 割り込みサービス ルーチン WDK オーディオ
- Isr WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d74c1d4e44e8c0721c586fe1499bce0c56735fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539106"
---
# <a name="service-sink-and-service-group-objects"></a>サービスのシンクとサービスのグループ オブジェクト


## <span id="service_sink_and_service_group_objects"></span><span id="SERVICE_SINK_AND_SERVICE_GROUP_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)と[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)ポートおよびミニポート ドライバーのためのインターフェイス。 ポート ドライバーでは、これらのインターフェイスを使用する独自のサービス ルーチンでは、割り込み通知を配布して、ミニポート ドライバーのような目的でこれらのインターフェイスを使用するオプションがあります。 IServiceSink オブジェクトが、サービス ルーチンをカプセル化し、IServiceGroup オブジェクトが IServiceSink オブジェクトのグループを表します。 サービス グループは、サービス要求を受信したときにそのサービスのシンクのそれぞれに要求を配信します。

[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)継承[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)します。 サービス グループは、サービス シンクではまた、オーディオ ドライバーがないこの機能の使用を行う通常サービス グループは他のサービス グループを含むことができます。 ポート ドライバーは、サービス グループの機能が他の目的に役立つ可能性のあるさせるほどの汎用現在サービス グループとの割り込みのサービス要求を多重に使用します。

ミニポート ドライバーの割り込みサービス ルーチン (ISR) は、ポート ドライバーで、次の通知方法のいずれかを呼び出します。

[**IPortDMus::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536880)

[**IPortMidi::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536893)

[**IPortWaveCyclic::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536903)

[**IPortWavePci::Notify**](https://msdn.microsoft.com/library/windows/hardware/ff536918)

通知方法は、呼び出しのパラメーターとしてサービス グループにポインターを受け取ります。 ポートのドライバーがサービス グループを呼び出し、この呼び出し中に[ **IServiceSink::RequestService** ](https://msdn.microsoft.com/library/windows/hardware/ff537009)メソッドで、遅延プロシージャ呼び出し (DPC) のキューします。 DPC が実行されると、サービス グループ内のすべてのメンバー オブジェクトにサービス要求を転送します。

ミニポート ドライバー コード通常しなくてもいずれかを呼び出す[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)インターフェイスのメソッド。 ただし、ポート ドライバー メソッドが呼び出される追加する独自[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)ミニポート ドライバーから取得するサービス グループにオブジェクト。 ミニポート ドライバーでは、必要に応じてサービス グループ オブジェクトを作成し、それらのサービス グループを定期的な処理を必要とするミニポートおよびストリームのオブジェクトに関連付けます。 たとえば、WaveCyclic ミニポート ドライバー グループに関連付けますストリーム オブジェクト、サービスへの出力パラメーターとして指定された、 [ **IMiniportWaveCyclic::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536723)メソッド。

WaveCyclic ミニポート ドライバーのコンテキストでの原因のすべてのストリームを 1 つのサービス グループに関連付ける 1 つの通知に基づくすべてのストリームを処理するポート ドライバー。 各ストリームを独自のサービス グループに関連付けるには、DPC の実行中に、ポート ドライバーによって処理されるストリームを選択する割り込みサービス ルーチンが使用できます。

ミニポート ドライバーは、ポート ドライバーでは、次の初期化方法のいずれかを呼び出すと、そのサービスのグループへの参照を出力します。

[**IMiniportDMus::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536700)

[**IMiniportMidi::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536709)

[**IMiniportWavePci::Init**](https://msdn.microsoft.com/library/windows/hardware/ff536734)

ポートのドライバーを追加、独自[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)オブジェクトから取得するサービスのグループに、 **Init**呼び出します。 ミニポート ドライバーの ISR が後で呼び出すときに**通知**サービス グループが順番に通知を転送する、ポート ドライバーの IServiceSink オブジェクトへの通知を転送する DPC をキュー サービス グループに通知を送信するには次のサービス メソッドのいずれかを呼び出してミニポート ドライバー:

[**IMiniportDMus::Service** ](https://msdn.microsoft.com/library/windows/hardware/ff536702) (未使用)

[**IMiniportMidi::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536711)

[**IMiniportWavePci::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536736)

ミニポート ドライバーでは、ポート ドライバーは、次のストリームの作成方法のいずれかを呼び出すときにそのサービスのグループへの参照も出力されます。

[**IMiniportDMus::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536701)

[**IMiniportMidi::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536710)

[**IMiniportWaveCyclic::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536723)

[**IMiniportWavePci::NewStream**](https://msdn.microsoft.com/library/windows/hardware/ff536735)

前述のように、ミニポート ドライバーによって各ストリームの別のサービス グループを作成するか、1 つのサービス グループのすべてのストリーム間で共有のオプションがあります。

次のメソッドのヘルプ MIDI と Dmu ポート ドライバーがハードウェア割り込みの削除を回避します。

[**IPortMidi::RegisterServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff536895)

[**IPortDMus::RegisterServiceGroup**](https://msdn.microsoft.com/library/windows/hardware/ff536882)

実行中にその**Init**メソッド、MIDI または Dmu のミニポート ドライバーは通常、ポート ドライバーの呼び出す**RegisterServiceGroup**シンセサイザーを開始する前にメソッド。 この呼び出しの目的では、サービスのグループにポート ドライバーは、(その割り込みハンドラーを含む)、そのサービス シンク オブジェクトの挿入を許可するのにはハードウェアは、割り込みの生成を開始する前にです。 ただし、 **Init**メソッドの出力ポート ドライバーへのサービス グループ ポインター、ポート ドライバーからの戻り値の後にのみ、このポインターを使用する**Init**。

WavePci ポート ドライバーでは、場合、ポート オブジェクトを追加独自[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)オブジェクトから取得するサービスのグループに、 [ **IMiniportWavePci::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)呼び出します。 ミニポート ドライバーの ISR が後で呼び出すときに**通知**サービス グループが、ポート ドライバーの IServiceSink オブジェクトは、さらに実行すると、次に、通知を転送する DPC をキュー サービス グループに通知を送信します。

-   サービス メソッドを呼び出すことによって、ミニポート ストリームへの通知を転送[ **IMiniportWavePciStream::Service**](https://msdn.microsoft.com/library/windows/hardware/ff536731)します。

-   位置やクロックのイベントを暗証番号 (pin) を起動することができるをトリガーします。

[IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)インターフェイスは、1 つのメソッドをサポートしています。

[**IServiceSink::RequestService**](https://msdn.microsoft.com/library/windows/hardware/ff537009)

[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)インターフェイスは、次のメソッドをサポートしています。

[**IServiceGroup::AddMember**](https://msdn.microsoft.com/library/windows/hardware/ff536996)

[**IServiceGroup::CancelDelayedService**](https://msdn.microsoft.com/library/windows/hardware/ff536997)

[**IServiceGroup::RequestDelayedService**](https://msdn.microsoft.com/library/windows/hardware/ff537003)

[**IServiceGroup::RemoveMember**](https://msdn.microsoft.com/library/windows/hardware/ff537001)

[**IServiceGroup::SupportDelayedService**](https://msdn.microsoft.com/library/windows/hardware/ff537004)

さらに、PortCls システム ドライバーが提供、 [ **PcNewServiceGroup** ](https://msdn.microsoft.com/library/windows/hardware/ff537719)新しいサービス グループ オブジェクトを作成するための関数。 ただし、サービス シンク オブジェクトを作成するのと同様の関数は存在しません。 単純にポート ドライバーを追加、 [IServiceSink](https://msdn.microsoft.com/library/windows/hardware/ff537006)インターフェイス - メイン ポート オブジェクトの実装にオブジェクトが作成されると、これはサービス シンク。 ポート ドライバーは、ミニポート ドライバーから受信するサービスのグループに、ポート オブジェクトの IServiceSink インターフェイスを追加することができます**Init**または**NewStream**メソッド。 便宜上、ヘッダー ファイル Portcls.h を定義します**IMP\_IServiceSink**と**IMP\_IServiceGroup** IServiceSink を追加するための定数と[IServiceGroup](https://msdn.microsoft.com/library/windows/hardware/ff536994)ドライバー オブジェクトへのインターフェイス。

 

 




