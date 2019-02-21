---
title: AVStream で DMA をパケットに基づく
description: AVStream で DMA をパケットに基づく
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
ms.openlocfilehash: 4c5d16f901b30cf7286fbcc69bab69845762e6f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538187"
---
# <a name="packet-based-dma-in-avstream"></a>AVStream で DMA をパケットに基づく





パケットに基づくダイレクト メモリ アクセス (DMA) は、ミニドライバーから直接データとユーザー モードから受け取るバッファーを取得するには、直接書き込みデータを読み取るときに発生します。 [AVStream シミュレートされたハードウェア ドライバーのサンプル (AVSHwS)](https://go.microsoft.com/fwlink/p/?linkid=256083) Windows Driver Kit でサンプルがこの種類の DMA を実行する AVStream ミニドライバーを作成する方法を示します。

DMA パケットに基づくスキームを実装するには。

1.  指定 KSPIN\_フラグ\_生成\_のマッピング、**フラグ**の関連するメンバー [ **KSPIN\_記述子\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造体。 このフラグはスキャッター/ギャザー サポート バス マスターによってのみ使用する必要がありますに注意してください。

2.  割り込みサービス ルーチン (ISR) の登録」の説明に従って[ハードウェア書き込み AVStream ミニドライバー](writing-avstream-minidrivers-for-hardware.md)します。

次に、 [ *AVStrMiniDeviceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff556297)ディスパッチを開始します。

1.  DMA アダプター オブジェクトを使用して、セットアップ[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)します。

2.  AVStream を呼び出すことによって、DMA アダプター オブジェクトを登録[ **KsDeviceRegisterAdapterObject**](https://msdn.microsoft.com/library/windows/hardware/ff561687)します。

提供することで、ミニドライバーが単一のスキャッター/ギャザー マッピングの最大サイズを指定する*MaxMappingByteCount*への呼び出しでパラメーター [ **KsDeviceRegisterAdapterObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561687).

AVStream が、それぞれがで指定されたサイズよりも小さいいくつかのスキャッター/ギャザー マッピングに、マッピングを自動的に分割するそのスキャッター/ギャザーのマッピングがこの最大サイズを超えている場合*MaxMappingByteCount*します。

指定することも必要があります、 [ *AVStrMiniPinProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556351)コールバック ルーチン。 ドライバー開発者は、このコールバックの適切な機能を選択する必要があります。 1 つの例として、次を実行できます。

1.  呼び出す[ **KsPinGetLeadingEdgeStreamPointer**](https://msdn.microsoft.com/library/windows/hardware/ff563513)します。

2.  リーディング エッジを呼び出すことによって複製[ **KsStreamPointerClone**](https://msdn.microsoft.com/library/windows/hardware/ff567129)します。

3.  クローンに基づいてプログラム DMA のハードウェア。

4.  呼び出す[ **KsStreamPointerAdvanceOffsets** ](https://msdn.microsoft.com/library/windows/hardware/ff567126)または[ **KsStreamPointerAdvance** ](https://msdn.microsoft.com/library/windows/hardware/ff567125)リーディング エッジを進める。

5.  手順 2. 追加のフレームの必要に応じて繰り返します。

ハードウェアの割り込みの DMA 完了、カーネルは、ベンダーに登録されている ISR を呼び出します。 ISR、ミニドライバーは遅延プロシージャ呼び出し (DPC) をキューします。

DPC を更新する必要があります**DataUsed**およびその他のメンバーの可能性があります、 [ **KSSTREAM\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff567138)構造体。 DPC は呼び出すことができますし、 [ **KsStreamPointerDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff567130)を複製を削除し、関連付けられているフレームを解放します。

またはの DPC は、フレームの部分が完了しただけの場合などに、複製ポインターを進めます。 これを行うには、呼び出す[ **KsStreamPointerAdvanceOffsets**](https://msdn.microsoft.com/library/windows/hardware/ff567126)します。

処理を再開する必要がある場合は、呼び出す[ **KsPinAttemptProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff563494)します。

マッピングが長さ未満の 1 つの物理ページの場合は、これは保証されません 1 つの物理ページ上に存在することを注意してください。

 

 




