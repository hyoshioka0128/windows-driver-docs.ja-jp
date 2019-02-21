---
title: WDM オーディオで 3D DirectSound アクセラレータのサポート
description: WDM オーディオで 3D DirectSound アクセラレータのサポート
ms.assetid: 7524c15a-e487-43b6-9101-7cdd0c5e6e0c
keywords:
- ハードウェア アクセラレータ WDK DirectSound、3 D の混在
- オーディオの WDK ミキシング 3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b464925a387ce6fc4021d82123863349779f6fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535839"
---
# <a name="supporting-3d-directsound-acceleration-in-wdm-audio"></a>WDM オーディオで 3D DirectSound アクセラレータのサポート


## <span id="supporting_3d_directsound_acceleration_in_wdm_audio"></span><span id="SUPPORTING_3D_DIRECTSOUND_ACCELERATION_IN_WDM_AUDIO"></span>


DirectSound は、次の要件を満たしている WDM オーディオ ミニポート ドライバーの 3D ミキシングをハードウェア アクセラレータによるを公開します。

-   Pin に一覧された要件を満たす必要があります[WDM オーディオでは 2D DirectSound アクセラレーションをサポートしている](supporting-2d-directsound-acceleration-in-wdm-audio.md)します。

-   Pin が 3D のノードを含める必要があります ([**KSNODETYPE\_3D\_効果**](https://msdn.microsoft.com/library/windows/hardware/ff537148)) のノードのチェーンにします。 (を参照してください[DirectSound ノード順序要件](directsound-node-ordering-requirements.md))。

-   Pin をサポートする必要があります、 [KSPROPSETID\_DirectSound3DBuffer](https://msdn.microsoft.com/library/windows/hardware/ff537447) 3D のノードのプロパティで設定します。

-   Pin をサポートする必要があります、 [KSPROPSETID\_DirectSound3DListener](https://msdn.microsoft.com/library/windows/hardware/ff537449) 3D のノードのプロパティで設定します。

 

 




