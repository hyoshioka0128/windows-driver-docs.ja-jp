---
title: GPU 仮想アドレス
description: グラフィックスプロセッシングユニット (GPU) の仮想アドレスは、デバイスドライバーインターフェイス (DDI) レベルで、論理 4 KB または 64 KB のページで管理されます。
ms.assetid: 65BD05FC-06FD-4DC2-977A-7F48E72B4858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a6d7eb382f3412cf8dfb4a3f75ecbaeb6b3a0c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838929"
---
# <a name="gpu-virtual-address"></a>GPU 仮想アドレス


グラフィックスプロセッシングユニット (GPU) の仮想アドレスは、デバイスドライバーインターフェイス (DDI) レベルで、論理 4 KB または 64 KB のページで管理されます。 これにより、GPU 仮想アドレスは、常に 4 KB 単位で割り当てられるか、または 4 kb または 64 KB で管理されるメモリセグメントページを参照できます。

ビデオメモリマネージャーは複数レベルの仮想アドレス変換スキームをサポートしており、複数のレベルのページテーブルを使用して仮想アドレスを変換します。 レベルにはゼロから番号が付けられ、レベル0はリーフレベルに割り当てられます。 変換は、ルートレベルのページテーブルから開始されます。 ページテーブルレベルの数が2の場合、可変 GPU 仮想アドレス空間のサイズを持つプロセスに合わせて、ルートページテーブルのサイズを変更できます。 すべてのレベルは、 [*DxgkDdiQueryAdapterInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_queryadapterinfo)の呼び出し中にカーネルモードドライバーによって入力される、 [**DXGK\_ページ\_テーブル\_レベル\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)構造によって記述されます。 カーネルモードドライバーは、GPU 仮想アドレスのサポートについて説明するために、 [**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps) caps 構造体にも入力します。

各プロセスには、独自の GPU 仮想アドレス空間があります。 プロセスのグラフィックスコンテキストを実行のために設定する前に、カーネルモードドライバーは、ルートページのテーブルアドレスを設定する[*DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)呼び出しを取得します。

2つのページテーブルレベルの場合の仮想アドレス変換を次の図に示します。

![2つのページテーブルレベルの場合、仮想アドレス変換が表示されます。](images/gpu-virtual-address.1.png)

GPU 仮想アドレスには、 [**DXGK\_GPUMMUCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_gpummucaps)::**Virtualaddressbitcount**ビットが含まれています。

下位ビット \[0-11\]、ページ内のオフセット (バイト単位) を表します。 次の[**DXGK\_ページ\_テーブル\_レベル\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**Pagetableindexbitcount**ビットは、リーフレベルのページテーブル内のページテーブルエントリのインデックスを表します。

ページテーブル内のエントリの数は、2つの<sup>DXGK\_ページ\_テーブル\_レベル\_DESC::P ageTableIndexBitCount</sup>とページテーブルサイズが[**DXGK\_page\_table\_LEVEL\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableSizeInBytes** bytes。

残りのビットは、ルートページテーブル内のページテーブルエントリのインデックスを表します。 ルートページテーブルは、2レベルの翻訳スキーム用にサイズ変更でき、そのサイズを取得するために新しい[*DxgkDdiGetRootPageTableSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI が導入されています。

[**DXGK\_PTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_dxgk_pte)構造体は、DDI を通じてページテーブルエントリを表すために使用されます。 この構造体は、Microsoft DirectX グラフィックスカーネルが管理する各エントリに関する情報を表します。 ドライバーは、この情報を使用して、ハードウェア固有のページテーブルエントリを作成します。

## <a name="span-idcreation_of_page_table_allocationsspanspan-idcreation_of_page_table_allocationsspanspan-idcreation_of_page_table_allocationsspancreation-of-page-table-allocations"></a><span id="Creation_of_page_table_allocations"></span><span id="creation_of_page_table_allocations"></span><span id="CREATION_OF_PAGE_TABLE_ALLOCATIONS"></span>ページテーブル割り当ての作成


ページテーブルは、暗黙的な割り当てとして作成され、ユーザーモードドライバーまたはカーネルモードドライバーハンドルを持っていません。

ページテーブルを割り当てるには、ビデオメモリマネージャーによって、サイズ[**DXGK\_ページ\_テーブル\_レベル\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)::**PageTableSizeInBytes**の割り当てが**DXGK\_ページで指定したセグメントから割り当てられ\_テーブル\_レベル\_DESC**::**PageTableSegmentId**。 作成後、ビデオメモリマネージャーは、新しい[*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を使用して、ページテーブル内のすべてのエントリを*無効*に初期化します。 2レベル翻訳スキームのルートページテーブルを除いて、ページテーブルのサイズは変更されません。

ビデオメモリマネージャーでは、2レベル翻訳スキームでのルートページテーブルのサイズ変更がサポートされています。 指定された量のアドレス空間をカバーするルートページテーブルを作成する場合、ビデオメモリマネージャーは新しい[*DxgkDdiGetRootPageTableSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)DDI を呼び出して、必要な割り当てサイズを決定します。 次に、ビデオメモリマネージャーは、 [**DXGK\_ページ\_テーブル\_\_レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_page_table_level_desc)で指定されたセグメントにそのサイズの割り当てを割り当てます。ルートレベルの場合は DESC::**PageTableSegmentId**です。 作成後、ビデオメモリマネージャーは、新しい[*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング操作を使用して、ページテーブル内のすべてのエントリを無効に初期化します。 プロセスで必要とされるビデオアドレス空間のサイズを拡大または縮小することで、ルートページテーブルを拡大または縮小できます。 ルートページテーブルが作成されると、ビデオメモリマネージャーは新しい[*DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI を呼び出して、新しく作成されたルートページテーブルを内で実行されるさまざまなコンテキストに関連付けます。

リンクされたディスプレイアダプターの構成では、ルートページテーブルは*Linkmirrored*割り当てとして作成されます。これは、同じコンテンツを持ち、リンク内の各 GPU の同じ物理アドレスに配置されます。 下位レベルのページテーブルは*linkinstanced*割り当てとして割り当てられ、コンテンツが GPU 間で異なる可能性があるという事実が反映されます。これは通常、ピアマッピングが異なるためです。 ページテーブルの内容は、すべての Gpu で個別に更新されます。

## <a name="span-idgrowing_and_shrinking_a_root_page_tablespanspan-idgrowing_and_shrinking_a_root_page_tablespanspan-idgrowing_and_shrinking_a_root_page_tablespangrowing-and-shrinking-a-root-page-table"></a><span id="Growing_and_shrinking_a_root_page_table"></span><span id="growing_and_shrinking_a_root_page_table"></span><span id="GROWING_AND_SHRINKING_A_ROOT_PAGE_TABLE"></span>ルートページテーブルの拡大と縮小


このセクションは、2つのレベルのページテーブルがあるシステムにのみ適用されます。 ページテーブルレベルの数が2より大きい場合、各レベルのページテーブルのサイズは仮想アドレス指定キャップによって定義され、固定されます。

ユーザーモードドライバーが GPU 仮想アドレスを要求すると、ビデオメモリマネージャーは、要求に対応するためにプロセスのアドレス空間のサイズを拡大します。 これを実現するには、現在のルートページテーブルのサイズを (必要に応じて) 拡大し、新しいページテーブルを新しい範囲に割り当てます。

ルートページテーブルを拡大するには、ビデオメモリマネージャーが別のルートページテーブル割り当てを作成し、それを常駐させて、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)操作を使用してエントリを初期化し、古い割り当てを破棄します。 [*DxgkDdiGetRootPageTableSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_getrootpagetablesize)関数は、新しいページテーブルのサイズをバイト単位で取得するために使用されます。

ルートページテーブルを圧縮するには、ビデオメモリマネージャーが新しいページテーブル割り当てを作成し、それを常駐させて、 *Copyrootpagetable*ページング操作を使用して古いページテーブルの一部を新しいテーブルにコピーし、古い割り当てを破棄します。

サイズ変更操作が完了すると、ビデオメモリマネージャーは[*DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI を呼び出して、影響を受けたコンテキストを新しいルートページテーブルに関連付けます。

## <a name="span-idupdating_page_tablespanspan-idupdating_page_tablespanspan-idupdating_page_tablespanupdating-page-table"></a><span id="Updating_page_table"></span><span id="updating_page_table"></span><span id="UPDATING_PAGE_TABLE"></span>ページテーブルを更新しています


サーフェイスがメモリ内を移動すると、ビデオメモリマネージャーは、新しいサーフェイスの場所を反映するようにページテーブルの内容を更新します。 これは、新しい[*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)ページング DDIs を使用して行います。

## <a name="span-idmoving_a_page_tablespanspan-idmoving_a_page_tablespanspan-idmoving_a_page_tablespanmoving-a-page-table"></a><span id="Moving_a_page_table"></span><span id="moving_a_page_table"></span><span id="MOVING_A_PAGE_TABLE"></span>ページテーブルの移動


ページテーブルは、デバイスがアイドル状態または中断状態のときに、ビデオメモリマネージャーによって再配置または削除されることがあります。 ページテーブルを移動すると、ビデオメモリマネージャーは、 [*Updatepagetable*](https://docs.microsoft.com/windows-hardware/drivers/display/dxgkddiupdatepagetable)DDIs を使用して、ページテーブルの新しい場所を参照するように上位レベルのページテーブルを更新します。

ルートページのテーブル自体が再配置されると、ビデオメモリマネージャーは[*DxgkDdiSetRootPageTable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_setrootpagetable)DDI を呼び出して、ページディレクトリの新しい場所の影響を受けるコンテキストを通知します。

## <a name="span-idphysical_page_sizespanspan-idphysical_page_sizespanspan-idphysical_page_sizespanphysical-page-size"></a><span id="Physical_page_size"></span><span id="physical_page_size"></span><span id="PHYSICAL_PAGE_SIZE"></span>物理ページサイズ


前述のように、ビデオメモリマネージャーは2ページのサイズをサポートしています。 システムメモリは常に 4 KB のページで管理されますが、メモリセグメントは、カーネルモードドライバーによって決定される 4 kb または 64 KB の粒度で管理できます。

64 KB のページで仮想メモリを管理するように設定すると、すべての割り当てが自動的にアラインされ、64 KB の倍数になるようにサイズが調整されます。

すべての割り当てを 64 KB に拡張すると、メモリに大きな影響を与える可能性があります。 メモリを無駄にするのを避けるために、小さい割り当てをより大きなものにパックするユーザーモードドライバーの役割です。

GPU 仮想アドレスを大きな 64 KB メモリセグメントページにマップすると、ビデオメモリマネージャーによって 4 KB のページテーブルエントリがメモリセグメントの16個の連続する 4 KB ページにマップされます。 仮想アドレスと物理アドレスの両方が、同じ 64 KB のアラインメントを共有することが保証されます (つまり、仮想アドレスの下位16ビットと物理アドレスが一致することが保証されます)。

 

 





