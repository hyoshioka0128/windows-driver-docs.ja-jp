---
title: DMus ミニポート ドライバー
description: DMus ミニポート ドライバー
ms.assetid: a0ce6545-2050-49fb-88b5-a75dcd4c7ebc
keywords:
- オーディオのミニポート ドライバー WDK、Dmu
- ミニポート ドライバー WDK オーディオ、Dmu
- DirectMusic WDK オーディオ、ミニポート ドライバー
- Dmu ミニポート ドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cca1a14a339fa2fcb0eadceb587140a67218c64e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360112"
---
# <a name="dmus-miniport-driver"></a>DMus ミニポート ドライバー


## <span id="dmus_miniport_driver"></span><span id="DMUS_MINIPORT_DRIVER"></span>


Dmu のミニポート ドライバーでは、高度な MIDI デバイスのハードウェアに依存する機能を管理します。 これらのデバイスでは、有効桁数 sequencer のタイミング、ダウンロード可能なサウンド (DL) およびチャネル グループなどの DirectMusic 機能をサポートします。 Dmu のミニポート ドライバーでは、片方などのデバイスで高パフォーマンスを実現できます。 タイミングは、ミニポート ドライバーまたはハードウェアの機能に応じて、ポート ドライバーのいずれかで処理されることができます。 Dmu のミニポート ドライバーでは、シンセサイザー wave 出力ストリームを生成するソフトウェアもサポートできます。

MIDI ハードウェア デバイス用の Dmu ミニポート ドライバーには、2 つのインターフェイスをサポートする必要があります。

-   ミニポート インターフェイスは、ミニポート オブジェクトを初期化し、MIDI ストリームを作成します。

-   ストリーム インターフェイスでは、MIDI ストリームを管理し、ミニポート ドライバーの機能のほとんどを公開します。

ミニポート インターフェイス[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)でメソッドを継承、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiport)インターフェイス。 **IMiniportDMus**次の追加のメソッドを提供します。

[**IMiniportDMus::Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-init)

ミニポート オブジェクトを初期化します。

[**IMiniportDMus::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)

新しいストリーム オブジェクトを作成します。

[**IMiniportDMus::Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-service)

サービスに対する要求のミニポート ドライバーに通知します。

ストリーム インターフェイス、 [IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)でメソッドを継承、 **IUnknown**インターフェイス。 **IMXF**次の追加のメソッドを提供します。

[**IMXF::ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-connectoutput)

データ ソースが、このストリーム オブジェクトを接続、 **IMXF**データ シンクは、別のストリーム オブジェクトのインターフェイス。

[**IMXF::DisconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-disconnectoutput)

このストリーム オブジェクトからの切断、 **IMXF**データ シンクは、別のストリーム オブジェクトのインターフェイス。

[**IMXF::PutMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-putmessage)

パスを[ **DMU\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/ns-dmusicks-_dmus_kernel_event)データ シンクへの構造体。

[**IMXF::SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imxf-setstate)

ストリームの状態を設定します。

さらに、Dmu のミニポート ドライバーの[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)インターフェイス ソフトウェア シンセサイザー DLS 機能を提供します。 **ISynthSinkDMus**基底インターフェイスでメソッドを継承**IMXF**します。 **ISynthSinkDMus**次の追加のメソッドを提供します。

[**ISynthSinkDMus::RefTimeToSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

参照の時間をサンプル時間に変換します。

[**ISynthSinkDMus::Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-render)

Wave シンクのバッファーには、wave データを表示します。

[**ISynthSinkDMus::SampleToRefTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

サンプルを参照の時刻に変換します。

[**ISynthSinkDMus::SyncToMaster**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

マスターの時計をサンプルのクロックを同期します。

ポート ドライバーのウェーブ シンクを呼び出す**ISynthSinkDMus::Render** wave PCM を読み取り、MIDI からシンセサイザーを生成するデータの入力ストリーム。 Wave シンクの詳細については、次を参照してください。[カーネル モードのソフトウェアのシンセサイザーの A Wave シンク](a-wave-sink-for-kernel-mode-software-synthesizers.md)します。

ミニポート ドライバーでは、Dmu ポート ドライバーで、次のインターフェイスを呼び出します。

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iportdmus)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)

PortCls には UART 関数を使用した、MIDI デバイス用の組み込み Dmu ミニポート ドライバーが含まれています。 詳細については、次を参照してください。 [ **PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)します。

 

 




