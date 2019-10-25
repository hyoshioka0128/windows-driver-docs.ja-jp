---
title: DRM ドライバーの開発とデバッグ
description: DRM ドライバーの開発とデバッグ
ms.assetid: 3450717a-fd27-4bea-8740-9d47b420ed32
keywords:
- デジタル Rights Management WDK audio、推奨事項
- DRM WDK オーディオ、推奨事項
- Digital Rights Management WDK audio、デバッグ
- DRM WDK オーディオ、デバッグ
- ドライバーのデバッグ WDK DRM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 244e29be2295b633314a8f0aad0853c1507eff82
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833555"
---
# <a name="developing-and-debugging-drm-drivers"></a>DRM ドライバーの開発とデバッグ


## <span id="developing_and_debugging_drm_drivers"></span><span id="DEVELOPING_AND_DEBUGGING_DRM_DRIVERS"></span>


次のチェックリストは、ドライバーの作成者がよくある落とし穴を回避するのに役立つ場合があります。

-   DRM で保護されたコンテンツの再生中に、ドライバーが wave out capture と S/PDIF の出力を無効にした場合、DRM で保護されたコンテンツの再生が終了した後に、ドライバーはその内容を再度有効にする必要があります (および DRM バッファーが破棄されます)。

-   デバイスがハードウェアミックスを実行する場合、ドライバーは、ミックスに対してストリームが追加または削除されるときに発生する複合使用権限の変更を追跡する必要があります。 ミックスにコピーによって保護された DRM ストリームが1つ以上含まれている場合は、キャプチャをミュートにする必要があります。 保護ミックスの再生中にキャプチャが有効になっている場合は、ミュート状態のままにしておく必要があります。

-   フィルターグラフに変更を行った後、またはストリームに関連付けられているプロパティ設定を変更した後、ドライバーはストリームのコピー防止設定と出力有効化設定をすぐに更新することが必要になる場合があります。 ドライバーは、保護されたコンテンツがキャプチャバッファーまたはデジタル出力にコピーされるのを防ぐために、操作を同期する必要があります。 たとえば、キャプチャマルチプレクサーへの入力ストリームが変更された場合、ドライバーは、ミュートをオンまたはオフにするために必要な時間に、セキュリティで保護されたコンテンツが脆弱になることを許可しないようにする必要があります。

[Drmk システムドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)は、DRM で保護されたコンテンツの再生中に、カーネルデバッガーが接続できないようにします。 アンチデバッグ防御は、DRMK が保護されたコンテンツを不透明にするために使用するいくつかの手段の1つです。 ただし、ドライバーをテストする準備ができたら、次の方法を使用して、DRM に準拠した機能をデバッグできます。

-   Wave ストリームの**SetState**メソッドを一時的に変更します (たとえば、 [**IMiniportWavePciStream:: SetState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setstate)を参照)。 [**IDrmAudioStream:: SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)を呼び出し、 [**drmrights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)パラメーターの**copyprotect**メンバーをに設定します。**TRUE**。

-   デバッグが完了したら、忘れずに**SetContentId**呼び出しを削除してください。

この手法では、保護されていないコンテンツを DRM で保護されたコンテンツとして再生できますが、デバッガーを無効にすることは避けてください。

たとえば、デバッガーを使用して、ドライバーによってコンテンツの記録が禁止されていることを確認できます。 SndVol32 プログラムのボリュームとミュートの設定を変更することで、このドライバーを使用して、capture MUX 経由での wave out ストリームの記録を有効にします。 スライダーには、設定に加えた変更が反映されている必要がありますが、それは永続的ですが、capture MUX は、"保護された" コンテンツの再生が終了するまで、wave out ストリームをミュートし続ける必要があります。 その後、新しい設定を有効にする必要があります。

 

 




