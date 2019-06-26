---
title: 64 KB ページのサポート
description: 64 KB のページの Windows Display Driver Model (WDDM) v2 をサポートするために、2 種類のリーフ ページのテーブル、64 KB のエントリをサポートする 1 つおよび 4 KB のページ テーブル エントリをサポートしているを提供します。
ms.assetid: 24D4854E-BBD7-46A9-8FEF-EF13D2968E6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5984d481dbf71dcd5879f884b291d793be4323b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353841"
---
# <a name="support-for-64kb-pages"></a>64 KB ページのサポート


64 KB のページの Windows Display Driver Model (WDDM) v2 をサポートするために、2 種類のリーフ ページのテーブル、64 KB のエントリをサポートする 1 つおよび 4 KB のページ テーブル エントリをサポートしているを提供します。 両方のページ テーブル エントリのサイズは 4 KB のページのページ テーブルは 64 KB のページ テーブル エントリの数の 16 回、同じ仮想アドレス範囲について説明します。

64 KB のページ テーブルのサイズが定義[ **DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**LeafPageTableSizeFor64KPagesInBytes**します。

[ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作がページ テーブルの種類が更新されるかを示すフラグ[ **DXGK\_UPDATEPAGETABLEFLAGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_updatepagetableflags)::**Use64KBPages**します。

これには、WDDM v2 でサポートされている操作の 2 つのモードがあります。

1.  レベル 1 のページ テーブルのページ テーブル エントリは、4 KB のページのテーブルまたは 64 KB のページ テーブルのいずれかをポイントします。
2.  レベル 1 のページ テーブルのページ テーブル エントリは、同時に 4 KB のページ テーブルと、64 KB のページ テーブルをポイントします。 これは、"デュアル PTE"モードと呼ばれます。

*デュアル PTE*サポートがによって表される、 [ **DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**DualPteSupported**キャップ。
ビデオ メモリ マネージャーは、割り当ての配置、グラフィックス処理ユニット (GPU) のメモリのセグメント プロパティ、および GPU のメモリ セグメントの種類に基づいて、ページ サイズを選択します。 割り当ては、アラインメントとサイズが複数ある場合は、64 KB のページを使用してマップする 64 KB が 64 KB のページをサポートするメモリ セグメントに常駐します。

## <a name="span-idsingleptemodespanspan-idsingleptemodespanspan-idsingleptemodespansingle-pte-mode"></a><span id="Single_PTE_mode"></span><span id="single_pte_mode"></span><span id="SINGLE_PTE_MODE"></span>1 つの PTE モード


このモードでは、レベル 1 のページ テーブルのページ テーブル エントリは、4 KB のページ テーブルまたは 64 KB のページ テーブルのいずれかをポイントします。

[**DXGK\_PTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_dxgk_pte)::**PageTablePageSize**フィールドに追加されます**DXGK\_PTE**します。 レベル 1 のページ テーブル (古い用語では、ページ ディレクトリ) のページ テーブル エントリに対してのみ使用してください。 このフィールドは、カーネル モード ドライバー (64 KB、または 4 KB のページを使用して)、対応するページ テーブルの種類を示します。

ビデオ メモリ マネージャーが仮想アドレスの 64 KB のページ テーブルを使用した場合の範囲します。

-   64 KB に配置割り当てのみが、範囲にマップされます。
-   範囲にマップされているすべての割り当てのメモリのセグメントは、64 KB のページをサポートします。

仮想アドレスの範囲が 64 KB のページによってマップされているし、上記の条件は無効になります (たとえば、割り当てがコミットされるシステム メモリのセグメントに) と、ビデオ メモリ マネージャーが、64 KB のページ テーブルから、4 KB のページ テーブルに切り替わります。

ページのテーブルが 64 KB のページ テーブル エントリのみとページ テーブル エントリの場合、4 KB のページを指す必要があります (たとえば、割り当ては、配置しているシステム メモリに) ページのテーブルは 4 KB のページ テーブル エントリを使用してに変換されます。

変換は、次のように行われます。

1.  プロセスのすべてのコンテキストが中断されます。
2.  4 KB のページをポイントする既存のページ テーブル エントリが更新されます。 ドライバー、 [ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作をページングします。
3.  ページ テーブルをポイントするレベル 1 のページ テーブル エントリが新しいページ サイズを反映するように更新されます (**PageTablePageSize** = **DXGK\_PTE\_ページ\_テーブル\_ページ\_4 KB**)。 ドライバー、 [ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作をページングします。
4.  プロセスのすべてのコンテキストが再開されます。

ページのテーブルが唯一の 4 KB ページ テーブル エントリと、4 KB のページをポイントする必要がありますのページ テーブル エントリの数が 0、ページの表は 64 KB のページ テーブル エントリを使用する変換されます。

変換は、次のように行われます。

1.  プロセスのすべてのコンテキストが中断されます。
2.  64 KB のページをポイントする既存のページ テーブル エントリが更新されます。 ドライバー、 [ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作をページングします。
3.  ページ テーブルをポイントするレベル 1 のページ テーブル エントリが新しいページ サイズを反映するように更新されます (**PageTablePageSize** = **DXGK\_PTE\_ページ\_テーブル\_ページ\_64 KB**)。 ドライバー、 [ *UpdatePageTable* ](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作をページングします。
4.  プロセスのすべてのコンテキストが再開されます。

別のページ テーブルのサイズを頻繁に切り替えますを防ぐためには、ドライバーはまとめて小さな割り当てをパックする必要があります。

## <a name="span-iddualptemodespanspan-iddualptemodespanspan-iddualptemodespandual-pte-mode"></a><span id="Dual_PTE_mode"></span><span id="dual_pte_mode"></span><span id="DUAL_PTE_MODE"></span>デュアル モードの PTE


このモードでは、レベル 1 のページ テーブルのページ テーブル エントリは同時に 4 KB のページ テーブルを 64 KB のページ テーブルにポイント可能性があります。

レベル 1 のページ テーブルのエントリで両方のポインターがあります、**有効**フラグが設定が同じ 64 KB 仮想アドレスの範囲をカバーする、レベル 0 のページ テーブル エントリが同時に有効することはできません。

64 KB のページ テーブル エントリを対象となる割り当てがページ サイズが 64 KB のメモリ セグメントに配置されると、64 KB のページ テーブル エントリが無効になり、対応する 4 KB のページ テーブル エントリが有効になります。

次の図に 4 KB の割り当ておよび割り当てが 64 KB に配置 level0 のページ テーブルの同じ仮想アドレス範囲および 64 KB のページをサポートするセグメントをれています。

![pte デュアル モードのページ テーブル](images/support-for-64kb-pages.1.png)

 

 





