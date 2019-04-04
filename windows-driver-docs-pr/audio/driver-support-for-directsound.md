---
title: DirectSound のドライバー サポート
description: DirectSound のドライバー サポート
ms.assetid: a32a2a01-4ecd-485f-8293-402a0bcc8336
keywords:
- WDM オーディオ ドライバー WDK、DirectSound
- オーディオ ドライバー WDK、DirectSound
- DirectSound WDK オーディオ
- DirectSound WDK オーディオ、DirectSound について
- ミニポート ドライバー WDK オーディオ、DirectSound
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c198d4efb067dfeccfed6519e4a08fd653a5fc1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532130"
---
# <a name="driver-support-for-directsound"></a>DirectSound のドライバー サポート


## <span id="driver_support_for_directsound"></span><span id="DRIVER_SUPPORT_FOR_DIRECTSOUND"></span>


WDM のオーディオ システムでは、オーディオ デバイスを Microsoft DirectSound API を通じてアクセスされるアプリケーション プログラムのドライバーのサポートを提供します。 DirectSound ドライバーのサポートを提供するシステム コンポーネントの説明は、[WDM オーディオ コンポーネント](wdm-audio-components.md)を参照してください。

次のセクションでは、オーディオのミニポート ドライバーを実装できるサポートを強化するアプリケーションのプログラム、DirectSound の API を公開するオーディオ機能機能について説明します。 これらの機能は、2 D および 3D サウンド効果、さまざまなスピーカーの構成のサポートのハードウェア アクセラレータを含めるし、アコースティック エコー キャンセルの全二重電話会議などの効果をキャプチャします。

このセクションでは、次のトピックが表示されます。

[WDM オーディオでは DirectSound ハードウェア高速化](directsound-hardware-acceleration-in-wdm-audio.md)

[DirectSound スピーカー構成の設定](directsound-speaker-configuration-settings.md)

[DirectSound キャプチャ効果](directsound-capture-effects.md)

 

 




