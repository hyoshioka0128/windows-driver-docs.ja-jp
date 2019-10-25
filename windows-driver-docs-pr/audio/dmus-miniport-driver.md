---
title: DMus ミニポート ドライバー
description: DMus ミニポート ドライバー
ms.assetid: a0ce6545-2050-49fb-88b5-a75dcd4c7ebc
keywords:
- オーディオミニポートドライバー WDK、DMus
- ミニポートドライバー WDK audio、DMus
- DirectMusic WDK audio, ミニポートドライバー
- DMus ミニポートドライバー WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05604d5e7e738ea44de9ff4acb7f4f55b7f7f1bd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833451"
---
# <a name="dmus-miniport-driver"></a>DMus ミニポート ドライバー


## <span id="dmus_miniport_driver"></span><span id="DMUS_MINIPORT_DRIVER"></span>


DMus ミニポートドライバーは、ハードウェアに依存する高度な MIDI デバイスの機能を管理します。 これらのデバイスは、precision sequencer のタイミング、ダウンロード可能なサウンド (DLS)、チャネルグループなどの DirectMusic 機能をサポートしています。 DMus ミニポートドライバーは、MPU-401 などのデバイスで高パフォーマンスを実現できます。 タイミングは、ハードウェアの機能に応じて、ミニポートドライバーまたはポートドライバーのいずれかで処理できます。 DMus ミニポートドライバーでは、wave 出力ストリームを生成するソフトウェアシンセサイザーをサポートすることもできます。

MIDI ハードウェアデバイス用の DMus ミニポートドライバーは、次の2つのインターフェイスをサポートする必要があります。

-   ミニポートインターフェイスは、ミニポートオブジェクトを初期化し、MIDI ストリームを作成します。

-   ストリームインターフェイスは、MIDI ストリームを管理し、ほとんどのミニポートドライバーの機能を公開します。

ミニポートインターフェイス[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)は、 [IMiniport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiport)インターフェイスのメソッドを継承します。 **IMiniportDMus**には、次の追加のメソッドが用意されています。

[**IMiniportDMus:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-init)

ミニポートオブジェクトを初期化します。

[**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)

新しいストリームオブジェクトを作成します。

[**IMiniportDMus:: Service**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-service)

サービスの要求をミニポートドライバーに通知します。

ストリームインターフェイスである[Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)は、 **IUnknown**インターフェイスのメソッドを継承します。 **Imxf**には、次の追加のメソッドが用意されています。

[**IMXF:: ConnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-connectoutput)

データソースであるこのストリームオブジェクトを、データシンクである別のストリームオブジェクトの**Imxf** interface に接続します。

[**IMXF::D isconnectOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-disconnectoutput)

データシンクである別のストリームオブジェクトの**Imxf** interface からこのストリームオブジェクトを切断します。

[**IMXF::P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)

データシンクに[**Dmus\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)構造体を渡します。

[**IMXF:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-setstate)

ストリームの状態を設定します。

さらに、DMus ミニポートドライバーの[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)インターフェイスは、ソフトウェアシンセサイザーの DLS 機能を提供します。 **ISynthSinkDMus**は、基本インターフェイス**imxf**のメソッドを継承します。 **ISynthSinkDMus**には、次の追加のメソッドが用意されています。

[**ISynthSinkDMus::RefTimeToSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

参照時刻をサンプル時間に変換します。

[**ISynthSinkDMus:: Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render)

Wave データを wave シンクのバッファーにレンダリングします。

[**ISynthSinkDMus:: SampleToRefTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

サンプル時間を参照時刻に変換します。

[**ISynthSinkDMus:: SyncToMaster**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

サンプルクロックをマスタークロックに同期します。

ポートドライバーの wave シンクは、 **ISynthSinkDMus:: Render**を呼び出して、シンセサイザーが MIDI 入力ストリームから生成した wave PCM データを読み取ります。 Wave シンクの詳細については、「[カーネルモードのソフトウェアシンセサイザーの Wave シンク](a-wave-sink-for-kernel-mode-software-synthesizers.md)」を参照してください。

ミニポートドライバーは、DMus ポートドライバーで次のインターフェイスを呼び出します。

[IPortDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)

PortCls には、UART 関数を使用する MIDI デバイス用の組み込みの DMus ミニポートドライバーが含まれています。 詳細については、「 [**Pcnewminiport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)」を参照してください。

 

 




