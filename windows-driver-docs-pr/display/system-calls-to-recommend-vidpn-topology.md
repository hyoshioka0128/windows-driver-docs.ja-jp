---
title: 推奨される VidPN トポロジへのシステム コール
description: 推奨される VidPN トポロジへのシステム コール
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2d6b33b223c0549e64965ff471e50b102844193
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352848"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>推奨される VidPN トポロジへのシステム コール


Windows 7 を実行するコンピューターでは、表示モード マネージャー (DMM) は、適用 CCD データベースで VidPN 履歴データを使用する適切な VidPN トポロジを決定します。 不要になった DMM は、Windows vista と同様に、最後の既知の適切なトポロジに基づいて VidPN トポロジを決定します。 その結果、Windows 7 DMM で呼び出すことはありません、 [ **DxgkDdiRecommendVidPnTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff559782)関数。

Windows Vista およびそのサービス パック、DMM の継続を呼び出す*DxgkDdiRecommendVidPnTopology*ドライバーが推奨される機能 VidPN トポロジを提供することを要求します。

 

 





