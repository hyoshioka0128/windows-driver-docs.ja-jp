---
title: AVStream のパケットベースの DMA
description: AVStream のパケットベースの DMA
ms.assetid: 4246819e-d8d6-4302-9477-675ca181b1e3
keywords:
- AVStream WDK、ハードウェア
- ハードウェア WDK AVStream
- DMA は、WDK AVStream をサービスします。
- ダイレクト メモリ アクセスの WDK AVStream
- DMA WDK AVStream のパケットに基づく
- DMA WDK AVStream のスキャッター/ギャザー
- WDK AVStream のバッファーをキャプチャします。
- WDK AVStream のバッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35938834d7122f955de864be1e0ad0a676cc4796
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370389"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream のパケットベースの DMA





パケットに基づくダイレクト メモリ アクセス (DMA) は、ミニドライバーから直接データとユーザー モードから受け取るバッファーを取得するには、直接書き込みデータを読み取るときに発生します。 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows Driver Kit でサンプルがこの種類の DMA を実行する AVStream ミニドライバーを作成する方法を示します。

DMA パケットに基づくスキームを実装するには。

1.  指定 KSPIN\_フラグ\_生成\_のマッピング、**フラグ**の関連するメンバー [ **KSPIN\_記述子\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)構造体。 このフラグはスキャッター/ギャザー サポート バス マスターによってのみ使用する必要がありますに注意してください。

2.  割り込みサービス ルーチン (ISR) の登録」の説明に従って[ハードウェア書き込み AVStream ミニドライバー](writing-avstream-minidrivers-for-hardware.md)します。

次に、 [ *AVStrMiniDeviceStart* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnksdevicepnpstart)ディスパッチを開始します。

1.  DMA アダプター オブジェクトを使用して、セットアップ[ **IoGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdmaadapter)します。

2.  AVStream を呼び出すことによって、DMA アダプター オブジェクトを登録[ **KsDeviceRegisterAdapterObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdeviceregisteradapterobject)します。

提供することで、ミニドライバーが単一のスキャッター/ギャザー マッピングの最大サイズを指定する*MaxMappingByteCount*への呼び出しでパラメーター [ **KsDeviceRegisterAdapterObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdeviceregisteradapterobject).

AVStream が、それぞれがで指定されたサイズよりも小さいいくつかのスキャッター/ギャザー マッピングに、マッピングを自動的に分割するそのスキャッター/ギャザーのマッピングがこの最大サイズを超えている場合*MaxMappingByteCount*します。

指定することも必要があります、 [ *AVStrMiniPinProcess* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nc-ks-pfnkspin)コールバック ルーチン。 ドライバー開発者は、このコールバックの適切な機能を選択する必要があります。 1 つの例として、次を実行できます。

1.  呼び出す[ **KsPinGetLeadingEdgeStreamPointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspingetleadingedgestreampointer)します。

2.  リーディング エッジを呼び出すことによって複製[ **KsStreamPointerClone**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerclone)します。

3.  クローンに基づいてプログラム DMA のハードウェア。

4.  呼び出す[ **KsStreamPointerAdvanceOffsets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)または[ **KsStreamPointerAdvance** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvance)リーディング エッジを進める。

5.  手順 2. 追加のフレームの必要に応じて繰り返します。

ハードウェアの割り込みの DMA 完了、カーネルは、ベンダーに登録されている ISR を呼び出します。 ISR、ミニドライバーは遅延プロシージャ呼び出し (DPC) をキューします。

DPC を更新する必要があります**DataUsed**およびその他のメンバーの可能性があります、 [ **KSSTREAM\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)構造体。 DPC は呼び出すことができますし、 [ **KsStreamPointerDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointerdelete)を複製を削除し、関連付けられているフレームを解放します。

またはの DPC は、フレームの部分が完了しただけの場合などに、複製ポインターを進めます。 これを行うには、呼び出す[ **KsStreamPointerAdvanceOffsets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksstreampointeradvanceoffsets)します。

処理を再開する必要がある場合は、呼び出す[ **KsPinAttemptProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kspinattemptprocessing)します。

マッピングが長さ未満の 1 つの物理ページの場合は、これは保証されません 1 つの物理ページ上に存在することを注意してください。

 

 




