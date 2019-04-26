---
title: オペレーティング システム モデル
description: オペレーティング システム モデル
ms.assetid: a7200472-24e1-4ecf-86c7-a1b72c5661fc
keywords:
- Static Driver Verifier WDK、オペレーティング システムのモデル
- StaticDV WDK、オペレーティング システムのモデル
- SDV の WDK、オペレーティング システムのモデル
- オペレーティング システムのモデル WDK Static Driver Verifier
- ハーネス WDK Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd5a9cb970bf8689caac966296453de3a5641e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356350"
---
# <a name="operating-system-model"></a>オペレーティング システム モデル


SDV*オペレーティング システムのモデル*または*ハーネス*検証中に、オペレーティング システムとして機能する Windows コードの部分と抽象化のセグメントで構成されます。 SDV には、既定のオペレーティング システムのモデルと特定の検証に使用されるいくつかの特殊なモデルが含まれます。[ルール](static-driver-verifier-rule.md)します。 SDV アセンブル時の検証のオペレーティング システムのモデル、**確認**の手順、[検証プロセス](verification-process.md)します。

Windows オペレーティング システムと同様に、ドライバー内のエントリ ポイントを呼び出すことによって、ドライバーの部分を実行するハーネスもあります。

 

 





