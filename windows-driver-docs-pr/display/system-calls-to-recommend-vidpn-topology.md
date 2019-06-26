---
title: 推奨される VidPN トポロジへのシステム コール
description: 推奨される VidPN トポロジへのシステム コール
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d214f6f60699a32b97bb9aeb6ca10a689eb1ffae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372040"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>推奨される VidPN トポロジへのシステム コール


Windows 7 を実行するコンピューターでは、表示モード マネージャー (DMM) は、適用 CCD データベースで VidPN 履歴データを使用する適切な VidPN トポロジを決定します。 不要になった DMM は、Windows vista と同様に、最後の既知の適切なトポロジに基づいて VidPN トポロジを決定します。 その結果、Windows 7 DMM で呼び出すことはありません、 [ **DxgkDdiRecommendVidPnTopology** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendvidpntopology)関数。

Windows Vista およびそのサービス パック、DMM の継続を呼び出す*DxgkDdiRecommendVidPnTopology*ドライバーが推奨される機能 VidPN トポロジを提供することを要求します。

 

 





