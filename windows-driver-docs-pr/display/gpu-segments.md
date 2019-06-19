---
title: GPU セグメント
description: グラフィックス プロセッシング ユニット (GPU) への物理メモリは、セグメント化モデルによって、デバイス ドライバー インターフェイス (DDI) の抽象化されています。
ms.assetid: E6CAD808-73C0-48AB-BF95-76911D5C104A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ecf2d534acfc82044c7aec174a042297da8f7df
ms.sourcegitcommit: 6dff49ca5880466c396be5b889c44481dfed44ec
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2019
ms.locfileid: "67161446"
---
# <a name="gpu-segments"></a>GPU セグメント


グラフィックス プロセッシング ユニット (GPU) への物理メモリは、セグメント化モデルによって、デバイス ドライバー インターフェイス (DDI) の抽象化されています。 カーネル モード ドライバーでは、一連のビデオ メモリ マネージャーによって管理される、セグメントを列挙することで、GPU で使用できる物理メモリ リソースを表します。

Windows Display Driver Model (WDDM) v2 でのセグメントの 3 つの種類があります。

<span id="Memory_Segment"></span><span id="memory_segment"></span><span id="MEMORY_SEGMENT"></span>メモリのセグメント  
メモリのセグメントは、専用の GPU メモリを表します。 不連続の GPU 上で VRAM または統合の GPU 上で予約されているファームウェアとドライバーのメモリがあります。 複数のメモリ セグメントを列挙できます。

新しい WDDM v2 でのメモリ セグメントは、プール サイズの 4 KB (64 kb) のいずれかである物理ページの管理します。 画面のデータがコピーを使用してメモリ セグメントの出入り*入力*/*転送*/*破棄*/ *FillVirtuall*/*TransferVirtual*ページング操作。

CPU は、2 つの方法のいずれかでメモリのセグメントのコンテンツにアクセスできます。 最初に、メモリ セグメントをケース ビデオ メモリ マネージャーだけ CPU 仮想アドレスに直接マップされます、セグメント内の割り当て、CPU の物理アドレス空間に表示される場合があります。 新しい WDDM v2 でのビデオ メモリ マネージャーもサポートそのセグメントに関連付けられている、プログラミング可能な CPU ホスト aperture を通じてメモリ セグメントのコンテンツにアクセスします。

<span id="Aperture__Segment"></span><span id="aperture__segment"></span><span id="APERTURE__SEGMENT"></span>Aperture セグメント  
Aperture セグメントは、連続していないシステムのメモリ ページを作成するために使用するグローバル ページ テーブルが GPU エンジンの観点から連続して表示されます。

WDDM v2 では、1 つの開口部セグメントを報告する必要があります。

<span id="System_Memory_Segment"></span><span id="system_memory_segment"></span><span id="SYSTEM_MEMORY_SEGMENT"></span>システム メモリのセグメント  
システム メモリのセグメントには、システム メモリ参照 (つまりゲスト物理アドレス) を表す暗黙的なセグメントです。 直接、システム メモリのセグメントは、カーネル モード ドライバーでは列挙されません。 常に割り当てを取得し、ビデオ メモリ マネージャーによって暗黙的に列挙された`SegmentId==0`します。 システム メモリのセグメントの割り当てを配置するには、カーネル モード ドライバーは aperture セグメント ID を使用する必要があります。

## <a name="span-idphysicalmemoryreferencespanspan-idphysicalmemoryreferencespanspan-idphysicalmemoryreferencespanphysical-memory-reference"></a><span id="Physical_memory_reference"></span><span id="physical_memory_reference"></span><span id="PHYSICAL_MEMORY_REFERENCE"></span>物理メモリの参照


DDI、物理メモリ参照は常に、セグメント ID のセグメントのオフセットのペアの形式になります。

## <a name="span-idaccessingallocationsbyphysicaladdressspanspan-idaccessingallocationsbyphysicaladdressspanspan-idaccessingallocationsbyphysicaladdressspanaccessing-allocations-by-physical-address"></a><span id="Accessing_allocations_by_physical_address"></span><span id="accessing_allocations_by_physical_address"></span><span id="ACCESSING_ALLOCATIONS_BY_PHYSICAL_ADDRESS"></span>物理アドレスの割り当てにアクセスします。


GPU エンジンは、GPU の仮想アドレス指定をサポートしていないは、物理アドレスを介して割り当てにアクセスする必要があります。 これは、割り当てが取得されたセグメントから別のリソースをどのように割り当てられている方法に影響があります。 物理参照では、割り当てが連続してメモリ セグメントに割り当てる必要がありますまたは aperture セグメント内で連続した範囲が占めることを意味します。

明示的に識別する、カーネル モード ドライバーする必要があります、レンダリング エンジンで、新しい設定が物理的にアクセスする必要の割り当て、不要かつ高価な連続した割り当てを避けるためには、 [ **DXGK\_ALLOCATIONINFOFLAGS2**](https://msdn.microsoft.com/library/windows/hardware/ff560970)::**AccessedPhysically**フラグの割り当ての作成時にします。

このような割り当ては、システム メモリに常駐しているときに、aperture セグメントにマップされます。 割り当ては連続したは、メモリのセグメントに常駐しているときになります。 、この方法で作成された割り当ては、物理アドレス指定モードで動作しているエンジンに割り当ての一覧を参照できます。

割り当てで、これがないは、フラグを設定した、メモリ セグメント内のページのセットまたは一連のシステムのメモリ内でページには GPU の仮想アドレスを通じてアクセスするのいずれかとして割り当てられます。 この方法で作成された割り当ては、割り当ての一覧を参照できません。 これにより、割り当てを参照しているコマンド バッファーの提出マテリアルの使用は拒否されます。

プライマリ サーフェスは表示コント ローラーが物理的にアクセスする理解されると、連続して割り当てられたメモリのセグメントでまたは表示されるときに、aperture セグメントにマップするは。 カーネル モード ドライバーを設定する必要がありますのみ、 **AccessedPhysically**レンダリング エンジンが、割り当てを物理的にアクセスするときにフラグを設定します。 プライマリ画面で暗黙的な物理的なアクセスと明示的なフラグの違いとは、割り当ての開口部にマップされる場合です。 ときに、 **AccessedPhysically**フラグが設定されている、常駐しているときに、割り当ては開口部にマップされます。 プライマリ サーフェスは、これがないは、フラグが設定されて、表示されている場合にのみの開口部にマップされます。 Aperture セグメント上の負荷を削除するには、これにより、通常は積極的に表示されている既存に表示されるに非常に多くのことがありますが、いくつかプライマリ画面のみ (つまり、すべて*FlipEx*スワッププライマリおよび表示可能な可能性のあるサーフェスとして作成*dFlip*/*iFlip*シナリオ)。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"></td>
<td align="left">AccessedPhysically 0 を = =</td>
<td align="left">AccessedPhysically 1 = =</td>
<td align="left">プライマリ (& a) (& a) AccessedPhysically 0 を = =</td>
</tr>
<tr class="even">
<td align="left">メモリのセグメント</td>
<td align="left"><p><strong>ページのセット</strong></p>
<p>GPU 仮想アクセスのみが許可されます。</p></td>
<td align="left"><p><strong>連続します。</strong></p>
<p>GPU の物理アクセスが許可されます。</p></td>
<td align="left"><p><strong>連続します。</strong></p>
<p>GPU 仮想アクセスのみが、レンダリング エンジンで許可されます。</p></td>
</tr>
<tr class="odd">
<td align="left">Aperture セグメント</td>
<td align="left"><p><strong>マップされていません</strong></p>
<p>Aperture セグメントが、GPU のページ テーブルによってのみにマップされる、システム メモリ ページです。</p>
<p>GPU 仮想アクセスのみが許可されます。</p></td>
<td align="left"><p><strong>常駐しているときに、マップ</strong></p>
<p>GPU の物理アクセスが許可されます。</p></td>
<td align="left"><p><strong>表示されるときに、マップ</strong></p>
<p>GPU 仮想アクセスのみが、レンダリング エンジンで許可されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





