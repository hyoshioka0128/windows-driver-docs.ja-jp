---
title: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
description: DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
ms.assetid: 2aef590f-2328-4175-ab60-c72b1fd83db7
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM
- 拡張形式 DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM、WDK の Windows 7 の表示
- DXGI_FORMAT_R10G10B10_XR_BIAS_A2_UNORM WDK Windows 7 の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 764d0f469421249e0a5f2849f1e54f480a045045
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372062"
---
# <a name="dxgiformatr10g10b10xrbiasa2unorm"></a>DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式には、バイアスをかけた形式に関連付けられているデータの性質を認識するアプリケーションが必要です。 シェーダーが XR の対応である必要があります、次のセクションで、変換規則からわかるように、\_バイアスから読み込まれたり、DXGI に書き込まれたデータで独自のバイアスとスケールを実行する必要がありますと\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式。

スキャン アウト ハードウェアは、バイアスとスケールを適用できる必要があります。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式には、表示スキャン アウト、CPU のロック可能なおよび「ビット レイアウト内でキャスト」リソースの属性のみです。 そのため、リソースをレンダリングするアプリケーション通常作成 DXGI 形式のレンダー ターゲット ビュー\_形式\_R10G10B10A2\_\*します。

すべての機能をディスプレイのミニポート ドライバーが XR をサポートする必要があります\_表示形式としてバイアス。 新しい D3DDDIFMT\_A2B10G10R10\_XR\_バイアスの値に追加された、 [ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat) XR の列挙体\_バイアス サポートします。

 

 





