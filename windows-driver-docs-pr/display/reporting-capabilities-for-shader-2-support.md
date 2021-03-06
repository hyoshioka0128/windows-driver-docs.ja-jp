---
title: シェーダー 2 サポートの機能のレポート
description: シェーダー 2 サポートの機能のレポート
ms.assetid: 27397e32-cdc0-47b5-b9b5-a4b22ed971f3
keywords:
- シェーダー WDK DirectX 9.0、シェーダー 2.0 のサポート
- 頂点シェーダー WDK DirectX 9.0、シェーダー 2.0 のサポート
- ピクセル シェーダー WDK DirectX 9.0、シェーダー 2.0 のサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd8ba775cad982606efaa804e342b127d737a412
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372754"
---
# <a name="reporting-capabilities-for-shader-2-support"></a>シェーダー 2 サポートの機能のレポート


## <span id="ddk_reporting_capabilities_for_shader_2_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_2_SUPPORT_GG"></span>


2\.0 以降のピクセルまたは頂点シェーダーのバージョンをサポートしているディスプレイ デバイスの DirectX 9.0 バージョンのドライバーでは、次の機能をサポートしているを示す必要があります。

デバイスは、頂点シェーダー 2.0 以降をサポートする場合、そのドライバーは、次の値に D3DCAPS9 構造体のメンバーを設定する必要があります。

-   設定、 **MaxStreams**をデバイスが 8 または多くの同時実行データ ストリームを処理できることを示すために、少なくとも 8 にするメンバー。

-   設定、D3DDTCAPS\_UBYTE4 ビット、 **DeclTypes** UBYTE4 頂点要素型のサポートを示すためのメンバーを 1 にします。 詳細については、次を参照してください。 [Reporting サポートの UBYTE4 頂点要素](reporting-support-of-ubyte4-vertex-element.md)します。

デバイスは、ピクセル シェーダー 2.0 をサポートし、後でそのドライバーが内の以下のビットを構成する必要がある場合、 **TextureCaps**ドライバーがまたは無条件で条件付きでとして nonpowers-2 の 2 次元テクスチャのマッピングをサポートしているかどうかを示すメンバー. 詳細については、これらのビットでの説明を参照して、 [ **D3DPRIMCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dcaps/ns-d3dcaps-_d3dprimcaps)リファレンス ページです。

-   設定、D3DPTEXTURECAPS\_POW2 と D3DPTEXTURECAPS\_NONPOW2CONDITIONAL ビットを 1 に示す条件付きでサポートします。

-   設定、D3DPTEXTURECAPS\_POW2 と D3DPTEXTURECAPS\_NONPOW2CONDITIONAL ビットを 0 (つまり、これらのビットは設定されません) 無条件のサポートを示すためです。

 

 





