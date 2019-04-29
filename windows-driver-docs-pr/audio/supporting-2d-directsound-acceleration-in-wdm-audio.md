---
title: WDM オーディオでの 2D DirectSound アクセラレータのサポート
description: WDM オーディオでの 2D DirectSound アクセラレータのサポート
ms.assetid: dbbb2416-8928-41ee-90d5-b3b77d23c251
keywords:
- ハードウェア アクセラレータ WDK DirectSound、2D の混在
- WDK のオーディオを混在させる 2D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a133cbaff37eb72dbdd6f7333c6f47d44bbcd6dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328585"
---
# <a name="supporting-2d-directsound-acceleration-in-wdm-audio"></a>WDM オーディオでの 2D DirectSound アクセラレータのサポート


## <span id="supporting_2d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_2D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound は、次の要件を満たしている WDM オーディオ ミニポート ドライバーの 2D ミキシングをハードウェア アクセラレータによる公開しています。

-   ミニポート ドライバーには、IRP シンクは、暗証番号 (pin) ファクトリが含まれています (KSPIN\_通信\_シンク) が、 [ **KSPIN\_データフロー** ](https://msdn.microsoft.com/library/windows/hardware/ff563532) KSPINの方向\_データフロー\_IN、データ範囲を公開して ([**KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096)構造体) を指定子 (**DataFormat**.**指定子**メンバー) KSDATAFORMAT に設定されている\_指定子\_DSOUND します。

-   ピン留めするファクトリの[ **KSPROPERTY\_PIN\_CINSTANCES** ](https://msdn.microsoft.com/library/windows/hardware/ff565193)ハンドラーのセット、 **PossibleCount**のメンバー、 **KSPIN\_CINSTANCES**構造体の 2 つ以上の値を (最初の pin が KMixer は確保されます)。 **PossibleCount**値を現在 pin ファクトリからインスタンス化する暗証番号 (pin) のインスタンスの数を指定します。

-   ピン留めするファクトリをサポートする必要があります、 [ **KSPROPERTY\_オーディオ\_CPU\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537255)プロパティおよび KSAUDIO をレポートする必要があります\_CPU\_リソース\_いない\_ホスト\_ハードウェアであるすべてのノードの cpu 使用率が高速です。

-   Pin が満たす必要があります、 [DirectSound ノード順序要件](directsound-node-ordering-requirements.md)します。

 

 




