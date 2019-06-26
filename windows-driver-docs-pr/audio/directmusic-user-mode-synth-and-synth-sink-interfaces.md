---
title: シンセサイザーおよびシンセサイザー シンクの DirectMusic ユーザー モード インターフェイス
description: シンセサイザーおよびシンセサイザー シンクの DirectMusic ユーザー モード インターフェイス
ms.assetid: 2b25f605-d9e6-415e-8f45-08f7cdd2f625
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c785d71d82567de741aacc2e74edd40a90b0ba6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356545"
---
# <a name="directmusic-user-mode-synth-and-synth-sink-interfaces"></a>シンセサイザーおよびシンセサイザー シンクの DirectMusic ユーザー モード インターフェイス


## <span id="ddk_directmusic_user_mode_synth_and_synth_sink_interfaces_ks"></span><span id="DDK_DIRECTMUSIC_USER_MODE_SYNTH_AND_SYNTH_SINK_INTERFACES_KS"></span>


このセクションでは、ユーザー モードおよびインターフェイスをシンセサイザー シンセサイザー シンク DirectMusic について説明します。 」の説明に従って[ユーザー モードとカーネル モード](https://docs.microsoft.com/windows-hardware/drivers/audio/user-mode-versus-kernel-mode)、これらのインターフェイスは、カーネル モードに後で移植できるユーザー モードでのドライバー コードの開発に役立ちます。 詳しくは、次を参照してください。[シンセサイザーと Wave シンク](https://docs.microsoft.com/windows-hardware/drivers/audio/synthesizers-and-wave-sinks)します。

このセクションでは、次の 2 つのユーザー モード インターフェイスが表示されます。

ユーザー モードのシンセサイザーのインターフェイス

ユーザー モードのシンセサイザー シンクのインターフェイス

[IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)

[IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)

 

 





