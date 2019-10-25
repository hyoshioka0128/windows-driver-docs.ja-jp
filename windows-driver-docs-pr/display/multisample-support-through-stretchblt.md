---
title: StretchBlt を介したマルチサンプル サポート
description: StretchBlt を介したマルチサンプル サポート
ms.assetid: c829c612-d09d-4a33-a117-e50b9ed57251
keywords:
- DirectX 8.0 リリースノート WDK Windows 2000 display、マルチサンプリングレンダリング、StretchBlt
- マルチサンプリングレンダリング WDK DirectX 8.0、StretchBlt
- multisamples のレンダリング WDK DirectX 8.0、StretchBlt
- stretch array.blit 操作 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b69c20734c15a0eb0d3027732b1600a273e40a6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840533"
---
# <a name="multisample-support-through-stretchblt"></a>StretchBlt を介したマルチサンプル サポート


## <span id="ddk_multisample_support_through_stretchblt_gg"></span><span id="DDK_MULTISAMPLE_SUPPORT_THROUGH_STRETCHBLT_GG"></span>


マルチサンプリングをサポートするための推奨メカニズムではありませんが、ドライバーでは、サイズの大きいバックバッファーにレンダリングし、ストレッチ blt を実行して大きなバックバッファーを低解像度のプライマリに再サンプリングすることで、マルチサンプリングをサポートできます。 ただし、これが、ドライバーがマルチサンプリングをサポートするメカニズムである場合、ドライバーは D3D8CAPS 構造体の**RasterCaps**メンバーに新しい機能ビット D3DPRASTERCAPS\_STRETCHBLTMULTISAMPLE を設定する必要があります。 D3DCAPS8 の説明については、DirectX 8.0 SDK のドキュメントを参照してください。

ドライバーで D3DPRASTERCAPS\_STRETCHBLTMULTISAMPLE ビットが設定されると、次のことが示されます。

-   同じシーンがレンダリングされている間に、アプリケーションからのフルシーンのアンチエイリアシングを有効または無効にする要求に失敗します。 つまり、1つのシーンのレンダリング中に、D3DRS\_MULTISAMPLEANTIALIAS デバイスのレンダリング状態 (D3DRENDERSTATETYPE) の**ブール**値をオンまたはオフにする要求は失敗します。 D3DRS\_MULTISAMPLEANTIALIAS エイリアシングの**ブール**値を変更する要求は、別のシーンでは失敗しないように注意してください。 つまり、1つのシーンで D3DRS\_MULTISAMPLEANTIALIAS エイリアスが**TRUE**の場合、別のシーンでは**FALSE**になる可能性があります。

-   は、マルチサンプリングレンダーターゲットのサンプルを変更するために、アプリケーションからの要求に応答しません。 つまり、D3DRS\_MULTISAMPLEMASK デバイスのレンダリング状態 (D3DRENDERSTATETYPE) のビットマスクの設定には応答しません。

ドライバーは、ストレッチ blt を使用して全画面表示モードでページフリップを実行する場合、サポートされるサンプル数を、 [**DdwFlipMSTypes 形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)の**MultiSampleCaps**構造体のメンバーで指定する必要があることに注意してください。また、 **wBltMSTypes**メンバーがフリップとして実行されているわけではありません。

 

 





