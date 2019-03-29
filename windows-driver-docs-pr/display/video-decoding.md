---
title: ビデオ デコード
description: ビデオ デコード
ms.assetid: 4e8bf7e9-7a3c-4732-9ac0-4f6f5ef07552
keywords:
- DirectX のビデオ アクセラレータ WDK Windows 2000 の表示、ビデオのデコード
- ビデオ アクセラレータの WDK DirectX のビデオのデコード
- VA WDK DirectX、ビデオのデコード
- ビデオのデコードについての詳細の va なので、ビデオの WDK DirectX のデコード
- ビデオのビデオをデコードについての詳細の WDK DirectX va なのでのデコード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed668d18e83876a0e7d695e5b240db0e2452e559
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581768"
---
# <a name="video-decoding"></a>ビデオ デコード


## <span id="ddk_video_decoding_gg"></span><span id="DDK_VIDEO_DECODING_GG"></span>


DirectX VA により、デコード処理の間で分割するビデオの 1 つまたは複数の段階、*ホスト CPU*とビデオ ハードウェア アクセラレータ。 実行される、[動き補償予測](motion-compensated-prediction.md)(MCP) 逆コサイン不連続変換 (IDCT) とデコードの処理の可変長のデコード (VLD) ステージも実行され、します。

DirectX の VA API は、1 つのビデオ ストリームをデコードします。 複数のビデオ ストリームのサポートには、各ビデオ ストリーム (出力および入力ピンがグラフの操作をフィルターで使用するには、ビデオ デコーダーとの高速化のドライバーの独立したペアなど) の別の DirectX VA セッションが必要です。 フィルターのグラフの詳細については、次を参照してください。 [KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)します。

 

 





