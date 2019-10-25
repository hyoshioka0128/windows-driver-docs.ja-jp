---
title: サービス シンクとサービスのグループのオブジェクト
description: サービス シンクとサービスのグループのオブジェクト
ms.assetid: 00e17e01-8889-4fae-a0ff-e110d7a9b21e
keywords:
- ヘルパーオブジェクト WDK オーディオ、サービスシンクオブジェクト
- ヘルパーオブジェクト WDK オーディオ、サービスグループオブジェクト
- サービスシンクオブジェクト WDK オーディオ
- サービスグループオブジェクト WDK オーディオ
- Iサービスインクインターフェイス
- IServiceGroup インターフェイス
- 割り込み通知の配布 (WDK audio)
- 通知 WDK オーディオ
- 割り込み通知の WDK オーディオ
- 割り込みサービスルーチン WDK オーディオ
- Isr WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8308f461877f386518c3c042c07eaef5cf4ec4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830175"
---
# <a name="service-sink-and-service-group-objects"></a>サービス シンクとサービスのグループのオブジェクト


## <span id="service_sink_and_service_group_objects"></span><span id="SERVICE_SINK_AND_SERVICE_GROUP_OBJECTS"></span>


PortCls システムドライバーは、ポートおよびミニポートドライバーの利点を得るために、 [iサービス](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)インターフェイスと[iservicesink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)インターフェイスを実装しています。 ポートドライバーは、これらのインターフェイスを使用して割り込み通知を独自のサービスルーチンに配布します。また、ミニポートドライバーは、これらのインターフェイスを同様の目的で使用するオプションを備えています。 Iservices Ink オブジェクトはサービスルーチンをカプセル化し、Iservicesink オブジェクトは iservices Ink オブジェクトのグループを表します。 サービスグループはサービス要求を受け取ると、その要求を各サービスシンクに配布します。

[Iservicegroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)は[Iサービスのインク](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)から継承します。 サービスグループはサービスシンクでもあるため、サービスグループは他のサービスグループを含むことができますが、通常、オーディオドライバーはこの機能を使用しません。 現在、ポートドライバーは、割り込みサービスの要求を多重化するためにサービスグループを使用しています。ただし、サービスグループの機能は、他の目的にも役立つ可能性があります。

ミニポートドライバーの割り込みサービスルーチン (ISR) は、ポートドライバーで次のいずれかの通知方法を呼び出します。

[**IPortDMus:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-notify)

[**IPortMidi:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-notify)

[**IPortWaveCyclic:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-notify)

[**IPortWavePci:: Notify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepci-notify)

通知メソッドは、サービスグループへのポインターを呼び出しパラメーターとして受け取ります。 この呼び出しの間、ポートドライバーは、遅延プロシージャ呼び出し (DPC) をキューに置いたサービスグループの[**iservices ink:: requestservice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)メソッドを呼び出します。 DPC が実行されると、サービスグループ内のすべてのメンバーオブジェクトにサービス要求が転送されます。

通常、ミニポートドライバーコードでは、 [Iservicegroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)インターフェイスメソッドを呼び出す必要はありません。 ただし、ポートドライバーは、これらのメソッドを呼び出して、ミニポートドライバーから取得したサービスグループに独自の[iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)オブジェクトを追加します。 ミニポートドライバーは、必要に応じてサービスグループオブジェクトを作成し、それらのサービスグループを、定期的なサービスを必要とするミニポートおよびストリームオブジェクトに関連付けます。 たとえば、WaveCyclic ミニポートドライバーは、 [**IMiniportWaveCyclic:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)メソッドに出力パラメーターとして指定されているサービスグループにストリームオブジェクトを関連付けます。

WaveCyclic ミニポートドライバーのコンテキストでは、すべてのストリームを1つのサービスグループに関連付けることにより、ポートドライバーは1つの通知に基づいてすべてのストリームを処理します。 各ストリームをそれぞれのサービスグループに関連付けることにより、割り込みサービスルーチンは、DPC の実行中にポートドライバーによって処理されるストリームを選択できます。

ポートドライバーが次のいずれかの初期化メソッドを呼び出すと、ミニポートドライバーはそのサービスグループへの参照を出力します。

[**IMiniportDMus:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

[**IMiniportMidi:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-init)

[**IMiniportWavePci:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init)

ポートドライバーは、 **Init**呼び出しから取得したサービスグループに、独自の[iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)オブジェクトを追加します。 その後、ミニポートドライバーの ISR が通知を呼び出して、そのサービスグループに通知を**送信すると**、サービスグループは、ポートドライバーの Iservices ink オブジェクトに通知を転送する DPC をキューに入れます。次のいずれかのサービスメソッドを呼び出します。

[**IMiniportDMus:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-service) (使用されていません)

[**IMiniportMidi:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-service)

[**IMiniportWavePci:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-service)

また、ポートドライバーが次のストリーム作成メソッドのいずれかを呼び出すと、そのサービスグループへの参照も出力されます。

[**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)

[**IMiniportMidi:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportmidi-newstream)

[**IMiniportWaveCyclic:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclic-newstream)

[**IMiniportWavePci:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)

前に説明したように、ミニポートドライバーには、ストリームごとに異なるサービスグループを作成するか、すべてのストリームで1つのサービスグループを共有するオプションがあります。

次のメソッドを使用すると、MIDI および DMus ポートドライバーがハードウェア割り込みを削除するのを防ぐことができます。

[**IPortMidi:: RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportmidi-registerservicegroup)

[**IPortDMus:: RegisterServiceGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iportdmus-registerservicegroup)

**Init**メソッドの実行中、通常、MIDI または dmus ミニポートドライバーは、シンセサイザーを起動する前に、ポートドライバーの**registerservicegroup**メソッドを呼び出します。 この呼び出しの目的は、ハードウェアが割り込みの生成を開始する前に、ポートドライバーがその割り込みハンドラーを含むサービスシンクオブジェクトをサービスグループに挿入できるようにすることです。 **Init**メソッドはポートドライバーへのサービスグループポインターを出力しますが、ポートドライバーは、 **init**からの戻り値の後にのみこのポインターを利用できます。

WavePci port ドライバーの場合、ポートオブジェクトは、 [**IMiniportWavePci:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)呼び出しから取得したサービスグループに独自の[iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)オブジェクトを追加します。 その後、ミニポートドライバーの ISR が通知を呼び出して、そのサービスグループに通知を**送信すると**、サービスグループは、ポートドライバーの Iサービスインクオブジェクトに通知を転送する DPC をキューに入れます。このオブジェクトは、次の処理を行います。

-   サービスメソッド[**IMiniportWavePciStream:: service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-service)を呼び出して、通知をミニポートストリームに転送します。

-   起動準備ができているピン上の任意の位置またはクロックイベントをトリガーします。

[Iサービスインク](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)インターフェイスは、次の1つのメソッドをサポートしています。

[**Iservices Ink:: RequestService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicesink-requestservice)

[Iservicegroup](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)インターフェイスは、次のメソッドをサポートしています。

[**IServiceGroup:: AddMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-addmember)

[**IServiceGroup:: CancelDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-canceldelayedservice)

[**IServiceGroup:: RequestDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-requestdelayedservice)

[**IServiceGroup:: RemoveMember**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-removemember)

[**IServiceGroup:: SupportDelayedService**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iservicegroup-supportdelayedservice)

また、PortCls システムドライバーには、新しいサービスグループオブジェクトを作成するための[**Pcnewservicegroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewservicegroup)関数が用意されています。 ただし、サービスシンクオブジェクトを作成するための類似した関数は存在しません。 ポートドライバーは、主なポートオブジェクトの実装に[iservices ink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicesink)インターフェイスを追加するだけです。オブジェクトが作成されると、サービスシンクになります。 ポートドライバーは、ポートオブジェクトの Iサービスインクインターフェイスを、ミニポートドライバーの**Init**または**newstream**メソッドから受信したサービスグループに追加できます。 便宜上、ヘッダーファイル Portcls では、iservicesink インターフェイスと[iservicesink](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iservicegroup)インターフェイスをドライバーオブジェクトに追加するための **\_iservicesink**定数としてを **\_** 定義しています。

 

 




