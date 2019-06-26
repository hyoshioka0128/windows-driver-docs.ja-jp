---
title: 専用のスピーカー構成ユーティリティ
description: 専用のスピーカー構成ユーティリティ
ms.assetid: d04b8c1b-13c6-422f-b13a-909f7074ac75
keywords:
- 専用のスピーカー構成ユーティリティの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f5190c13ad3a5445aad6d93f24168d749e8482
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362529"
---
# <a name="proprietary-speaker-configuration-utilities"></a>専用のスピーカー構成ユーティリティ


## <span id="proprietary_speaker_configuration_utilities"></span><span id="PROPRIETARY_SPEAKER_CONFIGURATION_UTILITIES"></span>


**注**  この情報は、Windows XP およびそれ以前のオペレーティング システムに適用されます。 以降、Windows Vista で**IDirectSound::GetSpeakerConfig**と**IDirectSound::SetSpeakerConfig**非推奨とされました。

 

場合によっては、ハードウェア ベンダーは、コントロール パネルの [スピーカー] ダイアログの代わりに、オーディオ ドライバーで使用する専用のスピーカー構成ユーティリティを提供します。 このようなユーティリティがある潜在的な問題: スピーカーの構成の変更の Windows の通知に失敗した独自の方法が変更ができます。 コントロール パネルにある独自のユーティリティの設定が一致しない場合は、不適切なユーザー エクスペリエンスをこれがあります。 デバイスが、独自のユーティリティが必要であると思われる場合、ユーティリティを Windows に統合するには、次の手順を行う必要があります。

1.  ドライバーをサポートする DAC のノードを実装、 [ **KSPROPERTY\_オーディオ\_チャネル\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-channel-config)プロパティ。 このノードからは、Windows は、コントロール パネルの ユーザーによって行われた変更のすぐにドライバーを通知します。

2.  DirectSound メソッドを呼び出して、スピーカーの構成を管理するには、構成ユーティリティを設計**GetSpeakerConfig**と**SetSpeakerConfig**します。

**SetSpeakerConfig** DirectSound (および Windows) のユーティリティがスピーカーの構成に加える変更の呼び出しが通知されます。 また、ユーティリティの初期化コードを呼び出す必要があります**GetSpeakerConfig**をユーザーがコントロール パネルからすべての設定を変更したかどうかを判断します。 そうである場合、ユーティリティは、ユーザー インターフェイスでこれらの変更を反映する必要があります。

デバイスは、Windows の正確な等価を持たないマルチ チャネルの形式をサポートする場合、構成ユーティリティでは、以下を実行します。

-   Windows と同等の正確なを持たないスピーカーの構成を変更するときに呼び出す**SetSpeakerConfig**最も近い Windows と等価です。 これは、ドライバーを構成するために必要な独自の呼び出しを行うだけでなくします。

-   Windows に相当する正確なスピーカーの構成を変更すると、ときに呼び出す**SetSpeakerConfig**スピーカー モードを更新します。

Windows をデバイスの機能について理解した場合、DirectSound は、それ以外の場合有効にできませんいくつかの機能を有効にできます (たとえば、マルチ チャンネル 3D パン)。

 

 




