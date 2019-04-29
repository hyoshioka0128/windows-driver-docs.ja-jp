---
title: waveOut クライアントの詳細
description: waveOut クライアントの詳細
ms.assetid: e2cfc59a-0c36-4b57-99e2-b7bed503bc12
keywords:
- waveOut 非 PCM wave 形式の WDK オーディオ
- 非 PCM オーディオ形式 WDK、waveOut
- ループの PCM 以外の形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4794a7f81cd145a3c3f12af06fe23c545fecbca7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335405"
---
# <a name="specifics-for-waveout-clients"></a>waveOut クライアントの詳細


## <span id="specifics_for_waveout_clients"></span><span id="SPECIFICS_FOR_WAVEOUT_CLIENTS"></span>


呼び出し[ **waveOutOpen** ](https://msdn.microsoft.com/library/windows/desktop/dd743866)返します WAVERR\_BADFORMAT ドライバーは、指定した wave 形式をサポートしていない場合。

Microsoft Windows では、PCM 以外の形式で wave ヘッダーのループを現在はサポートしていません。 PCM 以外の形式をループする試行が失敗するが、システムはアーキテクチャ上の制約によりヘッダー (いないヘッダー-準備) を提出段階まで、障害を検出できませんしません。 呼び出しでは具体的には、 [ **waveOutPrepareHeader** ](https://msdn.microsoft.com/library/windows/desktop/dd743868) WHDR で非 PCM wave ヘッダーを受け取る可能性\_BEGINLOOP や WHDR\_ENDLOOP 設定**dwFlags**、後続の呼び出しが、 [ **waveOutWrite** ](https://msdn.microsoft.com/library/windows/desktop/dd743876)失敗し、返します MMSYSERR\_INVALPARAM します。 場合 WHDR\_BEGINLOOP と WHDR\_ENDLOOP 設定されていない**dwFlags**、ただし、指定する**dwLoops**&gt;1 は発生しません**waveOutWrite**が失敗します。

再生時に PCM 以外のデータは、呼び出しを[ **waveOutBreakLoop** ](https://msdn.microsoft.com/library/windows/desktop/dd743854) MMSYSERR、リターン コードが失敗した\_INVALPARAM します。

 

 




