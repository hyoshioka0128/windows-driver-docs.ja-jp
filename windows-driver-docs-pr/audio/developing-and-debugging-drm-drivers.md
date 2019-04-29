---
title: DRM ドライバーの開発とデバッグ
description: DRM ドライバーの開発とデバッグ
ms.assetid: 3450717a-fd27-4bea-8740-9d47b420ed32
keywords:
- デジタル権利管理の WDK オーディオ、推奨事項
- DRM WDK オーディオ、推奨事項
- デジタル権利管理の WDK オーディオでは、デバッグ
- DRM WDK オーディオ、デバッグ
- ドライバー WDK DRM のデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d05032f85e6b2de8e81f145a41a92dd6c37d304
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333805"
---
# <a name="developing-and-debugging-drm-drivers"></a>DRM ドライバーの開発とデバッグ


## <span id="developing_and_debugging_drm_drivers"></span><span id="DEVELOPING_AND_DEBUGGING_DRM_DRIVERS"></span>


次のチェックリストは、ドライバー作成者がいくつかのよくある落とし穴の回避に役立つ場合があります。

-   ドライバーは、wave アウト キャプチャと S/PDIF 出力 DRM で保護されたコンテンツの再生中に無効化、DRM で保護されたコンテンツの再生が終了する (および DRM バッファーが破棄される) 後にもう一度有効にするドライバーは注意してください。

-   デバイスは、ハードウェアの混在を実行する場合、ドライバーする必要がありますの追跡でストリームを追加するときに発生する、または組み合わせから削除された複合使用権限の変更。 ミックスには、1 つまたは複数のコピーで保護されている DRM ストリームが含まれています。 いつでもなど、キャプチャする必要がありますはミュートにします。 保護されている組み合わせの再生中に、キャプチャがオンの場合はミュートにおきます。

-   フィルターのグラフまたはストリームに関連付けられているプロパティの設定を変更した後、ドライバーをすぐに更新して、ストリームのコピー防止設定の出力を有効に必要があります。 ドライバーは、保護されたコンテンツが、キャプチャ バッファーまたはデジタルの出力にコピーされていることを防ぐためには、その操作を同期する必要があります。 たとえば、キャプチャ マルチプレクサーの変更を入力ストリーム、ドライバーする必要がありますが許容されない場合を受けるミュートのオンとオフを必要な時間中にセキュリティで保護されたコンテンツ。

[DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver) DRM で保護されたコンテンツを再生中に、接続から、カーネル デバッガーを防止します。 アンチ デバッグ防御では、DRMK を使用して保護されたコンテンツを不透明な複数のメジャーの 1 つです。 後、ドライバーをテストする準備ができたら、ただし、次の手法を使用して、DRM 準拠の機能をデバッグできます。

-   Wave ストリームを一時的に変更**SetState**メソッド (たとえばを参照してください[ **IMiniportWavePciStream::SetState**](https://msdn.microsoft.com/library/windows/hardware/ff536733)) を呼び出す[ **IDrmAudioStream::SetContentId** ](https://msdn.microsoft.com/library/windows/hardware/ff536570)設定と、 [ **DRMRIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff536355)パラメーターの**CopyProtect** メンバー**TRUE**します。

-   デバッグが完了したら、忘れずに削除してください、 **SetContentId**呼び出します。

この手法では、DRM で保護されたコンテンツと同様に、保護されていないコンテンツを再生できますが、デバッガーを無効にしません。

たとえば、デバッガーを使用するには、ドライバーから記録されている内容によって禁止されていることを確認します。 ドライバーをだまして SndVol32 プログラムのボリュームを変更することで、キャプチャ MUX を通じて wave アウト ストリームの記録を有効にすると、ミュート設定します。 スライダーは永続的で、その設定が「保護」のコンテンツの再生が終了するまで、wave アウト ストリームをミュートする MUX を続行するキャプチャに加えた変更を反映する必要があります。 その後で新しい設定が有効になります。

 

 




