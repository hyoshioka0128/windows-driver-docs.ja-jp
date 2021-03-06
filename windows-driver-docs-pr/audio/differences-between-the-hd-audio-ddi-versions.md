---
title: HD オーディオ DDI バージョン間の相違点
description: HD オーディオ DDI バージョン間の相違点
ms.assetid: e24071d3-9021-40c0-907a-91ada8a1306b
keywords:
- HD オーディオ、DDI のバージョンの違い
- Hd オーディオ (HD オーディオ) DDI のバージョンの違い
- HDAUDIO_BUS_INTERFACE 構造体
- HDAUDIO_BUS_INTERFACE_BDL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 799483b2133c751b9951a0a48e7e5b2564de0c89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359060"
---
# <a name="differences-between-the-hd-audio-ddi-versions"></a>HD オーディオ DDI バージョン間の相違点


HD オーディオ DDI には次のように定義されている 3 つの異なるバージョンがあります。

-   定義されている HD オーディオ DDI のベースライン バージョン、 [ **HDAUDIO\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造体。 オーディオとモデムのコーデックのほとんどの関数のドライバーでは、この DDI バージョンが用意されている機能のみが必要です。 このバージョンは、Windows XP および Windows Vista で提供される HD オーディオ バス ドライバーを利用します。

-   定義されている HD オーディオ DDI の拡張のバージョン、 [ **HDAUDIO\_BUS\_インターフェイス\_V2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体。 DDI のこのバージョンは、柔軟性を DMA 駆動のイベント通知をサポートするために必要な追加機能を提供します。 Windows Vista 以降のバージョンの Windows で使用可能になります。

-   HD オーディオ DDI で定義されているは、次の変更済み、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体。 このバージョンの要件に対応するオーディオとモデムの数が比較的少ないドライバーのセットアップをさらに制御が必要なバッファーの DMA 操作記述子のリスト (BDLs)。 DDI のこのバージョンは、Windows XP および以降のバージョンの Windows で使用できます。 ただし、いずれか、HDAUDIO を使用して、\_BUS\_インターフェイスまたは、HDAUDIO\_BUS\_インターフェイス\_V2 DDI バージョン代わりにします。 .

すべての 3 つの構造に名前と最初の 5 つのメンバーの型の一致の 5 つのメンバー、 [**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)構造体。 これらのメンバーの値の詳細については、次を参照してください[、HDAUDIO を取得する\_BUS\_インターフェイス DDI オブジェクト](obtaining-an-hdaudio-bus-interface-ddi-object.md)、 [、HDAUDIO を取得する\_BUS\_インターフェイス。\_V2 DDI オブジェクト](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)または[取得、HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクト](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)します。

HD オーディオ DDI の 3 つのバージョンのルーチンでは、次のタスクを実行します。

-   コーデックにコマンドを転送し、これらのコマンドに応答を取得します。

-   割り当て、レンダリングのデータを転送して、ストリームをキャプチャする DMA エンジンを設定します。

-   実行中、一時停止、停止、またはリセットするには、1 つまたは複数の DMA エンジンのストリームの状態を変更します。

-   レンダリングのリンクの帯域幅を確保し、ストリームをキャプチャします。

-   ウォール クロックのレジスタへの直接アクセスを提供し、位置のレジスタをリンクします。

-   要請されていない応答コーデックからのクライアントに通知します。

-   カーネル イベントを登録し、DMA の進行状況の通知を受信できるようにします。

HDAUDIO\_BUS\_インターフェイスと HDAUDIO\_BUS\_インターフェイス\_DDI の BDL バージョンは、次の点をいます。

-   HDAUDIO\_BUS\_インターフェイス構造体は、2 つのルーチンを定義します[ **AllocateDmaBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_dma_buffer)と[ **FreeDmaBuffer** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_dma_buffer)、HDAUDIO に存在しない\_BUS\_インターフェイス\_BDL します。

-   HDAUDIO\_BUS\_インターフェイス\_BDL 構造は、3 つのルーチンを定義します[ **SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)、 [  **。AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)、および[ **FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)、HDAUDIO に存在しない\_BUS\_インターフェイスです。

クライアントが呼び出すときに、 **AllocateDmaBuffer** DDI の最初のバージョンで日常的な HD オーディオ バス ドライバー。

-   DMA バッファーと使用の DMA エンジン BDL を割り当てます。

-   BDL を初期化します。

-   DMA エンジンを設定すると、バッファーと BDL を使用します。

これに対し、 **AllocateContiguousDmaBuffer** 2 番目の日常的な DDI バージョン DMA バッファーと BDL、記憶域を割り当てますが、BDL を初期化するために、呼び出し元に依存します。 **SetupDmaEngineWithBdl**ルーチンは、バッファーと呼び出し元初期化 BDL を使用する、DMA エンジンを設定します。

BDL には、DMA エンジンのスキャッター/ギャザー キュー内の物理メモリ ブロックの一覧が含まれています。 呼び出して**SetupDmaEngineWithBdl** BDL を設定するクライアントは、割り込みが DMA エンジンによって生成されるデータ ストリームで、ポイントを指定できます。 クライアントは、選択 BDL エントリで、割り込みの完了時 (IOC) のビットを設定しています。 この機能により、クライアントは、オーディオ ストリームの処理中に発生する IOC 割り込みのタイミングを正確に制御することができます。 オーディオのモデム ドライバーでは、正確なシステム時計の情報を取得するのに 2 つ目の DDI バージョンを使用することもできます。

詳細については、次を参照してください。、 *Intel 高度な定義オーディオ仕様*します。

ただし、ほぼすべてのクライアントでは、HDAUDIO は使用\_BUS\_DDI のインターフェイスのバージョン。 割り込みのタイミングを正確に制御を必要とするいくつかのクライアントが、HDAUDIO を使用してのみ\_BUS\_インターフェイス\_BDL バージョン。

 

 




