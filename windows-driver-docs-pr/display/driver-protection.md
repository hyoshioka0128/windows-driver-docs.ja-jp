---
title: ドライバー保護
description: ビデオ メモリ マネージャーにより、独立系ハードウェア ベンダー (Ihv) ドライバーを定義すると共に、すべての仮想アドレス/ハードウェアの特定の保護 (つまり、
ms.assetid: 3D636BD1-683D-49B4-A7E5-176853EA11EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fb9be08be6b35803739c11528c517982c512780
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380376"
---
# <a name="driver-protection"></a>ドライバー保護


ビデオ メモリ マネージャーにより、独立系ハードウェア ベンダー (Ihv) ドライバーを定義すると共に、すべての仮想アドレス/ハードウェアの特定の保護 (つまりページ テーブル エントリのエンコード) 具体的にはその仮想アドレスに関連付けられています。 ドライバー保護、ビデオ メモリ マネージャが把握している最適な方法で、グラフィックス プロセッシング ユニット (GPU) メモリにアクセスするために、ドライバーを制御する必要がありますが、そのページ テーブル エントリで余分なビットとして考えてください。

**注**  ドライバー保護はオプションであり、この機能を必要としない任意のプラットフォームでの 0 のままでかまいません。

 

マッピングまたは GPU 仮想アドレスの範囲を予約するときに、ドライバーは 64 ビット ドライバー保護の値を指定できます。 指定されたドライバー保護は、その特定の仮想アドレスに対応するページ テーブル エントリを初期化するときに、ビデオ メモリ マネージャーによって使用されます。 具体的には、ドライバー保護は指定のドライバーにいずれかの[ *BuildPagingBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)**DXGK\_操作\_UPDATE\_ページ\_テーブル**指定された仮想アドレスに対応します。

別のドライバーの保護を使用して 1 つの割り当てには、複数の仮想アドレスをマップすることがあります。 適切なドライバーの保護を使用して、これらの仮想アドレスの各ページ テーブル エントリが更新されます。

のみ、ドライバー保護はレベル 0 のページ テーブル エントリに適用され、その他のページ テーブル エントリ レベルの場合は 0 に設定されます。

## <a name="span-idpaginganduniquedriverprotectionspanspan-idpaginganduniquedriverprotectionspanspan-idpaginganduniquedriverprotectionspanpaging-and-unique-driver-protection"></a><span id="Paging_and_unique_driver_protection"></span><span id="paging_and_unique_driver_protection"></span><span id="PAGING_AND_UNIQUE_DRIVER_PROTECTION"></span>ページングと一意のドライバー保護


メモリのセグメントの内外で割り当てをページングするには、ビデオ メモリ マネージャーは、割り当てのコンテンツを転送するために、システムのデバイスのアドレス空間から一時的な仮想アドレスを割り当てます。 このマッピングを作成するときに別のドライバー保護でのさまざまなプロセス アドレス空間に複数のマッピングが存在しているため、割り当てに関連するドライバー保護はあいまいです。

このため、ビデオ メモリ マネージャーは既定ではページングに使用されるすべてのシステム デバイス マッピングにゼロのドライバーの保護を指定します。

ドライバーは設定してこの動作を変更することができます、**一意**ビット仮想アドレスに関連付けられているドライバーの保護を指定する場合。

`#define D3DGPU_UNIQUE_DRIVER_PROTECTION 0x8000000000000000ULL`

ビデオ メモリ マネージャーが、同じ割り当て範囲にすべてのマッピングを使用して、同じドライバー保護値、またはマッピングの要求は失敗に適用されますこのビットが設定されている場合**状態\_無効な\_パラメーター**.

ドライバー固有の保護の値を含むマップを割り当ての範囲は、別の保護の値をもう一度マップできません。 ここでアクセスなしの範囲にマップすることは、保護を変更するしかありません。

一意ではないドライバー保護値でマップされる割り当て範囲は、任意の保護の値をもう一度マップできます。

設定をドライバー保護がマップされる仮想アドレスの範囲を持つ割り当てを削除すると*一意*、ビデオ メモリ マネージャーが適切なドライバー保護でこれらの範囲のために使用するページング プロセス マッピングをセットアップあいまいさなしの値。

次の図は、別のドライバーの保護の値を使用し、割り当ての VA マッピングを示します。

![別のドライバーの保護を使用し、割り当ての仮想アドレスのマッピング](images/driver-protection.1.png)

ページング操作中に、割り当てのチャンク単位でコピーします。

1. 割り当ての範囲をコピー \[0、A1\]ドライバー保護 0
2. 割り当ての範囲をコピー \[A1, A2\]ドライバー保護 P1
3. 割り当ての範囲をコピー \[A2、A4\]ドライバー保護 0
4. 割り当ての範囲をコピー \[A4、A5\]ドライバー保護 P4
5. 割り当ての範囲をコピー \[A5、サイズ\]ドライバー保護 0 とことプロセス ページ テーブル エントリをページングするときに設定されます保護値は 1 つのドライバー、割り当てが削除され、割り当てが別の値に設定できますコミットされます。 ドライバーは、仮想アドレスのマッピングを更新した後は、割り当てデータを更新する必要がありますと見なされます。
たとえば、マッピングのセットの現在の割り当てが M1 とユーザー モード ドライバーと呼ばれる場合を考えます[ *UpdateGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)マッピングと M2 を設定します。 M2 を適用すると、マッピングのセットの直前に、ビデオ メモリ マネージャーによって、割り当てを削除することができます。 M2 が適用されるマッピングのセットと、割り当てのコミットが戻ります。 今すぐローカル メモリ セグメントに割り当てコンテンツは、元と異なる可能性があります。

## <a name="span-idtiledresourcesspanspan-idtiledresourcesspanspan-idtiledresourcesspantiled-resources"></a><span id="Tiled_Resources"></span><span id="tiled_resources"></span><span id="TILED_RESOURCES"></span>タイル型のリソース


タイル化されたリソースは、仮想アドレスの範囲を予約するときにドライバー保護を指定します。 ユーザー モード ドライバー呼び出し[ *UpdateGpuVirtualAddress* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)仮想アドレス現在ドライバー保護が継承されます。

 

 





