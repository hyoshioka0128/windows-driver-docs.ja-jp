---
title: 静的パラメーターを設定します。
description: 静的パラメーターを設定します。
ms.assetid: 0a41d8b4-8dd8-4a6b-a9b9-d19d07acd083
keywords:
- WDK ネットワーク、静的パラメーターを追加レジストリ セクション
- 静的パラメーター WDK ネットワーク
- パラメーターの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9777de3fc8ee33f813cb98c29a4ccca738e1dfd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537785"
---
# <a name="setting-static-parameters"></a>静的パラメーターを設定します。





INF ファイルでは、静的パラメーターを 1 回だけ設定します。 このパラメーターは、ユーザー インターフェイスのプロパティ ページで再構成することはできません。

*追加レジストリ セクション*、REG として静的パラメーターを追加します。\_SZ 値コンポーネントのインスタンス キーに次の例で示すようにします。

```INF
[a1.staticparams.reg]
HKR,, MediaType, 0, "1"
HKR,, InternalId, 0, "232"
```

*追加レジストリ セクション*コンポーネントのインスタンス キーをベンダ定義の静的パラメーターを追加することができます。

 

 





