---
title: 結合された言語とポート モニター
description: 結合された言語とポート モニター
ms.assetid: 5da362cf-92b8-4c78-80b2-57106b978600
keywords:
- 印刷モニター WDK、言語モニター
- WDK 印刷モニターは、ポートを監視します。
- 言語は、WDK 印刷、ポート モニター相互作用を監視します。
- ポートは、WDK 印刷、言語モニター相互作用を監視します。
- WDK の言語とポート モニターを組み合わせる
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c87cc2f2f7ffb9905ab91f84c2ccebfd42d4681
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578892"
---
# <a name="combined-language-and-port-monitor"></a>結合された言語とポート モニター





結合の言語およびポート モニターとして機能する 1 つのカスタマイズされた印刷モニターでは、プリンター特別なハードウェアをサポートできます。 このようなモニターは、構成パラメーターを取得するユーザーの介入を必要とする場合、UI の DLL とサーバーのモデルは、次の DLL に分割する必要があります[ポート モニター](port-monitors.md)します。 言語関連の機能は、サーバー DLL に属しています。

結合されたモニターの UI の DLL を定義する必要があります[モニター クライアント DLL 関数をポート](port-monitor-client-dll-functions.md)します。 両方のサーバー DLL を定義する必要があります[モニター サーバー DLL 関数をポート](port-monitor-server-dll-functions.md)と[言語モニター関数](language-monitor-functions.md)します。

 

 




