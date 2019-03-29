---
title: スキャッター/ギャザー DMA の使用
description: スキャッター/ギャザー DMA の使用
ms.assetid: dacc618f-d4d4-4c3c-a18c-baeef779e931
keywords:
- AdapterListControl ルーチン
- スキャッター/ギャザー DMA WDK I/O
- PutScatterGatherList
- GetScatterGatherList
- DMA 転送 WDK カーネルでは、DMA のスキャッター/ギャザー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b2227b4bf979e90a35375764b18eb74441337da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570668"
---
# <a name="using-scattergather-dma"></a>スキャッター/ギャザー DMA の使用





システムを実行するドライバーやバス マスター、パケットに基づく DMA では、スキャッター/ギャザー DMA 向けサポート ルーチンを使用できます。 記載されているルーチンのシーケンスを呼び出す代わりに[Using Packet-Based システム DMA](using-packet-based-system-dma.md)と[パケットに基づくバス-マスター DMA](using-packet-based-bus-master-dma.md)、ドライバーを使用できる[ **GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)と[ **PutScatterGatherList**](https://msdn.microsoft.com/library/windows/hardware/ff559967)します。

デバイスは、そのドライバーは、これらのルーチンを使用するための組み込みのスキャッター/ギャザー サポートされている必要はありません。

パケットに基づく DMA を使用するドライバーは、スキャッター/ギャザー操作のサポート ルーチンの次の一般的なシーケンスを呼び出します。

1.  [**MmGetMdlVirtualAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff554539)への呼び出しでパラメーターとして必要な MDL にインデックスを取得する**GetScatterGatherList**

2.  [**GetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff546531)ドライバーが DMA のデバイスをプログラムする準備ができておよび DMA コント ローラーのシステムまたはバス マスター アダプターが必要

    **GetScatterGatherList** DMA コント ローラーのシステムまたはバス マスター アダプターを割り当て、マップの数を決定しますレジスタが必要なおよびライセンスを割り当てます、スキャッター/ギャザーの一覧を入力し、ドライバーのを呼び出す[  *。AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)ルーチン DMA コント ローラーまたはアダプターとマップのレジスタが使用できる場合。

3.  [**PutScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff559967)直後、要求されたすべてのデータが転送されたまたはドライバーが IRP をデバイス I/O エラーのために失敗

    **PutScatterGatherList**アダプター バッファーをフラッシュ、マップのレジスタを解放し、スキャッター/ギャザーの一覧を解放します。 ドライバーを呼び出す必要があります**PutScatterGatherList**バッファー内のデータにアクセスします。

によって返されるアダプター オブジェクト ポインター **IoGetDmaAdapter**を除くこれらのルーチンのそれぞれに必要なパラメーターは、 **MmGetMdlVirtualAddress**で MDL へのポインターがありますが、 *Irp* - &gt; **MdlAddress**します。

**GetScatterGatherList**ルーチンにはへの呼び出しが含まれています**AllocateAdapterChannel**と**MapTransfer**ので、ドライバーはこれらの呼び出しを作成する必要はありません。 ルーチンは、以下をパラメーターとしてを受け取ります。

-   ポインター、 [ **DMA\_アダプター** ](https://msdn.microsoft.com/library/windows/hardware/ff544062)によって返される構造体[ **IoGetDmaAdapter**](https://msdn.microsoft.com/library/windows/hardware/ff549220)

-   DMA 操作の対象のデバイス オブジェクトへのポインター

-   MDL バッファーを記述するへのポインター *Irp*-&gt;**MdlAddress**

-   Mdl で説明されているバッファーの現在の仮想アドレスへのポインター

-   マップするバイト数

-   ポインター、 [ *AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)転送を実行するルーチン

-   渡されるコンテキストのドライバー定義領域へのポインター、 *AdapterListControl*ルーチン

-   ブール値です。**TRUE**デバイスへの転送**FALSE**それ以外の場合

必要なマップのレジスタの数を決定した後の割り当て、アダプター チャネルとマップの登録、スキャッター/ギャザーの一覧を入力し、転送を準備**GetScatterGatherList**ドライバーによって提供されるを呼び出す*AdapterListControl*ルーチン。 *AdapterListControl*ルーチンは IRQL で任意のスレッド コンテキストで実行 = ディスパッチ\_レベル。

*AdapterListControl*への呼び出しでの日常的なドライバー提供**GetScatterGatherList**とは異なります、 [ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)渡されたルーチン**AllocateAdapterChannel**以下の重要なは尊重します。

-   *AdapterListControl*ルーチンには、戻り値がありませんが、 *AdapterControl*ルーチンを返します、 [ **IO\_割り当て\_アクション**](https://msdn.microsoft.com/library/windows/hardware/ff550534).

-   ポインターではなく、 *MapRegisterBase*システムによって割り当てられたマップ レジスタ、3 番目のパラメーターについて、 *AdapterListControl*ルーチンの代わりに指す、 [ **散布図\_収集\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff563664)構造体のドライバーが DMA を実行します。

-   *AdapterListControl*ルーチンで必要なタスクのサブセットを実行する、 *AdapterControl*ルーチン。

    *AdapterListControl*ルーチンを呼び出しません**AllocateAdapterChannel**または**MapTransfer**します。 その唯一の役目は、スキャッター/ギャザーの入力リストのポインターを保存、そのデバイスを設定および DMA を実行するスキャッター/ギャザーのリストを使用します。

スキャッター/ギャザー リスト構造が含まれています、**散布図\_収集\_要素**配列と、配列内の要素の数。 配列の各要素は、長さと物理的に連続するスキャッター/ギャザー リージョンの物理アドレスの開始を提供します。 ドライバーは、データ転送で長さとアドレスを使用します。

ドライバーを使用できる**GetScatterGatherList**かどうか、デバイスはスキャッター/ギャザー DMA に関係なく。 スキャッター/ギャザーをサポートしていないデバイスの DMA、スキャッター/ギャザー一覧には、1 つだけの要素が含まれます。

スキャッター/ギャザー ルーチンを使用して呼び出し経由でパフォーマンスを向上できます**AllocateAdapterChannel** (で説明したよう[Using Packet-Based システム DMA](using-packet-based-system-dma.md)と[を使用してパケットに基づくBus-Master DMA](using-packet-based-bus-master-dma.md))。 呼び出しとは異なり**AllocateAdapterChannel**、1 つ以上の呼び出し**GetScatterGatherList**デバイス オブジェクトの任意の時点でキューに追加されます。 ドライバーを呼び出すことができます**GetScatterGatherList**する前に同じドライバー オブジェクトで別の DMA 操作用にもう一度その*AdapterListControl*ルーチンの実行が完了しました。

ドライバーによって提供されるから返された場合*AdapterListControl*ルーチン、 **GetScatterGatherList**保持マップに登録しますが、DMA アダプターの構造体を解放します。

呼び出す必要がありますが、ドライバーは IRP が現在の転送要求を満たしていますか IRP が、デバイスまたはバス I/O エラーが原因で失敗する必要があります、 **PutScatterGatherList**バッファーに転送されたデータにアクセスします。 **PutScatterGatherList**アダプター バッファーをフラッシュし、マップのレジスタとスキャッター/ギャザーの一覧を解放します。

 

 




