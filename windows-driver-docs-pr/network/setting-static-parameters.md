---
title: 静的パラメーターの設定
description: 静的パラメーターの設定
ms.assetid: 0a41d8b4-8dd8-4a6b-a9b9-d19d07acd083
keywords:
- WDK ネットワーク、静的パラメーターを追加レジストリ セクション
- 静的パラメーター WDK ネットワーク
- パラメーターの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9777de3fc8ee33f813cb98c29a4ccca738e1dfd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346664"
---
# <a name="setting-static-parameters"></a>静的パラメーターの設定





INF ファイルでは、静的パラメーターを 1 回だけ設定します。 このパラメーターは、ユーザー インターフェイスのプロパティ ページで再構成することはできません。

*追加レジストリ セクション*、REG として静的パラメーターを追加します。\_SZ 値コンポーネントのインスタンス キーに次の例で示すようにします。

```INF
[a1.staticparams.reg]
HKR,, MediaType, 0, "1"
HKR,, InternalId, 0, "232"
```

*追加レジストリ セクション*コンポーネントのインスタンス キーをベンダ定義の静的パラメーターを追加することができます。

 

 





