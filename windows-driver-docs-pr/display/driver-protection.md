---
title: ドライバー保護
description: ビデオメモリマネージャーでは、すべての仮想アドレスに加えて、独立系ハードウェアベンダー (Ihv) がドライバー/ハードウェア固有の保護を定義することができます (つまり、
ms.assetid: 3D636BD1-683D-49B4-A7E5-176853EA11EE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99b619713892465b0c2a92d41197f11db1db7314
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839744"
---
# <a name="driver-protection"></a>ドライバー保護


ビデオメモリマネージャーでは、すべての仮想アドレスと共に、専用のハードウェアベンダー (Ihv) が、その仮想アドレスに関連付けられたドライバー/ハードウェア固有の保護 (つまり、ページテーブルの入力エンコード) を定義できます。 ドライバー保護については、ビデオメモリマネージャーが認識していないページテーブルエントリの余分な部分を考えてみてください。ただし、最適な方法でグラフィックス処理装置 (GPU) がメモリにアクセスするためには、ドライバーで制御する必要があります。

**注**  ドライバー保護は省略可能であり、この機能を必要としないプラットフォームではゼロのままにすることができます。

 

GPU 仮想アドレス範囲をマッピングまたは予約する場合、ドライバーは64ビットのドライバー保護値を指定できます。 指定されたドライバー保護は、その特定の仮想アドレスに対応するページテーブルエントリを初期化するときにビデオメモリマネージャーによって使用されます。 具体的には、指定された仮想アドレスに対応する **\_ページ\_テーブルを更新\_** 、 [*Buildpagingbuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)DXGK\_操作のドライバーに対してドライバー保護が返されます。

異なるドライバー保護を使用して、複数の仮想アドレスを1つの割り当てにマップすることができます。 これらの各仮想アドレスのページテーブルエントリは、適切なドライバー保護を使用して更新されます。

ドライバー保護は、レベル0のページテーブルエントリにのみ適用され、その他のページテーブルエントリレベルでは0に設定されます。

## <a name="span-idpaging_and_unique_driver_protectionspanspan-idpaging_and_unique_driver_protectionspanspan-idpaging_and_unique_driver_protectionspanpaging-and-unique-driver-protection"></a><span id="Paging_and_unique_driver_protection"></span><span id="paging_and_unique_driver_protection"></span><span id="PAGING_AND_UNIQUE_DRIVER_PROTECTION"></span>ページングと固有のドライバー保護


メモリセグメント内で割り当てをページングする場合、ビデオメモリマネージャーは、割り当てのコンテンツを転送するために、システムデバイスアドレス空間から一時的な仮想アドレスを割り当てます。 このマッピングを作成するときに、異なるドライバー保護を使用するさまざまなプロセスアドレス空間に複数のマッピングが存在する可能性があるため、割り当てに関連するドライバー保護があいまいになります。

このため、ビデオメモリマネージャーは、既定でページングに使用されるすべてのシステムデバイスマッピングのドライバー保護を0に指定します。

ドライバーは、仮想アドレスに関連付けられたドライバー保護を指定するときに、**一意**のビットを設定することによって、この動作を変更できます。

`#define D3DGPU_UNIQUE_DRIVER_PROTECTION 0x8000000000000000ULL`

このビットが設定されている場合、ビデオメモリマネージャーは、同じ割り当て範囲へのマッピングが同じドライバー保護値を使用することを強制します。または、マッピング要求が失敗し、**状態\_無効\_パラメーター**で失敗します。

一意のドライバー保護値でマップされた割り当て範囲は、別の保護値で再度マップすることはできません。 この場合、保護を変更する唯一の方法は、範囲をアクセスなしでマップすることです。

一意でないドライバー保護値でマップされた割り当て範囲は、保護の値を使用して再度マップできます。

ドライバー保護が "*一意*" に設定された仮想アドレス範囲が割り当てられている割り当てを解除すると、ビデオメモリマネージャーによって、適切なドライバー保護値を持つその範囲に対して、あいまいさのないページングプロセスマッピングが設定されます。

次の図は、異なるドライバー保護値を持つ割り当てに対する VA マッピングを示しています。

![異なるドライバー保護を使用した割り当て用の仮想アドレスマッピング](images/driver-protection.1.png)

ページング操作中、割り当てはチャンク単位でコピーされます。

1. コピー割り当て範囲 \[0、A1\] ドライバー保護0
2. ドライバー保護 P1 での \[A1、A2\] の割り当て範囲のコピー
3. コピー割り当て範囲 \[A2, A4\] とドライバー保護0
4. ドライバー保護 P4 での \[A4、A5\] のコピー割り当て範囲
5. コピー割り当ての範囲 \[A5、サイズ\] ドライバー保護0を使用します。割り当てが削除され、割り当てがコミットされるときに別の値に設定されると、ページングプロセスページテーブルエントリが1つのドライバー保護値で設定される可能性があります。 仮想アドレスマッピングが更新された後、ドライバーが割り当てデータを更新する必要があると想定されています。
たとえば、現在の割り当てマッピングセットが M1 で、ユーザーモードドライバーが[*Updat・ Pupuvirtualaddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)とマッピングセット M2 で呼び出されている場合を考えてみます。 マッピングセット M2 が適用される直前に、ビデオメモリマネージャーによって割り当てが削除されます。 マッピングセット M2 が適用され、割り当てがコミットされます。 これで、ローカルメモリセグメントの割り当てコンテンツが元のものと異なる場合があります。

## <a name="span-idtiled_resourcesspanspan-idtiled_resourcesspanspan-idtiled_resourcesspantiled-resources"></a><span id="Tiled_Resources"></span><span id="tiled_resources"></span><span id="TILED_RESOURCES"></span>タイルリソース


タイル化されたリソースの場合、仮想アドレス範囲を予約するときにドライバー保護が指定されます。 [*Updat/Puvirtualaddress*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updategpuvirtualaddresscb)へのユーザーモードドライバーの呼び出しでは、仮想アドレスの現在のドライバー保護が継承されます。

 

 





