---
title: StretchBlt を通じて multisample のサポート
description: StretchBlt を通じて multisample のサポート
ms.assetid: c829c612-d09d-4a33-a117-e50b9ed57251
keywords:
- WDK の Windows 2000 の表示、表示、マルチ サンプリング StretchBlt の DirectX 8.0 リリース ノートします。
- マルチ サンプリング レンダリング WDK DirectX 8.0、StretchBlt
- multisamples WDK DirectX 8.0、StretchBlt のレンダリング
- blit 操作 WDK DirectX 8.0 を拡大します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b43d65a06e4bf45f3830e13b3bdd789fef8f41a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552458"
---
# <a name="multisample-support-through-stretchblt"></a>StretchBlt を通じて multisample のサポート


## <span id="ddk_multisample_support_through_stretchblt_gg"></span><span id="DDK_MULTISAMPLE_SUPPORT_THROUGH_STRETCHBLT_GG"></span>


ない、推奨されるメカニズムのマルチ サンプリングをサポートするため、ドライバーは大きなバック バッファーへのレンダリングでサンプリング サポートを実装することができ、プライマリの低解像度の大規模なバックアップをリサンプル blt バッファーの stretch を実行します。 ただし、ドライバーでのマルチ サンプリングをサポートするメカニズムの場合は、ドライバー設定があります、新しい機能ビット D3DPRASTERCAPS\_で STRETCHBLTMULTISAMPLE、 **RasterCaps** D3D8CAPS 構造体のメンバー。 D3DCAPS8 の説明は、DirectX 8.0 SDK ドキュメントを参照してください。

ドライバーが、D3DPRASTERCAPS を設定するときに\_STRETCHBLTMULTISAMPLE ビット、ことを示します。

-   同じシーンがレンダリングされるときに、完全なシーンのアンチエイリアシングを無効にするアプリケーションからの要求は失敗します。 つまり、オンとオフをへの要求が失敗した、 **BOOL** 、D3DRS の値\_MULTISAMPLEANTIALIAS デバイスは、1 つのシーンのレンダリング中に (D3DRENDERSTATETYPE) の状態を表示します。 変更を要求に注意してください、 **BOOL** D3DRS @property\_MULTISAMPLEANTIALIAS が異なるシーンの失敗しない必要があります。 つまり場合、D3DRS\_MULTISAMPLEANTIALIAS は**TRUE**可能性があります、1 つのシーンの**FALSE**もう 1 つのシーンの。

-   応答していない要求をマルチ サンプリングのレンダー ターゲットのサンプルを変更するアプリケーションです。 つまり、応答しない、D3DRS のビットマスクを設定する\_MULTISAMPLEMASK デバイス (D3DRENDERSTATETYPE) の状態を表示します。

ドライバーは、stretch を使用している場合に注意する必要が全画面表示モードでページを実行する blt が反転、ドライバーがサポートされているサンプル カウントを指定する必要があります、 **wFlipMSTypes**のメンバー、 [ **DDPIXELFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff550274)の**MultiSampleCaps**構造および not、 **wBltMSTypes**反転するとメンバーが実行されています。

 

 





