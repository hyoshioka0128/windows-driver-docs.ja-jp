---
title: シェーダー 2 サポートの機能のレポート
description: シェーダー 2 サポートの機能のレポート
ms.assetid: 27397e32-cdc0-47b5-b9b5-a4b22ed971f3
keywords:
- シェーダー WDK DirectX 9.0、シェーダー2.0 のサポート
- 頂点シェーダー WDK DirectX 9.0、シェーダー2.0 のサポート
- ピクセルシェーダー WDK DirectX 9.0、シェーダー2.0 のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e019992e95183f1a1e63a5d2ae2e0e51e38c941d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825946"
---
# <a name="reporting-capabilities-for-shader-2-support"></a>シェーダー 2 サポートの機能のレポート


## <span id="ddk_reporting_capabilities_for_shader_2_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_2_SUPPORT_GG"></span>


ピクセルまたは頂点シェーダーバージョン2.0 以降をサポートするディスプレイデバイス用の DirectX 9.0 バージョンドライバーは、次の機能をサポートしていることを示す必要があります。

デバイスで頂点シェーダー2.0 以降がサポートされている場合、そのドライバーは、D3DCAPS9 構造体のメンバーを次の値に設定する必要があります。

-   デバイスが8個以上の同時実行データストリームを処理できることを示すために、 **Maxstreams**メンバーを8以上に設定します。

-   **DeclTypes**メンバーの D3DDTCAPS\_UBYTE4 bit を1に設定して、UBYTE4 vertex 要素型のサポートを示します。 詳細については、「 [Reporting Support FOR UBYTE4 Vertex Element](reporting-support-of-ubyte4-vertex-element.md)」を参照してください。

デバイスでピクセルシェーダー2.0 以降がサポートされている場合、ドライバーで2次元のテクスチャマッピングがサポートされているかどうかを示すために、 **Texturecaps**メンバーで次のビットを構成する必要があります。 詳細については、 [**D3DPRIMCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps)のリファレンスページでこれらのビットの説明を参照してください。

-   D3DPTEXTURECAPS\_POW2 と D3DPTEXTURECAPS\_NONPOW2CONDITIONAL ビットを1に設定して、条件付きサポートを示します。

-   D3DPTEXTURECAPS\_POW2 と D3DPTEXTURECAPS\_NONPOW2CONDITIONAL ビットを0に設定します (つまり、これらのビットは設定しないでください)。無条件のサポートが示されます。

 

 





