---
title: 高次パッチ サーフェスのサポート
description: 高次パッチ サーフェスのサポート
ms.assetid: 020fb91c-c8cd-43e8-a180-bbb2ef606be8
keywords:
- 上位のパッチが適用されたサーフェス WDK DirectX 9.0
- 変位の WDK DirectX 9.0 のマッピング
- テセレーション アダプティブ レンダリング WDK DirectX 9.0 を状態します。
- テセレーションの WDK DirectX 9.0 のマッピング
- パッチが適用されたサーフェス WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d4f3d4a323adc5d0b822740d0edf85e7b2e52c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355542"
---
# <a name="supporting-high-order-patched-surfaces"></a>高次パッチ サーフェスのサポート


## <span id="ddk_supporting_high_order_patched_surfaces_gg"></span><span id="DDK_SUPPORTING_HIGH_ORDER_PATCHED_SURFACES_GG"></span>


上位のパッチが適用されたサーフェスする必要があります機能ビットでは、このようなサポートを示す、新しいアダプティブ テセレーションを処理できるアダプティブ テセレーション、変位マッピングをサポートするデバイスの DirectX 9.0 バージョンのドライバーの状態を表示して、置き換えマップ テクスチャ段階の状態。 アダプティブ テセレーションと変位マッピングする方法の詳細については、最新の DirectX SDK を参照してください。

アダプティブ テセレーションと変位マッピングのサポートを指定するには、ドライバー次の機能のビットを設定、 **DevCaps2** D3DCAPS9 構造体のメンバー。

<span id="D3DDEVCAPS2_ADAPTIVETESSRTPATCH"></span><span id="d3ddevcaps2_adaptivetessrtpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSRTPATCH  
デバイスでは、レンダー ターゲットの更新プログラムがテセレーション続けことができます。

<span id="D3DDEVCAPS2_ADAPTIVETESSNPATCH"></span><span id="d3ddevcaps2_adaptivetessnpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSNPATCH  
デバイスでは、N 更新プログラムがテセレーション続けことができます。

<span id="D3DDEVCAPS2_DMAPNPATCH"></span><span id="d3ddevcaps2_dmapnpatch"></span>D3DDEVCAPS2\_DMAPNPATCH  
デバイスは、N 更新プログラムの置き換えマップをサポートします。

<span id="D3DDEVCAPS2_PRESAMPLEDDMAPNPATCH"></span><span id="d3ddevcaps2_presampleddmapnpatch"></span>D3DDEVCAPS2\_PRESAMPLEDDMAPNPATCH  
デバイスは、N 更新プログラムの置き換え presampled マップをサポートします。

N パッチ目盛り表示デバイスをサポートできる、ドライバーのセットの最大数を示すために、 **MaxNpatchTessellationLevel**最大数に D3DCAPS9 構造体のメンバー。 この最大数にクランプするデバイスでは、presampled 変位マッピングを使用するアプリケーションが影響します。

ドライバーへの応答で D3DCAPS9 構造体を返す、 **GetDriverInfo2** 」の説明に従って D3DCAPS8 構造体を返すにする方法と同様にクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

ドライバーの指定、D3DFORMAT\_OP\_DMAP フラグ、 **dwOperations**のメンバー、 [ **DDPIXELFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)特定の構造置き換えマップ サンプリングの形式をマークする画面形式です。 テクスチャ サーフェスを作成すると、Direct3D のランタイム設定、DDSCAPS3\_DMAP ビット、 **dwCaps3** 、DDSCAPSEX のメンバー ([**DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 構造体テセレーション単位にテクスチャをサンプリングすることを示します。

DirectX 9.0 と以降のドライバーが N パッチ機能を無効にする必要があることに注意してください。 場合にのみ、D3DRS @property\_PATCHSEGMENTS でレンダリング状態は、1.0 f より小さい。 DirectX 8.1 と以前のドライバーは、このように動作する必要はありません。

既定値と共に次のテセレーション アダプティブ レンダリング状態には、DirectX 9.0 の新機能

D3DRS\_MAXTESSELLATIONLEVEL 1.0f を =

D3DRS\_MINTESSELLATIONLEVEL 1.0f を =

D3DRS\_ADAPTIVETESS\_X = 0.0 f

D3DRS\_ADAPTIVETESS\_Y = 0.0 f

D3DRS\_ADAPTIVETESS\_Z = 1.0f

D3DRS\_ADAPTIVETESS\_W = 0.0f

D3DRS\_ENABLEADAPTIVETESSELLATION = **FALSE**

これは DirectX 9.0 の新機能も、D3DDMAPSAMPLER サンプラーは、置き換えマップ テクスチャを設定するテセレーション単体で使用されます。

**注**   DirectX 9.0 と以降のアプリケーションは、D3DSAMP を使用できる\_DMAPOFFSET presampled 置き換えマップにコントロールを頂点のオフセットを D3DSAMPLERSTATETYPE 列挙値。 ランタイムは、ユーザー モード サンプラーの状態をマップ (D3DSAMP\_*Xxx*) には、カーネル モード D3DTSS\_*Xxx*値 DirectX 9.0 と以降のドライバーは処理する必要はありませんユーザー モード サンプラーの状態。 そのため、ドライバーには、D3DTSS が処理しなければならない代わりに\_DMAPOFFSET 値、 **TSState**のメンバー、 [ **D3DHAL\_DP2TEXTURESTAGESTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)D3DDP2OP 構造\_TEXTURESTAGESTATE 操作。 D3DSAMPLERSTATETYPE と presampled 変位マッピングする方法の詳細については、DirectX SDK の最新のドキュメントを参照してください。

 

 

 





