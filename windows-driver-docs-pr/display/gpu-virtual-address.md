---
title: GPU の仮想アドレス
description: グラフィックス プロセッシング ユニット (GPU) の仮想アドレスは、デバイス ドライバー インターフェイス (DDI) レベルで 4 KB (64 kb) の論理ページで管理されます。
ms.assetid: 65BD05FC-06FD-4DC2-977A-7F48E72B4858
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e710b677e222d1b93f7b57c3714e8b81c420c4fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561111"
---
# <a name="gpu-virtual-address"></a>GPU の仮想アドレス


グラフィックス プロセッシング ユニット (GPU) の仮想アドレスは、デバイス ドライバー インターフェイス (DDI) レベルで 4 KB (64 kb) の論理ページで管理されます。 これにより、システム メモリ、4 KB の粒度で常に割り当てられた、または管理できるは 4 KB (64 kb) のいずれかでメモリ セグメントのページを参照する GPU の仮想アドレス。

ビデオ メモリ マネージャーは、仮想アドレスに変換するいくつかのレベルのページ テーブルが使用されている、複数レベルの仮想アドレス変換スキームをサポートします。 レベルの番号が 0 から、レベル 0 は、リーフ レベルに割り当てられます。 翻訳は、ルート レベルのページ テーブルから開始します。 テーブル レベルのページ数が 2 つの場合は、ルート ページのテーブルの変数 GPU 仮想アドレス領域のサイズを持つプロセスを対応するためにサイズ変更できます。 すべてのレベルは、 [ **DXGK\_ページ\_テーブル\_レベル\_DESC** ](https://msdn.microsoft.com/library/windows/hardware/dn906832) 中ときに、カーネルモードドライバーが格納される構造体[*DxgkDdiQueryAdapterInfo* ](https://msdn.microsoft.com/library/windows/hardware/ff559746)呼び出します。 カーネル モード ドライバーにも入力、 [ **DXGK\_GPUMMUCAPS** ](https://msdn.microsoft.com/library/windows/hardware/dn906348) GPU 仮想のアドレス指定のサポートを記述する構造体の上限を設定します。

各プロセスでは、GPU 仮想アドレス空間があります。 実行のプロセスのグラフィックス コンテキストを設定できる前に、カーネル モード ドライバーが表示されます、 [ *DxgkDdiSetRootPageTable* ](https://msdn.microsoft.com/library/windows/hardware/dn906342)呼び出し、ルート ページ テーブルのアドレスを設定します。

2 つのページ テーブル レベルの大文字と小文字の仮想アドレス変換は、次の図に表示されます。

![2 つのページ テーブル レベルの大文字と小文字の仮想アドレス変換が表示されます。](images/gpu-virtual-address.1.png)

GPU の仮想アドレスが[ **DXGK\_GPUMMUCAPS**](https://msdn.microsoft.com/library/windows/hardware/dn906348)::**VirtualAddressBitCount**ビット。

下位ビット\[0 - 11\]ページ内のバイト オフセットを表します。 次[ **DXGK\_ページ\_テーブル\_レベル\_DESC**](https://msdn.microsoft.com/library/windows/hardware/dn906832)::**PageTableIndexBitCount**ビットを表し、リーフ レベルのページ テーブル内のページ テーブル エントリのインデックス。

ページ テーブル内のエントリの数は 2<sup>DXGK\_ページ\_テーブル\_レベル\_DESC::PageTableIndexBitCount</sup>ページ テーブルのサイズと[ **DXGK\_ページ\_テーブル\_レベル\_DESC**](https://msdn.microsoft.com/library/windows/hardware/dn906832)::**PageTableSizeInBytes**バイト。

残りのビットは、ルート ページ テーブル内のページ テーブル エントリにインデックスを表します。 ルート ページのテーブルが 2 レベルの変換のスキームと新しいサイズを変更できる[ *DxgkDdiGetRootPageTableSize*](https://msdn.microsoft.com/library/windows/hardware/dn906339)のサイズを取得する DDI が導入されました。

[ **DXGK\_PTE** ](https://msdn.microsoft.com/library/windows/hardware/ff562008)ページ テーブル エントリを表す DDI を通じて構造体を使用します。 この構造体は、各エントリは、Microsoft DirectX グラフィックスのカーネルの管理に関する情報を表します。 ドライバーでは、この情報を使用して、ハードウェア固有のページ テーブル エントリを作成します。

## <a name="span-idcreationofpagetableallocationsspanspan-idcreationofpagetableallocationsspanspan-idcreationofpagetableallocationsspancreation-of-page-table-allocations"></a><span id="Creation_of_page_table_allocations"></span><span id="creation_of_page_table_allocations"></span><span id="CREATION_OF_PAGE_TABLE_ALLOCATIONS"></span>ページ テーブルの割り当ての作成


ページ テーブルは、暗黙的な割り当てとして作成され、ユーザー モード ドライバーやカーネル モード ドライバーの処理はありません。

ビデオ メモリ マネージャがサイズの割り当てを割り当てるページ テーブルを割り当て、 [ **DXGK\_ページ\_テーブル\_レベル\_DESC**](https://msdn.microsoft.com/library/windows/hardware/dn906832)::**PageTableSizeInBytes**で指定されたセグメントから**DXGK\_ページ\_テーブル\_レベル\_DESC**::**PageTableSegmentId**. ビデオ メモリ マネージャーの作成後にページの表に、すべてのエントリを初期化します*無効な*新しい[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)操作をページングします。 ページ テーブルは、を除き、2 レベルの変換の構成でルート ページ テーブルのサイズを変更することはありません。

ビデオ メモリ マネージャーでは、2 レベルの変換の方法で、ルート ページ テーブルのサイズ変更をサポートします。 ビデオ メモリ マネージャーは、新しい、アドレス空間の指定された量をカバーする、ルート ページ テーブルの作成に[ *DxgkDdiGetRootPageTableSize*](https://msdn.microsoft.com/library/windows/hardware/dn906339)DDI 必要な割り当てを確認するにはサイズ。 ビデオ メモリ マネージャーで指定されたセグメントでは、そのサイズの割り当てを割り当てます[ **DXGK\_ページ\_テーブル\_レベル\_DESC**](https://msdn.microsoft.com/library/windows/hardware/dn906832):。**PageTableSegmentId**ルート レベルにします。 ビデオ メモリ マネージャーの作成後に、new を使用して無効なページの表に、すべてのエントリを初期化します[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)操作をページングします。 ルート ページのテーブルでは、拡張したり、プロセスに必要なビデオのアドレス領域の量の展開し、縮小を縮小することができます。 ビデオ メモリ マネージャーは、新しい、ルート ページのテーブルが作成されると、 [ *DxgkDdiSetRootPageTable*](https://msdn.microsoft.com/library/windows/hardware/dn906342)DDI さまざまなコンテキスト内で実行すると、新しく作成したルートのページ テーブルを関連付ける.

リンクされたディスプレイ アダプターの構成ではルート ページ テーブルとして作成されます*LinkMirrored*割り当ては、同一のコンテンツおよびリンクには、各 GPU 上で同じ物理アドレスであります。 として割り当てられている下位レベルのページ テーブル*LinkInstanced*割り当て、コンテンツは、マッピングのさまざまなピアにより通常の GPU の間で異なる可能性があるという事実を反映するようにします。 ページのテーブルの内容は、すべての Gpu に個別に更新されます。

## <a name="span-idgrowingandshrinkingarootpagetablespanspan-idgrowingandshrinkingarootpagetablespanspan-idgrowingandshrinkingarootpagetablespangrowing-and-shrinking-a-root-page-table"></a><span id="Growing_and_shrinking_a_root_page_table"></span><span id="growing_and_shrinking_a_root_page_table"></span><span id="GROWING_AND_SHRINKING_A_ROOT_PAGE_TABLE"></span>拡大および縮小ルート ページのテーブル


このセクションでは、システム ページ テーブルの 2 つのレベルでのみ適用できます。 ページ テーブル レベルの数が 2 では、各レベルのページ テーブルのサイズを超える場合が仮想のアドレス指定の上限によって定義され、固定します。

ユーザー モード ドライバーでは、GPU の仮想アドレスを要求するときに、ビデオ メモリ マネージャーは、要求に対応するプロセスのアドレス空間のサイズを拡大します。 これは、新しいページ テーブルを新しい範囲の割り当てと (必要に応じて) 現在のルート ページ テーブルのサイズを拡大することにより実現されます。

ルート ページのテーブルを拡張するビデオ メモリ マネージャー別のルート ページ テーブルの割り当てを作成、常駐、なりますおよびを使用してそのエントリを初期化します[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815)操作し、古いの破棄割り当てです。 [ *DxgkDdiGetRootPageTableSize* ](https://msdn.microsoft.com/library/windows/hardware/dn906339)関数を使用して、新しいページ テーブルのサイズをバイト単位で取得します。

ルート ページのテーブルを圧縮するには、ビデオ メモリ マネージャー新しいページ テーブルの割り当てを作成し、により、常駐、新しい 1 つを使用する古いページ テーブルの一部をコピー、 *CopyRootPageTable*ページング操作し、古いの破棄割り当てです。

サイズ変更操作の完了後、ビデオ メモリ マネージャーの呼び出し、 [ *DxgkDdiSetRootPageTable*](https://msdn.microsoft.com/library/windows/hardware/dn906342)DDI に影響を受けるコンテキストに、新しいルート ページ テーブルを関連付けます。

## <a name="span-idupdatingpagetablespanspan-idupdatingpagetablespanspan-idupdatingpagetablespanupdating-page-table"></a><span id="Updating_page_table"></span><span id="updating_page_table"></span><span id="UPDATING_PAGE_TABLE"></span>ページ テーブルを更新しています


サーフェスがメモリ内で移動も、ビデオ メモリ マネージャーは、サーフェスの新しい場所を反映するようにページ テーブルの内容を更新します。 これを行う新しい[ *UpdatePageTable* ](https://msdn.microsoft.com/library/windows/hardware/ff560815) Ddi をページングします。

## <a name="span-idmovingapagetablespanspan-idmovingapagetablespanspan-idmovingapagetablespanmoving-a-page-table"></a><span id="Moving_a_page_table"></span><span id="moving_a_page_table"></span><span id="MOVING_A_PAGE_TABLE"></span>ページ テーブルの移動


ページ テーブルを再配置またはデバイスがアイドル状態または中断されたときに、ビデオ メモリ マネージャーによって削除された可能性があります。 更新プログラムを使用して、ページ テーブルの新しい場所を参照するより高いレベルのページ テーブルのビデオ メモリ マネージャー ページ テーブルを移動するときに、 [ *UpdatePageTable*](https://msdn.microsoft.com/library/windows/hardware/ff560815)Ddi します。

ビデオ メモリ マネージャーは、ルート ページ テーブル自体が再配置される場合、 [ *DxgkDdiSetRootPageTable*](https://msdn.microsoft.com/library/windows/hardware/dn906342)DDI、新しいディレクトリの場所のページの影響を受けるコンテキストに通知します。

## <a name="span-idphysicalpagesizespanspan-idphysicalpagesizespanspan-idphysicalpagesizespanphysical-page-size"></a><span id="Physical_page_size"></span><span id="physical_page_size"></span><span id="PHYSICAL_PAGE_SIZE"></span>物理的なページ サイズ


説明したように以前、ビデオ メモリ マネージャー サポートしている 2 つのページ サイズ。 4 KB のページでは、システム メモリが、4 KB またはカーネル モード ドライバーによって決定される 64 KB の粒度のいずれかで管理できるのメモリ セグメント中に常に管理されています。

すべての割り当てが自動的に配置され、に対して複数のサイズを 64 KB のページで管理できる仮想メモリの停止、する場合に 64 KB です。

64 kb のすべての割り当てを展開すると、大量のメモリに影響することができます。 1 つメモリの無駄使いを回避したり、小さな割り当てをパックするユーザー モード ドライバーの役目です。

GPU の仮想アドレスを大規模な 64 KB のメモリ セグメントのページにマップするときに、ビデオ メモリ マネージャーは 4 KB のページ テーブル エントリをメモリ セグメントに連続する 16 の 4 KB ページにマップされます。 (つまり、仮想アドレスと物理アドレスの下位 16 ビットは一致する保証します。) 同じ 64 KB のアラインメントを共有する仮想アドレスと物理アドレスの両方が保証されます。

 

 





