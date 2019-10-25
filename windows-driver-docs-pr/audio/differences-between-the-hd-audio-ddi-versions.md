---
title: HD オーディオ DDI バージョン間の相違点
description: HD オーディオ DDI バージョン間の相違点
ms.assetid: e24071d3-9021-40c0-907a-91ada8a1306b
keywords:
- HD audio、DDI バージョンの相違点
- High Definition Audio (HD audio)、DDI バージョンの違い
- HDAUDIO_BUS_INTERFACE 構造体
- HDAUDIO_BUS_INTERFACE_BDL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2431a5f9a999b5ce9375b006088436dfcbeb3659
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833551"
---
# <a name="differences-between-the-hd-audio-ddi-versions"></a>HD オーディオ DDI バージョン間の相違点


HD audio DDI は、次のように定義されている3つのわずかなバージョンで使用できます。

-   HD audio DDI のベースラインバージョン。 [**hdaudio\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造によって定義されます。 オーディオおよびモデムコーデックのほとんどの関数ドライバーには、この DDI バージョンで提供される機能のみが必要です。 このバージョンは、Windows XP および Windows Vista に付属している HD オーディオバスドライバーを通じて入手できます。

-   [**Hdaudio\_BUS\_INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体で定義されている HD audio DDI の拡張バージョン。 このバージョンの DDI は、柔軟性のある DMA ドリブンイベント通知をサポートするために必要な追加機能を提供します。 Windows Vista 以降のバージョンの Windows で使用できます。

-   [**Hdaudio\_BUS\_INTERFACE\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体で定義されている HD audio DDI の修正バージョン。 このバージョンは、DMA 操作用のバッファー記述子リスト (BDLs) の設定を追加で制御する必要がある、比較的少数のオーディオおよびモデムドライバーの要件に対応しています。 このバージョンの DDI は、Windows XP 以降のバージョンの Windows で使用できます。 ただし、HDAUDIO\_BUS\_インターフェイスまたは HDAUDIO\_BUS\_INTERFACE\_V2 DDI バージョンのいずれかを使用してください。 の順に移動します。

3つのすべての構造体では、最初の5つのメンバーの名前と型が、[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)構造の5つのメンバーの名前と型に一致します。 これらのメンバーの値の詳細については、「 [hdaudio\_bus\_INTERFACE DDI オブジェクトの取得](obtaining-an-hdaudio-bus-interface-ddi-object.md)」、「 [hdaudio\_bus\_INTERFACE\_V2 DDI オブジェクト](obtaining-an-hdaudio-bus-interface-v2-ddi-object.md)の取得」、または「hdaudio の取得」を参照してください[\_バス\_インターフェイス\_BDL DDI オブジェクト](obtaining-an-hdaudio-bus-interface-bdl-ddi-object.md)。

HD audio DDI の3つのバージョンのルーチンでは、次のタスクを実行します。

-   コマンドをコーデックに転送し、それらのコマンドに対する応答を取得します。

-   レンダーストリームとキャプチャストリームでデータを転送するために、DMA エンジンを割り当てて設定します。

-   1つ以上の DMA エンジンのストリームの状態を "実行中"、"一時停止"、"停止"、または "リセット" に変更します。

-   レンダーストリームとキャプチャストリームのリンク帯域幅を確保します。

-   ウォールクロックレジスタとリンク位置レジスタへの直接アクセスを提供します。

-   コーデックからの要請していない応答をクライアントに通知します。

-   カーネルイベントを登録して、DMA の進行状況に関する通知を受信できるようにします。

HDAUDIO\_BUS\_INTERFACE および HDAUDIO\_BUS\_INTERFACE\_BDL バージョンの DDI では、次の点が異なります。

-   HDAUDIO\_BUS\_インターフェイス構造では、HDAUDIO\_BUS\_INTERFACE\_BDL に存在しない2つのルーチン[**AllocateDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_dma_buffer)と[**FreeDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_dma_buffer)が定義されています。

-   HDAUDIO\_BUS\_INTERFACE\_BDL 構造体は、HDAUDIO\_BUS に存在しない3つのルーチン、 [**SetupDmaEngineWithBdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-psetup_dma_engine_with_bdl)、 [**AllocateContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer)、 [**FreeContiguousDmaBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pfree_contiguous_dma_buffer)を定義します。\_インターフェイス。

クライアントが最初の DDI バージョンで**AllocateDmaBuffer**ルーチンを呼び出すと、HD オーディオバスドライバーは次のようになります。

-   Dma エンジンが使用する DMA バッファーと BDL を割り当てます。

-   BDL を初期化します。

-   バッファーと BDL を使用するように DMA エンジンを設定します。

これに対して、2番目の DDI バージョンの**AllocateContiguousDmaBuffer**ルーチンは DMA バッファーと bdl のストレージを割り当てますが、呼び出し元に依存して bdl を初期化します。 **SetupDmaEngineWithBdl**ルーチンは、バッファーと呼び出し元に初期化された bdl を使用するように DMA エンジンを設定します。

BDL には、DMA エンジンのスキャッター/ギャザーキューにある物理メモリブロックの一覧が含まれています。 **SetupDmaEngineWithBdl**を呼び出して bdl を設定することにより、クライアントは、DMA エンジンが割り込みを生成するデータストリーム内のポイントを指定できます。 クライアントは、選択された BDL エントリで、入力候補 (IOC) ビットを設定することによってこれを行います。 この機能を使用すると、クライアントは、オーディオストリームの処理中に発生する IOC 割り込みのタイミングを正確に制御できます。 また、オーディオモデムドライバーは、2番目の DDI バージョンを使用して、正確なシステムクロック情報を取得します。

詳細については、「 *Intel High Definition Audio Specification*」を参照してください。

ただし、ほとんどすべてのクライアントは、HDAUDIO\_BUS\_インターフェイスバージョンの DDI を使用します。 割り込みのタイミングを正確に制御する必要がある少数のクライアントのみが、HDAUDIO\_BUS\_インターフェイス\_BDL バージョンを使用します。

 

 




