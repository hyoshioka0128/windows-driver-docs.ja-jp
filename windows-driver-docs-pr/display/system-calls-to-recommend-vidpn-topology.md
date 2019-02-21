---
title: システム コール VidPN トポロジをお勧めします。
description: システム コール VidPN トポロジをお勧めします。
ms.assetid: cc23be93-be31-4069-960c-268a8b151063
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2d6b33b223c0549e64965ff471e50b102844193
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552159"
---
# <a name="system-calls-to-recommend-vidpn-topology"></a>システム コール VidPN トポロジをお勧めします。


Windows 7 を実行するコンピューターでは、表示モード マネージャー (DMM) は、適用 CCD データベースで VidPN 履歴データを使用する適切な VidPN トポロジを決定します。 不要になった DMM は、Windows vista と同様に、最後の既知の適切なトポロジに基づいて VidPN トポロジを決定します。 その結果、Windows 7 DMM で呼び出すことはありません、 [ **DxgkDdiRecommendVidPnTopology** ](https://msdn.microsoft.com/library/windows/hardware/ff559782)関数。

Windows Vista およびそのサービス パック、DMM の継続を呼び出す*DxgkDdiRecommendVidPnTopology*ドライバーが推奨される機能 VidPN トポロジを提供することを要求します。

 

 





