---
title: デインター レース、フレーム レートの変換
description: デインター レース、フレーム レートの変換
ms.assetid: 73435a68-532a-4a15-b2b9-a6165cadb8fe
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、フレーム レートの変換
- ビデオ アクセラレータ WDK DirectX、フレーム レートの変換
- VA WDK DirectX、フレーム レートの変換
- デインター レース、DirectX ビデオ アクセラレータ WDK Windows 2000 を表示します。
- ビデオの高速化 WDK DirectX デインター レース
- VA WDK の DirectX デインター レース
- WDK DirectX VA デインター レース
- フレーム レート変換 WDK DirectX VA
- デインター レースについて WDK DirectX va なので、インター レースを解除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e31311751b166968cf89e08fb39eac0c4be0e425
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530400"
---
# <a name="deinterlacing-and-frame-rate-conversion"></a>デインター レース、フレーム レートの変換


## <span id="ddk_deinterlacing_and_frame_rate_conversion_gg"></span><span id="DDK_DEINTERLACING_AND_FRAME_RATE_CONVERSION_GG"></span>


DirectDraw とグラフィックス デバイス ドライバーの間の DDI DirectDraw DDI と Direct3D DDI のカーネル モードの部分を使用してビデオのコンテンツのデインター レース、フレーム レートの変換をサポートする DirectX VA を拡張します。 ノンインター レース化し、フレーム レート変換インターフェイスは、すべてのビデオ プレゼンテーション メカニズム依存しません。

デインター レースまたはフレーム レート変換プロセスの出力は、累進フレームでは常にします。

このインターフェイスを使用するには、次の要件を満たす必要があります。

-   Deinterlaced の出力は、ターゲットの DirectDraw surface に物理的に存在する必要があります。 この要件は、すべてのハードウェア オーバーレイ ソリューションをできません。

-   グラフィックス エンジンおよびハードウェアのオーバーレイ、存在する場合は、最低の bob と機能をデインター レース weave をサポートする必要があります。

-   この DDI は、Microsoft Windows XP SP1 以降のバージョンに適用されます。

このセクションでは、次のトピックについて説明します。

[インター レース モードを解除します。](deinterlace-modes.md)

[フレーム レート変換モード](frame-rate-conversion-modes.md)

[Bob デインター レース](bob-deinterlacing.md)

[マッピング、DirectDraw を DirectX VA DDI インター レースを解除](mapping-the-deinterlace-ddi-to-directdraw-and-directx-va.md)

[ビデオ コンテンツのインターとフレーム レートの変換](video-content-for-deinterlace-and-frame-rate-conversion.md)

[64 ビット オペレーティング システムでデインター レース](deinterlacing-on-64-bit-operating-systems.md)

[結合がデインター レース、ビデオ サブストリーム合成](combining-deinterlacing-and-video-substream-compositing.md)

[デインター レースのサンプル関数](sample-functions-for-deinterlacing.md)

 

 





