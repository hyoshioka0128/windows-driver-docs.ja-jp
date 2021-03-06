---
title: StretchBlt を介したマルチサンプル サポート
description: StretchBlt を介したマルチサンプル サポート
ms.assetid: c829c612-d09d-4a33-a117-e50b9ed57251
keywords:
- WDK の Windows 2000 の表示、表示、マルチ サンプリング StretchBlt の DirectX 8.0 リリース ノートします。
- マルチ サンプリング レンダリング WDK DirectX 8.0、StretchBlt
- multisamples WDK DirectX 8.0、StretchBlt のレンダリング
- blit 操作 WDK DirectX 8.0 を拡大します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d80d7c367eca695ff362422ae755409d7818a89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372819"
---
# <a name="multisample-support-through-stretchblt"></a>StretchBlt を介したマルチサンプル サポート


## <span id="ddk_multisample_support_through_stretchblt_gg"></span><span id="DDK_MULTISAMPLE_SUPPORT_THROUGH_STRETCHBLT_GG"></span>


ない、推奨されるメカニズムのマルチ サンプリングをサポートするため、ドライバーは大きなバック バッファーへのレンダリングでサンプリング サポートを実装することができ、プライマリの低解像度の大規模なバックアップをリサンプル blt バッファーの stretch を実行します。 ただし、ドライバーでのマルチ サンプリングをサポートするメカニズムの場合は、ドライバー設定があります、新しい機能ビット D3DPRASTERCAPS\_で STRETCHBLTMULTISAMPLE、 **RasterCaps** D3D8CAPS 構造体のメンバー。 D3DCAPS8 の説明は、DirectX 8.0 SDK ドキュメントを参照してください。

ドライバーが、D3DPRASTERCAPS を設定するときに\_STRETCHBLTMULTISAMPLE ビット、ことを示します。

-   同じシーンがレンダリングされるときに、完全なシーンのアンチエイリアシングを無効にするアプリケーションからの要求は失敗します。 つまり、オンとオフをへの要求が失敗した、 **BOOL** 、D3DRS の値\_MULTISAMPLEANTIALIAS デバイスは、1 つのシーンのレンダリング中に (D3DRENDERSTATETYPE) の状態を表示します。 変更を要求に注意してください、 **BOOL** D3DRS @property\_MULTISAMPLEANTIALIAS が異なるシーンの失敗しない必要があります。 つまり場合、D3DRS\_MULTISAMPLEANTIALIAS は**TRUE**可能性があります、1 つのシーンの**FALSE**もう 1 つのシーンの。

-   応答していない要求をマルチ サンプリングのレンダー ターゲットのサンプルを変更するアプリケーションです。 つまり、応答しない、D3DRS のビットマスクを設定する\_MULTISAMPLEMASK デバイス (D3DRENDERSTATETYPE) の状態を表示します。

ドライバーは、stretch を使用している場合に注意する必要が全画面表示モードでページを実行する blt が反転、ドライバーがサポートされているサンプル カウントを指定する必要があります、 **wFlipMSTypes**のメンバー、 [ **DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ddpixelformat)の**MultiSampleCaps**構造および not、 **wBltMSTypes**反転するとメンバーが実行されています。

 

 





