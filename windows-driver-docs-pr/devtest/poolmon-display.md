---
title: PoolMon の表示
description: PoolMon の表示
ms.assetid: 1dee4331-a508-4e7f-b621-4d22f6572aec
keywords:
- PoolMon の WDK を表示します
- メモリ プール モニタの WDK を表示します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de486ea2c5533242c67d882b2148702c0af2f9fc
ms.sourcegitcommit: bb482ef6935e171674c6a99bb499668c0f62ca24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66051639"
---
# <a name="poolmon-display"></a>PoolMon の表示

PoolMon は、コマンド ウィンドウで、プールのメモリ割り当てに関するデータの列を表示します。 方向キー、PAGEUP、PAGEDOWN キーを使用して、データをスクロールします。

>[!NOTE]
>PoolMon 表示全体を表示するには、コマンド プロンプト ウィンドウのサイズが 80 以上の文字幅をある必要があります (幅 = 80)、少なくとも 53 行の高さ (高さ = 53)。コマンド プロンプト ウィンドウのバッファーが 500 以上の文字幅をする必要があります (幅 = 500)、少なくとも 2000 行の高さ (高さ = 2000)。 それ以外の場合、表示は切り捨てられます。

次の表では、PoolMon 表示内の列について説明します。

|列名|説明|
|----|----|
|**タグ**|プールの割り当てに割り当てられた 4 バイトのタグ。|
|**型**|かどうか、メモリの割り当ては、ページまたは非ページ バイトには。|
|**回数**|割り当ての数。|
|**( )**|前回の更新以降の割り当ての数に変更します。|
|**解放**|無料の操作の数。|
|**( )**|前回の更新以降の割り当ての数に変更します。|
|**相違点**|無料の操作の数-割り当ての数。|
|**バイト数**|使用されるバイトの割り当てのサイズ。|
|**( )**|前回の更新以降の割り当てサイズの変更。|
|**Alloc ごと**|相違の値を除算してバイト単位の値|
|**Mapped_Driver**|ローカルのドライバー (**/c**) ドライバーとシステム コンポーネント頻繁に使用し、(**/g**) プール タグの値を割り当てることです。 この列は、使用する場合のみ表示されます、 **/c**または **/g**パラメーター。|

次のサンプル PoolMon 出力は、割り当ての数によって並べ替えられます。 (このように、ディスプレイを並べ替え、開始と PoolMon、 **/a**パラメーターです)。

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

## <a name="update-rate"></a>更新間隔

PoolMon では、5 秒ごとの表示を更新します。 更新間隔をプログラムで変更することはできません。 ただし、強制的に更新する PoolMon 結果の一部のキーをクリックして PoolMon がで実行されているウィンドウにフォーカスがある場合。 **Ctrl キーを押し**と**ALT**、たとえば、強制的に更新。 ただし、 **Print screen**はありません。

## <a name="accumulated-values"></a>累積値

PoolMon を表示するデータが収集され、プールのタグ付けを有効にするたびに、Windows によって計算されます。 割り当て、解放操作は、使用されているバイトの値は、Windows が起動された時間から蓄積し、Windows が再起動されるまで 1 ずつ増加します。 Windows が既に開始後に、ドライバーまたはコンポーネントが開始されると場合、は、値が前回開始し、リセット、ドライバーまたはシステムを再起動したときにのみ、ドライバーまたはコンポーネントの蓄積されます。

## <a name="interpreting-tag-values"></a>タグの値を解釈します。

プールのすべてのメモリ割り当ては、タグがすべてが特徴的なタグの値。 プールのメモリ割り当てが、メモリの割り当て、ドライバーを使用して、タグの値を設定するときに、特性のタグの値を持つ[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)または[ **ExAllocatePoolWithQuotaTag**](https://msdn.microsoft.com/library/windows/hardware/ff544513)します。 ドライバーをタグの値を割り当てない場合 ([**ExAllocatePool**](https://msdn.microsoft.com/library/windows/hardware/ff544501)、 [ **ExAllocatePoolWithQuota**](https://msdn.microsoft.com/library/windows/hardware/ff544506))、Windows がまだですが、タグを作成します[なし] の既定のタグ値を割り当てます。 その結果、他のプール割り当てのドライバーの割り当ての統計情報を区別できません。
