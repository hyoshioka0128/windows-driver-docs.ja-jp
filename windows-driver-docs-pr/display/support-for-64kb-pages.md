---
title: 64 KB ページのサポート
description: 64 KB のページをサポートするために、Windows Display Driver Model (WDDM) v2 は2種類のリーフページテーブルを提供しています。1つは 4 KB のページテーブルエントリをサポートし、もう1つは 64 KB エントリをサポートします。
ms.assetid: 24D4854E-BBD7-46A9-8FEF-EF13D2968E6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe3a4e9c2406b3e7cd722bb22cf4ebbb2f973172
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829396"
---
# <a name="support-for-64kb-pages"></a>64 KB ページのサポート


64 KB のページをサポートするために、Windows Display Driver Model (WDDM) v2 は2種類のリーフページテーブルを提供しています。1つは 4 KB のページテーブルエントリをサポートし、もう1つは 64 KB エントリをサポートします。 どちらのページテーブルエントリのサイズも同じ仮想アドレス範囲をカバーするため、4 kb のページのページテーブルには、64 KB ページテーブルとしてエントリの数が16倍になります。

64 KB ページテーブルのサイズは、 [**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**LeafPageTableSizeFor64KPagesInBytes**によって定義されます。

[*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作には、ページテーブルが更新されたことを示すフラグ ( [**DXGK\_UPDATEPAGETABLEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_updatepagetableflags)::**Use64KBPages**) があります。

WDDM v2 でサポートされている操作には、次の2つのモードがあります。

1.  レベル1のページテーブルのページテーブルエントリは、4 KB ページテーブルまたは 64 KB ページテーブルのいずれかになります。
2.  レベル1のページテーブルのページテーブルエントリは、4 KB のページテーブルと 64 KB のページテーブルを指します。 これは、"デュアル PTE" モードと呼ばれます。

*2 つの PTE*のサポートは、 [**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**DualPteSupported** cap によって表されます。
ビデオメモリマネージャーは、割り当ての配置、グラフィックス処理ユニット (GPU) のメモリセグメントのプロパティ、および GPU のメモリセグメントの種類に基づいてページサイズを選択します。 アロケーションは 64 KB のページを使用してマップされ、サイズは 64 KB の倍数で、64 KB ページをサポートするメモリセグメントに常駐します。

## <a name="span-idsingle_pte_modespanspan-idsingle_pte_modespanspan-idsingle_pte_modespansingle-pte-mode"></a><span id="Single_PTE_mode"></span><span id="single_pte_mode"></span><span id="SINGLE_PTE_MODE"></span>単一の PTE モード


このモードでは、レベル1のページテーブルのページテーブルエントリは、4 KB のページテーブルまたは 64 KB のページテーブルのいずれかになります。

[**DXGK\_pte**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_dxgk_pte)::**pagetablepagesize**フィールドが**DXGK\_pte**に追加されます。 これは、レベル1のページテーブル (古い用語のページディレクトリ) のページテーブルエントリに対してのみ使用してください。 このフィールドは、対応するページテーブルの種類をカーネルモードドライバーに指示します (64 KB または 4 KB のページを使用します)。

ビデオメモリマネージャーは、次の場合に、仮想アドレスの範囲に 64 KB のページテーブルを使用することを選択します。

-   64 KB のアラインされた割り当てのみが範囲にマップされます。
-   範囲にマップされているすべての割り当てのメモリセグメントは、64 KB のページをサポートします。

仮想アドレス範囲が 64 KB ページによってマップされていて、上記の条件が有効ではない場合 (たとえば、割り当てがシステムメモリセグメントにコミットされた場合)、ビデオメモリマネージャーは 64 KB ページテーブルから 4 KB ページテーブルに切り替えます。

ページテーブルに 64 KB のページテーブルエントリが1つだけあり、ページテーブルエントリが 4 kb のページをポイントする必要がある場合 (たとえば、割り当てがシステムメモリに配置されている場合)、ページテーブルは 4 KB のページテーブルエントリを使用するように変換されます。

変換は次のように行われます。

1.  プロセスのすべてのコンテキストが中断されています。
2.  既存のページテーブルエントリは、4 KB のページを指すように更新されます。 ドライバーは、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を取得します。
3.  ページテーブルを指すレベル1のページテーブルエントリが更新され、新しいページサイズ (**Pagetablepagesize** = **DXGK\_PTE\_ページ\_テーブル\_ページ\_4 kb**) が反映されます。 ドライバーは、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を取得します。
4.  プロセスのすべてのコンテキストが再開されます。

ページテーブルに 4 kb のページテーブルエントリしかなく、4 kb のページを指す必要があるページテーブルエントリの数が0の場合、ページテーブルは 64 KB のページテーブルエントリを使用するように変換されます。

変換は次のように行われます。

1.  プロセスのすべてのコンテキストが中断されています。
2.  既存のページテーブルエントリは、64 KB のページを指すように更新されます。 ドライバーは、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を取得します。
3.  ページテーブルをポイントするレベル1のページテーブルエントリが更新され、新しいページサイズ (**Pagetablepagesize** = **DXGK\_PTE\_ページ\_テーブル\_ページ\_64 kb**) が反映されます。 ドライバーは、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を取得します。
4.  プロセスのすべてのコンテキストが再開されます。

異なるページテーブルサイズが頻繁に切り替わるのを防ぐために、ドライバーは小さい割り当てをまとめてパックする必要があります。

## <a name="span-iddual_pte_modespanspan-iddual_pte_modespanspan-iddual_pte_modespandual-pte-mode"></a><span id="Dual_PTE_mode"></span><span id="dual_pte_mode"></span><span id="DUAL_PTE_MODE"></span>デュアル PTE モード


このモードでは、レベル1のページテーブルのページテーブルエントリは、4 KB のページテーブルと 64 KB のページテーブルを指している場合があります。

レベル1のページテーブルのエントリ内の両方のポインターに**有効な**フラグが設定されている可能性がありますが、同じ 64 KB の仮想アドレス範囲をカバーするレベル0のページテーブルのエントリは、同時に有効にすることができません。

64 KB のページテーブルエントリによってカバーされる割り当てが、64 KB ページサイズのメモリセグメントに配置されると、64 KB ページテーブルエントリが無効になり、対応する 4 KB のページテーブルエントリが有効になります。

次の図では、4 KB の割り当てと 64 KB でアラインされた割り当てが、level0 page テーブルと 64 KB ページをサポートするセグメントでカバーされる同じ仮想アドレス範囲内にあります。

![デュアル pte モードのページテーブル](images/support-for-64kb-pages.1.png)

 

 





