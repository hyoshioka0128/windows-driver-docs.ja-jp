---
title: PoolMon の表示
description: PoolMon の表示
ms.assetid: 1dee4331-a508-4e7f-b621-4d22f6572aec
keywords:
- PoolMon WDK、表示
- メモリプールモニタ WDK、表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1b60378d1da67dad206c0cf7196d89fdcc0a083
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840052"
---
# <a name="poolmon-display"></a>PoolMon の表示

[PoolMon] コマンドウィンドウでのプールメモリの割り当てに関するデータの列が表示されます。 方向キー、pageup キー、および PAGEDOWN キーを使用して、データをスクロールします。

>[!NOTE]
>PoolMon の表示全体を表示するには、コマンドプロンプトウィンドウのサイズが80文字以上で、少なくとも53行以上 (高さ = 53) である必要があります。また、コマンドプロンプトウィンドウバッファーは、500文字以上で、少なくとも2000行 (高さ = 2000) 以上である必要があります。 それ以外の場合は、表示が切り捨てられる可能性があります。

次の表では、PoolMon 表示の列について説明します。

|列名|説明|
|----|----|
|**Tag**|プール割り当てに割り当てられた4バイトのタグ。|
|**型**|メモリ割り当てがページングされているかどうか、またはページングされていないバイトかどうか。|
|**Allocs**|割り当ての数。|
|**( )**|前回の更新以降に行われた割り当ての数の変更。|
|**費やす**|無料操作の数。|
|**( )**|前回の更新以降に行われた割り当ての数の変更。|
|**差異**|割り当ての数から、無料操作の数を差し引いた値。|
|**メモリ**|割り当てのサイズ (バイト単位)。|
|**( )**|前回の更新以降の割り当てサイズの変更。|
|**割り当てごと**|Diff の値で除算されたバイトの値。|
|**Mapped_Driver**|ローカルドライバー ( **/c**) およびその他の一般的に使用されるドライバーとシステムコンポーネント ( **/g**) で、プールタグの値を割り当てます。 この列は、 **/c**または **/g**パラメーターを使用した場合にのみ表示されます。|

次の例の PoolMon 出力は、割り当ての数によって並べ替えられています。 (この方法で表示を並べ替えるには、 **/a**パラメーターを使用して PoolMon を開始します。)

```command
 Memory:  260620K Avail:   96364K  PageFlts:     0   InRam Krnl: 1916K P:17856K
 Commit: 203500K Limit: 640916K Peak: 260632K            Pool N: 8332K P:27220K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Wait Nonp    3971107 (   0)   3971077 (   0)       30    8456 (     0)    281
 ObSt Nonp    2791258 (   0)   2791258 (   0)        0       0 (     0)      0
 Gxlt Paged   1161638 (   0)   1161630 (   0)        8     864 (     0)    108
 Ustm Paged   1088342 (   0)   1088298 (   0)       44    2464 (     0)     56
 Io   Nonp    1021112 (   1)   1020985 (   1)      127   91912 (     0)    723
 ObSq Paged    967615 (   0)    967615 (   0)        0       0 (     0)      0
 Key  Paged    954821 (   0)    953979 (   0)      842   87528 (     0)    103
 SePa Nonp     680348 (   0)    680321 (   0)       27    3656 (     0)    135
```

## <a name="update-rate"></a>更新率

PoolMon は、5秒ごとにディスプレイを更新します。 更新頻度をプログラムで変更することはできません。 ただし、ウィンドウ PoolMon がフォーカスされている場合は、一部のキーをクリックして、PoolMon の結果を強制的に更新できます。 たとえば、 **CTRL キー**と ALT キーを**押す**と、更新が強制されます。ただし、**印刷画面は表示**されません。

## <a name="accumulated-values"></a>累積値

PoolMon によって表示されるデータは、プールのタグ付けが有効になっているたびに Windows によって収集され、計算されます。 割り当て、解放操作、および使用されたバイトの値は、Windows が起動した時点から累積し、Windows が再起動されるまで単調に増加します。 Windows が既に起動した後にドライバーまたはコンポーネントを起動した場合、値はドライバーまたはコンポーネントが最後に起動したときから累積され、ドライバーまたはシステムが再起動されたときにのみリセットされます。

## <a name="interpreting-tag-values"></a>タグ値の解釈

すべてのプールメモリ割り当てにはタグがありますが、すべての特性タグ値を持つわけではありません。 プールメモリ割り当ては、メモリを割り当てるドライバーが[**exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)または[**Exallocatepoolwithquotatag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquotatag)を使用してタグ値を設定するときに、特性タグ値を持ちます。 ドライバーがタグ値 ([**exallocatepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)、 [**exallocatepoolwithquota**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithquota)) を割り当てない場合でも、Windows は引き続きタグを作成しますが、既定のタグ値は None に割り当てられます。 そのため、そのドライバーの割り当ての統計情報を、他のプール割り当ての統計と区別することはできません。
