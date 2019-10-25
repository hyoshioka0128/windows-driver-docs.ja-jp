---
title: MapTransferEx ルーチンの使用
description: MapTransferEx ルーチンは、以前に割り当てられた DMA リソースのセットを初期化し、DMA 転送を開始します。
ms.assetid: 79D3DDB2-B134-43B2-A6CC-94035C793047
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9ded07867af93b12bbb052c69999bb1a76760c92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835848"
---
# <a name="using-the-maptransferex-routine"></a>MapTransferEx ルーチンの使用


[**Maptransferex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer_ex)ルーチンは、以前に割り当てられた dma リソースのセットを初期化し、dma 転送を開始します。 このルーチンは、DMA 操作インターフェイスのバージョン3で使用できます。 このインターフェイスのバージョン3は、Windows 8 以降でサポートされています。 DMA 操作インターフェイスの詳細については、「 [**dma\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)」を参照してください。

## <a name="comparison-of-maptransferex-to-maptransfer"></a>MapTransferEx と MapTransfer の比較


**Maptransferex**は、 [**maptransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pmap_transfer)ルーチンの改善されたバージョンです。 **Maptransfer**は、Windows 2000 のバージョン1以降で、DMA 操作インターフェイスのすべてのバージョンで使用できます。 **Maptransfer**を1回呼び出すと、1つの物理メモリブロックを MDL からマップできます。 ただし、複雑な DMA 転送のデータバッファーは、MDL チェーンによって記述される場合があります。また、チェーン内の各 MDL は、物理的に連続したメモリのいくつかのブロックを記述する場合があります。 **Maptransfer**を使用してこのようなバッファーを転送するには、ドライバーが**maptransfer**を多数呼び出す必要があります。 通常、これらの呼び出しは、入れ子になったループのペア内で行われます。 内側のループは、連続する物理メモリの1つのブロックから各 MDL の次のブロックに反復処理を行い、外側のループは、1つの MDL から MDL チェーン内の次のものへと反復処理を行います。

これに対し、 **Maptransferex**の1回の呼び出しでは、複雑な DMA 転送のデータバッファー全体を転送できます。 次の3つの**Maptransferex**パラメーターは、転送に使用するバッファーメモリを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Mdl</em></td>
<td><p>1つ以上の MDLs のチェーン内の最初の MDL へのポインター。 MDL チェーンの詳細については、「 <a href="using-mdls.md" data-raw-source="[Using MDLs](using-mdls.md)">MDLs の使用</a>」を参照してください。</p></td>
</tr>
<tr class="even">
<td><em>影</em></td>
<td><p>MDL チェーンによって記述されるメモリの先頭からのバッファーのバイトオフセット。</p></td>
</tr>
<tr class="odd">
<td><em>長さ</em></td>
<td><p>データバッファーの長さ (バイト単位) を格納している場所へのポインター。</p></td>
</tr>
</tbody>
</table>

 

**Maptransferex**呼び出しの開始時に、 **maptransferex**ルーチンは、MDL チェーンを進めてバッファーの開始を検出します。 バッファーの先頭は、 *Offset*パラメーターによって指定されます。 次に、バッファーの先頭から末尾までの作業で、 **Maptransferex**はスキャッター/ギャザーリストを構築します。このリストには、リスト内の各バッファーフラグメントが、MDL チェーンの物理的に連続したメモリブロックとして含まれています。 このリストを構築するには、1つの物理的に連続したメモリブロックから各 MDL 内の次のメモリブロック**にステップインし、1**つの MDL から mdl チェーン内の次の場所にステップインします。 リスト構築は、スキャッター/ギャザーリストによって記述されるバッファーメモリの合計量が、\**Length*入力パラメーターで指定されたバイト数と等しい場合に終了します。 結果として得られるスキャッター/ギャザーリスト内のバッファーフラグメントの順序は、MDL チェーン内の物理的に連続するブロックの順序と一致します。

## <a name="multiple-calls-to-maptransferex"></a>MapTransferEx への複数の呼び出し


**Maptransferex**は、常に DMA データバッファー全体を1回の呼び出しで転送できない場合があります。 次の一覧では、転送を完了するために**Maptransferex**が2回以上呼び出される必要がある状況について説明します。

-   DMA アダプターにはマップレジスタが必要であり、アダプターに割り当てられているマップレジスタの数がバッファー全体を記述するのに十分ではありません。
-   スキャッター/ギャザーリストを格納するためにドライバーによって割り当てられたストレージは、バッファー全体のスキャッター/ギャザーリストを格納するのに十分な大きさではありません。
-   転送では、ハードウェアのスキャッター/ギャザーリストで指定できるバッファーフラグメントの数を制限するシステム DMA コントローラーを使用します。

これらすべての場合、 **Maptransferex**は、1回の呼び出しで可能な限り多くのデータバッファーをマップし、呼び出しによってどの程度のバッファーがマップされたかをドライバーに通知します。 前の一覧には、転送を完了するために**Maptransferex**への複数の呼び出しを必要とする可能性がある、プラットフォーム固有のキャッシュ動作などの他の条件は含まれていません。 将来のハードウェアプラットフォームでは、DMA 転送の長さに追加の制約が課される場合があります。 このような理由から、ドライバー開発者は、 **Maptransferex**が1回の呼び出しで DMA データバッファー全体をマップできないケースを正しく処理するようにドライバーを設計する必要があります。

**Maptransferex**を呼び出す前に、呼び出し元は、\*の*長さ*のパラメーターを、割り当てられる必要がある DMA データバッファー内のバイト数に設定します。 を返す前に、 **Maptransferex**は、呼び出しによって実際にマップされたバッファー内のバイト数に \*の*長さ*を設定します。 **Maptransferex**呼び出しで、\**長さ*の入力値によって指定されたバッファー長全体をマップできない場合、\*の*長さ*の出力値は入力値よりも小さくなります。 DMA 転送に2つ以上の**Maptransferex**呼び出しが必要な場合、呼び出し元のドライバーは、次の呼び出しに対して \**長さ*の入力値を指定する前に、1回の呼び出しから \**長さ*の出力値を取得する必要があります。

たとえば、 **Maptransferex**呼び出しで、 *Offset* = B および \**length* = N (入力時) のバッファーとの間で X バイトのみを転送できる場合、戻り値では \**length* = X になります。次に**Maptransferex**を呼び出す場合、ドライバーは*Offset* = B + X および \**Length* = N-x に設定する必要があります。どちらの呼び出しでも、同じ MDL チェーンが変更なしで使用されます。

呼び出し元が[*Dmacompletionroutine*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-dma_completion_routine)を指定する場合、 **Maptransferex**は、 *dmacomの*実行をスケジュールする前に、\**長さ*の出力値を書き込みます。 この動作により、更新された \**長さ*の値が常に使用可能になり、 *dmacomの tiontionルーチン*が実行されるようになります。 たとえば、DMA 転送に2つの**Maptransferex**呼び出しが必要な場合、最初の呼び出しスケジュールである*dmacomの tiontionルーチン*は、最初の呼び出しから \**長さ*の出力値を取得できます。 ルーチンは、この値を使用して、2回目の呼び出しの \**長さ*の入力値を計算できます。 通常、*長さ*パラメーターは、パラメーターとして*dmacomの tionルーチン*に渡さ*れる \*の*完了値内の場所を指します。

 

 




