---
title: 高次パッチ サーフェスのサポート
description: 高次パッチ サーフェスのサポート
ms.assetid: 020fb91c-c8cd-43e8-a180-bbb2ef606be8
keywords:
- 高順序のパッチが適用済みサーフェスの WDK DirectX 9.0
- 変位マッピング WDK DirectX 9.0
- アダプティブテセレーションレンダリングの状態 WDK DirectX 9.0
- テセレーションマッピング WDK DirectX 9.0
- パッチが適用済みのサーフェス WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d5794017680a9d858c887444d21a0544aae9dca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825615"
---
# <a name="supporting-high-order-patched-surfaces"></a>高次パッチ サーフェスのサポート


## <span id="ddk_supporting_high_order_patched_surfaces_gg"></span><span id="DDK_SUPPORTING_HIGH_ORDER_PATCHED_SURFACES_GG"></span>


高順序のパッチが適用されたサーフェイスのアダプティブテセレーションとディスプレイスメントマッピングをサポートするデバイス用の DirectX 9.0 バージョンドライバーは、機能ビットを使用したこのようなサポートを示す必要があり、新しいアダプティブテセレーションレンダリング状態を処理できる必要があります。変位-マップのテクスチャステージの状態。 アダプティブテセレーションと変位マッピングの詳細については、最新の DirectX SDK を参照してください。

アダプティブテセレーションとディスプレイスメントマッピングのサポートを示すために、ドライバーは D3DCAPS9 構造体の**DevCaps2**メンバーに次の機能ビットを設定します。

<span id="D3DDEVCAPS2_ADAPTIVETESSRTPATCH"></span><span id="d3ddevcaps2_adaptivetessrtpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSRTPATCH  
デバイスは、テセレーションのレンダリングターゲットの修正プログラムを使用することができます。

<span id="D3DDEVCAPS2_ADAPTIVETESSNPATCH"></span><span id="d3ddevcaps2_adaptivetessnpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSNPATCH  
デバイスは、テセレーションを使用してアダプティブに更新できます。

<span id="D3DDEVCAPS2_DMAPNPATCH"></span><span id="d3ddevcaps2_dmapnpatch"></span>D3DDEVCAPS2\_DMAPNPATCH  
デバイスは、N パッチのディスプレイスメントマップをサポートしています。

<span id="D3DDEVCAPS2_PRESAMPLEDDMAPNPATCH"></span><span id="d3ddevcaps2_presampleddmapnpatch"></span>D3DDEVCAPS2\_PRESAM氏 DDMAPNPATCH  
デバイスは、N パッチの presampled ディスプレースメントマップをサポートしています。

ディスプレイデバイスでサポートできる N パッチの区分の最大数を指定するために、ドライバーは D3DCAPS9 構造体の**MaxNpatchTessellationLevel**メンバーを最大数に設定します。 Presampled ディスプレースメントマッピングを使用するアプリケーションは、デバイスがこの最大数に固定されることによって影響を受けます。

このドライバーは、 **GetDriverInfo2**クエリに対する応答として、D3DCAPS9 構造体を返します。「 [DirectX 8.0 スタイルの Direct3D 機能の報告](reporting-directx-8-0-style-direct3d-capabilities.md)」で説明されているように、D3DCAPS8 構造体を返す方法と似ています。 このクエリのサポートについては、「 [GetDriverInfo2](supporting-getdriverinfo2.md)のサポート」を参照してください。

ドライバーは、特定のサーフェイス形式に対して、 [**DDD3DFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の**dwoperations**メンバーで、\_OP\_dmap フラグを指定して、ディスプレースメントマップサンプリングの形式をマークします。 テクスチャサーフェイスが作成されると、Direct3D ランタイムは、DDSCAPSEX ([**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 構造体の**DWCAPS3**メンバーの DDSCAPS3\_dmap ビットを設定し、そのテクスチャをテセレーション単位でサンプリングできることを示します。

DirectX 9.0 以降のドライバーでは、D3DRS\_patch SEGMENT render state の値が 1.0 f より小さい場合にのみ、N パッチ機能を無効にする必要があることに注意してください。 DirectX 8.1 以前のドライバーは、この方法で動作する必要はありません。

次のアダプティブテセレーションレンダリング状態と、既定値は DirectX 9.0 の新しいものです。

D3DRS\_MAXTESSELLATIONLEVEL = 1.0 f

D3DRS\_MINTESSELLATIONLEVEL = 1.0 f

D3DRS\_ADAPTIVETESS\_X = 0.0 f

D3DRS\_ADAPTIVETESS\_Y = 0.0 f

D3DRS\_ADAPTIVETESS\_Z = 1.0 f

D3DRS\_ADAPTIVETESS\_W = 0.0 f

D3DRS\_ENABLEADAPTIVETESSELLATION = **FALSE**

D3DDMAPSAMPLER サンプラーは DirectX 9.0 でも新たに追加されています。これは、テセレーション単位でディスプレースメントマップテクスチャを設定するために使用されます。

**   DirectX** 9.0 以降のアプリケーションでは、D3DSAMPLERSTATETYPE 列挙体の D3DSAMP\_DMAPOFFSET 値を使用して、頂点のオフセットを presampled ディスプレースメントマップに制御できます。 ランタイムは、ユーザーモードサンプラーの状態 (D3DSAMP\_*xxx*) をカーネルモードの D3DTSS\_*xxx*値にマップします。これにより、DirectX 9.0 以降のドライバーでは、ユーザーモードのサンプラーの状態を処理する必要がなくなります。 そのため、ドライバーは、D3DDP2OP\_TEXTURESTAGESTATE 操作の[**D3DHAL\_DP2TEXTURESTAGESTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)構造体の**TSSTATE**メンバーの D3DTSS\_dmapoffset 値を処理する必要があります。 D3DSAMPLERSTATETYPE と presampled ディスプレースメントマッピングの詳細については、最新の DirectX SDK のドキュメントを参照してください。

 

 

 





