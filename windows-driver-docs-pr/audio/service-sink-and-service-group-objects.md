---
title: サービス シンクとサービスのグループのオブジェクト
description: サービス シンクとサービスのグループのオブジェクト
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
ms.openlocfilehash: cc28d79bf70282e6598f5fe502a786c4a35c9d0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355264"
---
# <a name="service-sink-and-service-group-objects"></a>サービス シンクとサービスのグループのオブジェクト


## <span id="service_sink_and_service_group_objects"></span><span id="SERVICE_SINK_AND_SERVICE_GROUP_OBJECTS"></span>


PortCls システム ドライバーの実装、 [IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)と[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)ポートおよびミニポート ドライバーのためのインターフェイス。 ポート ドライバーでは、これらのインターフェイスを使用する独自のサービス ルーチンでは、割り込み通知を配布して、ミニポート ドライバーのような目的でこれらのインターフェイスを使用するオプションがあります。 IServiceSink オブジェクトが、サービス ルーチンをカプセル化し、IServiceGroup オブジェクトが IServiceSink オブジェクトのグループを表します。 サービス グループは、サービス要求を受信したときにそのサービスのシンクのそれぞれに要求を配信します。

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)継承[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)します。 サービス グループは、サービス シンクではまた、オーディオ ドライバーがないこの機能の使用を行う通常サービス グループは他のサービス グループを含むことができます。 ポート ドライバーは、サービス グループの機能が他の目的に役立つ可能性のあるさせるほどの汎用現在サービス グループとの割り込みのサービス要求を多重に使用します。

ミニポート ドライバーの割り込みサービス ルーチン (ISR) は、ポート ドライバーで、次の通知方法のいずれかを呼び出します。

[**IPortDMus::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-notify)

[**IPortMidi::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-notify)

[**IPortWaveCyclic::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavecyclic-notify)

[**IPortWavePci::Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepci-notify)

通知方法は、呼び出しのパラメーターとしてサービス グループにポインターを受け取ります。 ポートのドライバーがサービス グループを呼び出し、この呼び出し中に[ **IServiceSink::RequestService** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)メソッドで、遅延プロシージャ呼び出し (DPC) のキューします。 DPC が実行されると、サービス グループ内のすべてのメンバー オブジェクトにサービス要求を転送します。

ミニポート ドライバー コード通常しなくてもいずれかを呼び出す[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)インターフェイスのメソッド。 ただし、ポート ドライバー メソッドが呼び出される追加する独自[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)ミニポート ドライバーから取得するサービス グループにオブジェクト。 ミニポート ドライバーでは、必要に応じてサービス グループ オブジェクトを作成し、それらのサービス グループを定期的な処理を必要とするミニポートおよびストリームのオブジェクトに関連付けます。 たとえば、WaveCyclic ミニポート ドライバー グループに関連付けますストリーム オブジェクト、サービスへの出力パラメーターとして指定された、 [ **IMiniportWaveCyclic::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)メソッド。

WaveCyclic ミニポート ドライバーのコンテキストでの原因のすべてのストリームを 1 つのサービス グループに関連付ける 1 つの通知に基づくすべてのストリームを処理するポート ドライバー。 各ストリームを独自のサービス グループに関連付けるには、DPC の実行中に、ポート ドライバーによって処理されるストリームを選択する割り込みサービス ルーチンが使用できます。

ミニポート ドライバーは、ポート ドライバーでは、次の初期化方法のいずれかを呼び出すと、そのサービスのグループへの参照を出力します。

[**IMiniportDMus::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportWavePci::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)

ポートのドライバーを追加、独自[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)オブジェクトから取得するサービスのグループに、 **Init**呼び出します。 ミニポート ドライバーの ISR が後で呼び出すときに**通知**サービス グループが順番に通知を転送する、ポート ドライバーの IServiceSink オブジェクトへの通知を転送する DPC をキュー サービス グループに通知を送信するには次のサービス メソッドのいずれかを呼び出してミニポート ドライバー:

[**IMiniportDMus::Service** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-service) (未使用)

[**IMiniportMidi::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-service)

[**IMiniportWavePci::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-service)

ミニポート ドライバーでは、ポート ドライバーは、次のストリームの作成方法のいずれかを呼び出すときにそのサービスのグループへの参照も出力されます。

[**IMiniportDMus::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)

[**IMiniportMidi::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportmidi-newstream)

[**IMiniportWaveCyclic::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclic-newstream)

[**IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)

前述のように、ミニポート ドライバーによって各ストリームの別のサービス グループを作成するか、1 つのサービス グループのすべてのストリーム間で共有のオプションがあります。

次のメソッドのヘルプ MIDI と Dmu ポート ドライバーがハードウェア割り込みの削除を回避します。

[**IPortMidi::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportmidi-registerservicegroup)

[**IPortDMus::RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

実行中にその**Init**メソッド、MIDI または Dmu のミニポート ドライバーは通常、ポート ドライバーの呼び出す**RegisterServiceGroup**シンセサイザーを開始する前にメソッド。 この呼び出しの目的では、サービスのグループにポート ドライバーは、(その割り込みハンドラーを含む)、そのサービス シンク オブジェクトの挿入を許可するのにはハードウェアは、割り込みの生成を開始する前にです。 ただし、 **Init**メソッドの出力ポート ドライバーへのサービス グループ ポインター、ポート ドライバーからの戻り値の後にのみ、このポインターを使用する**Init**。

WavePci ポート ドライバーでは、場合、ポート オブジェクトを追加独自[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)オブジェクトから取得するサービスのグループに、 [ **IMiniportWavePci::NewStream** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)呼び出します。 ミニポート ドライバーの ISR が後で呼び出すときに**通知**サービス グループが、ポート ドライバーの IServiceSink オブジェクトは、さらに実行すると、次に、通知を転送する DPC をキュー サービス グループに通知を送信します。

-   サービス メソッドを呼び出すことによって、ミニポート ストリームへの通知を転送[ **IMiniportWavePciStream::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-service)します。

-   位置やクロックのイベントを暗証番号 (pin) を起動することができるをトリガーします。

[IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)インターフェイスは、1 つのメソッドをサポートしています。

[**IServiceSink::RequestService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicesink-requestservice)

[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)インターフェイスは、次のメソッドをサポートしています。

[**IServiceGroup::AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-addmember)

[**IServiceGroup::CancelDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-canceldelayedservice)

[**IServiceGroup::RequestDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-requestdelayedservice)

[**IServiceGroup::RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-removemember)

[**IServiceGroup::SupportDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iservicegroup-supportdelayedservice)

さらに、PortCls システム ドライバーが提供、 [ **PcNewServiceGroup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewservicegroup)新しいサービス グループ オブジェクトを作成するための関数。 ただし、サービス シンク オブジェクトを作成するのと同様の関数は存在しません。 単純にポート ドライバーを追加、 [IServiceSink](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicesink)インターフェイス - メイン ポート オブジェクトの実装にオブジェクトが作成されると、これはサービス シンク。 ポート ドライバーは、ミニポート ドライバーから受信するサービスのグループに、ポート オブジェクトの IServiceSink インターフェイスを追加することができます**Init**または**NewStream**メソッド。 便宜上、ヘッダー ファイル Portcls.h を定義します**IMP\_IServiceSink**と**IMP\_IServiceGroup** IServiceSink を追加するための定数と[IServiceGroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iservicegroup)ドライバー オブジェクトへのインターフェイス。

 

 




