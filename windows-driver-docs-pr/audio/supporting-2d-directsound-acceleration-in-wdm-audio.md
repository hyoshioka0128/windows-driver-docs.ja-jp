---
title: WDM オーディオでの 2D DirectSound アクセラレータのサポート
description: WDM オーディオでの 2D DirectSound アクセラレータのサポート
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- ハードウェア アクセラレータ WDK DirectSound、2D の混在
- WDK のオーディオを混在させる 2D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a86d410b927d26440d22192694ece5e2642918c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354250"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>WDM オーディオでの 2D DirectSound アクセラレータのサポート


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound は、次の要件を満たしている WDM オーディオ ミニポート ドライバーの 2D ミキシングをハードウェア アクセラレータによる公開しています。

-   ミニポート ドライバーには、IRP シンクは、暗証番号 (pin) ファクトリが含まれています (KSPIN\_通信\_シンク) が、 [ **KSPIN\_データフロー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow) KSPINの方向\_データフロー\_IN、データ範囲を公開して ([**KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体) を指定子 (**DataFormat**.**指定子**メンバー) KSDATAFORMAT に設定されている\_指定子\_DSOUND します。

-   ピン留めするファクトリの[ **KSPROPERTY\_PIN\_CINSTANCES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-cinstances)ハンドラーのセット、 **PossibleCount**のメンバー、 **KSPIN\_CINSTANCES**構造体の 2 つ以上の値を (最初の pin が KMixer は確保されます)。 **PossibleCount**値を現在 pin ファクトリからインスタンス化する暗証番号 (pin) のインスタンスの数を指定します。

-   ピン留めするファクトリをサポートする必要があります、 [ **KSPROPERTY\_オーディオ\_CPU\_リソース**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-cpu-resources)プロパティおよび KSAUDIO をレポートする必要があります\_CPU\_リソース\_いない\_ホスト\_ハードウェアであるすべてのノードの cpu 使用率が高速です。

-   Pin が満たす必要があります、 [DirectSound ノード順序要件](directsound-node-ordering-requirements.md)します。

 

 




