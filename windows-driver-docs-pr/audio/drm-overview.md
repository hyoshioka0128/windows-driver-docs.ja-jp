---
title: DRM の概要
description: DRM の概要
ms.assetid: 81f47eca-aa8a-43c4-96c9-7446cba50d00
keywords:
- DRM について、digital Rights Management の WDK オーディオ
- DRM WDK オーディオ、DRM について
- DRMK システム ドライバー WDK オーディオ
- WDK のオーディオを復号化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b39c7b3b3f7e7d1dda56ac4385f80efc4c54abd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333725"
---
# <a name="drm-overview"></a>DRM の概要


## <span id="drm_overview"></span><span id="DRM_OVERVIEW"></span>


Microsoft Windows 2000 以降、デジタル オーディオの DRM を実装し、Windows Me/98 です。 ただし、Microsoft Windows XP のみ以降では、および Windows Me、カーネル内での DRM セキュリティを実装します。 現時点では、Windows では、DRM セキュリティ MIDI ストリームまたは DLS セットはありません。

DRM で保護されたデジタル コンテンツがディスク上の暗号化された形式で格納されている、またはその他のストレージ メディアの種類します。 暗号化アルゴリズム、暗号化が解除されるまで判読できないようにする内容にスクランブルをかけます。 再生中に、コンテンツは、ディスクからの読み取りおよびメモリにバッファリングされるスクランブルにします。 データ パスの末尾付近の[DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver) (Drmk.sys) データを解読し、フィードを再生するオーディオ ドライバーに直接します。 Unscrambled コンテンツを転送するデータ パスの範囲を制限すると、DRMK 受けやすくなりますコンテンツ小さい無断でコピーします。

セキュリティ抜け穴では Windows 2000 および Windows 98 で、簡単に暗号化されていない形式でディスクにセキュリティで保護されたコンテンツの再生をルーティングする悪意のあるドライバーを読み込むができます。 Windows XP 以降では、および Windows Me、DRM で保護されたコンテンツを再生するオーディオ ドライバーを信頼できるのみ許可することでこの抜け穴を閉じます。

Windows XP 以降では、および Windows Me、スクランブル カーネルの保護された環境になるまで、オーディオ データ パスを通過するときにコンテンツが変更をセキュリティで保護します。 、カーネル内で保護されたコンポーネント、データを解読され unscrambled データを再生用のドライバーを信頼済みにフィードされます。 Unscrambled のオーディオ ストリームを再生するフィルター グラフを構成するときに、DRMK はグラフに配置された各 KS フィルター ドライバーを認証します。 システムは保護されたコンテンツの使用に関する規則のドライバーに通知します。 ドライバーには、さらに、DRMK、ダウン ストリームのフィルター、コンテンツ ルーティングし、もこれらのフィルターがシステムによって認証を行うが表示されます。 このプロセスは、グラフが完了するまで続きます。 システムは、デジタル再生ストリームは、DRM 準拠していない、任意のコンポーネントを通過する場合に、グラフ全体を拒否します。

DRM 準拠のドライバーでは、デジタル コンテンツの再生中に不正コピーを防ぐ必要があります。 さらに、ドライバーを復号化されたコンテンツをキャプチャできます (S/PDIF) などの標準インターフェイスを介してコンテンツを転送できるすべてのデジタル出力を無効にする必要があります。 この要件は、USB デバイスに適用されないことに注意してください。 現時点では、DRMK はデジタル出力はありませんで USB スピーカー デバイスからのみで保護されたコンテンツを再生します。

 

 




