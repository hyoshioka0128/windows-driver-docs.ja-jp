---
title: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
description: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
ms.assetid: 2aef590f-2328-4175-ab60-c72b1fd83db7
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- 拡張形式 WDK Windows 7 display、DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM WDK Windows 7 ディスプレイ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ad036b530d8443c05fd4de31ee01976a12d26d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838973"
---
# <a name="dxgi_format_r10g10b10_xr_bias_a2_unorm"></a>DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式では、アプリケーションは、形式に関連するデータのバイアスを持つ性質を認識している必要があります。 次のセクションの変換規則からわかるように、シェーダーは XR\_バイアスを認識している必要があります。また、R10G10B10\_XR\_形式で読み取りまたは\_書き込みが行われるすべてのデータに対して、独自のバイアスとスケールを行う必要があります。\_バイアス\_A2\_UNORM 形式です。

スキャンアウトハードウェアでは、バイアスとスケールを適用できる必要があります。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式には、表示スキャンアウト、CPU ロック可能、および "ビットレイアウト内でのキャスト" リソース属性のみがあります。 そのため、リソースにレンダリングするには、通常、アプリケーションでは、R10G10B10A2\_\*形式\_、DXGI\_形式のレンダーターゲットビューを作成します。

すべての機能を使用するには、ディスプレイミニポートドライバーで、表示形式として XR\_バイアスがサポートされている必要があります。 XR\_バイアスサポートの[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)列挙に新しい D3DDDIFMT\_A2B10G10R10\_XR\_バイアス値が追加されました。

 

 





