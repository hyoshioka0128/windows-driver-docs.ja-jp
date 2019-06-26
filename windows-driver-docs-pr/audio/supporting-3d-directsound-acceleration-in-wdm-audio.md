---
title: WDM オーディオでの 3D DirectSound アクセラレータのサポート
description: WDM オーディオでの 3D DirectSound アクセラレータのサポート
ms.assetid: 7524c15a-e487-43b6-9101-7cdd0c5e6e0c
keywords:
- ハードウェア アクセラレータ WDK DirectSound、3 D の混在
- オーディオの WDK ミキシング 3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00e8ceea90b7919591ae721ce8be3312a737ea7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354239"
---
# <a name="supporting-3d-directsound-acceleration-in-wdm-audio"></a>WDM オーディオでの 3D DirectSound アクセラレータのサポート


## <span id="supporting_3d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_3D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound は、次の要件を満たしている WDM オーディオ ミニポート ドライバーの 3D ミキシングをハードウェア アクセラレータによるを公開します。

-   Pin に一覧された要件を満たす必要があります[WDM オーディオでは 2D DirectSound アクセラレーションをサポートしている](supporting-2d-directsound-acceleration-in-wdm-audio.md)します。

-   Pin が 3D のノードを含める必要があります ([**KSNODETYPE\_3D\_効果**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-3d-effects)) のノードのチェーンにします。 (を参照してください[DirectSound ノード順序要件](directsound-node-ordering-requirements.md))。

-   Pin をサポートする必要があります、 [KSPROPSETID\_DirectSound3DBuffer](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-directsound3dbuffer) 3D のノードのプロパティで設定します。

-   Pin をサポートする必要があります、 [KSPROPSETID\_DirectSound3DListener](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-directsound3dlistener) 3D のノードのプロパティで設定します。

 

 




