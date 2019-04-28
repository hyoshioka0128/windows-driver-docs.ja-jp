---
title: 複数レンダー ターゲットのオプション機能
description: 複数レンダー ターゲットのオプション機能
ms.assetid: 265df4d3-acc9-4978-97d1-a6f81bc7afaf
keywords:
- 複数のターゲット WDK DirectX 9.0、省略可能な機能を表示
- 複数のレンダー ターゲット WDK DirectX 9.0、省略可能な機能
- 同時のレンダー ターゲット WDK DirectX 9.0、省略可能な機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d4919bf071b256753a16a3f85f946fe03752ae8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379842"
---
# <a name="optional-features-for-multiple-render-targets"></a>複数レンダー ターゲットのオプション機能


## <span id="ddk_optional_features_for_multiple_render_targets_gg"></span><span id="DDK_OPTIONAL_FEATURES_FOR_MULTIPLE_RENDER_TARGETS_GG"></span>


同時に複数のターゲットに表示をサポートする DirectX 9.0 バージョンのドライバーでは、拡張機能をサポートできます。 機能のビットを報告することによってこのようなサポートを示す必要があります、ドライバーは、これらの拡張機能をサポートする場合、 **PrimitiveMiscCaps** D3DCAPS9 構造体のメンバー。 ドライバーは、次の拡張機能をサポートできます。

-   複数のレンダー ターゲット グループ内のレンダー ターゲットに対して独立したビット深度を設定します。 レンダー ターゲットは、別の形式を持つことができます。ただし、この機能はサポートされていない場合は、同じビットの深さをレンダー ターゲットが必要です。 D3DPMISCCAPS\_を独立したビット深度のサポートを示す MRTINDEPENDENTBITDEPTHS 機能ビットを設定する必要があります。

-   ピクセル シェーダーの操作の後に複数のレンダー ターゲット グループ内のレンダー ターゲット上で、z 値およびステンシル テスト以外の操作を実行しています。 たとえば、この機能はサポートされていない場合、ドライバーはできません。 ディザー、アルファ テストは、適用霧、blend、またはピクセル シェーダーの操作の後のラスター オペレーションを実行します。 D3DPMISCCAPS\_postpixel シェーダーの操作のサポートを示す MRTPOSTPIXELSHADERBLENDING 機能ビットを設定する必要があります。

    場合 D3DPMISCCAPS\_MRTPOSTPIXELSHADERBLENDING が設定されている、ディスプレイ デバイスが同時に表示されるすべてのレンダー ターゲットに、次の状態を適用する必要があります。

    -   アルファ ブレンドします。 OCi させる場合に限りますレンダー ターゲットをブレンドする色の値を設定します。
    -   アルファ テストします。 OC0; が発生するための比較を設定します。比較に失敗した場合は、すべてのレンダー ターゲットのピクセルが取り消されました。
    -   霧します。 0 以外のターゲットを表示するために霧を適用します。その他のレンダー ターゲットが定義されていません。 ドライバーは、同じ状態を使用してすべてのレンダー ターゲットに霧を適用できます。
    -   ディザーです。 定義されていません。
-   独立した色書き込みマスクの適用 (D3DRS\_COLORWRITEENABLE) レンダリングの複数のターゲットがターゲット グループを表示します。 D3DPMISCCAPS\_を独立した色書き込みマスクのサポートを示す INDEPENDENTWRITEMASKS 機能ビットを設定する必要があります。 場合 D3DPMISCCAPS\_INDEPENDENTWRITEMASKS が設定されている、独立した色書き込みマスクの使用可能な数は、複数のレンダー ターゲット グループ内のレンダー ターゲットの最大数と同じ (、 **NumSimultaneousRTs**D3DCAPS9 構造体のメンバー)。

複数のレンダー ターゲットに対して拡張機能をサポートしているかをピクセル シェーダーのバージョン 3.0 以降をサポートしているディスプレイ デバイスのドライバーが示す必要がありますに注意してください。 詳細については、次を参照してください。[シェーダー 3 のサポートの機能を Reporting](reporting-capabilities-for-shader-3-support.md)します。

 

 





