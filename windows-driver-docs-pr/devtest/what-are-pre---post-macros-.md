---
title: 以前はマクロを投稿/
description: 以前はマクロを投稿/
ms.assetid: f5acb047-def3-443a-b220-77543f9a71e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb8f0ef4b4af320b1e2b26d836a6d1484fb67e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570134"
---
# <a name="what-are-pre--post-macros"></a>PRE/POST マクロとは


前のログ記録と後のログ記録のマクロ定義 WPP\_レベル\_前 (*レベル*) と WPP\_レベル\_POST (*レベル*) マクロです。 後者には、トレース機能の拡張の一部となるユーザー コードを示します。 プロセスのセットアップまたはトレース ポイントの周りのクリーンアップの前と後のログ記録のマクロを使用できます。

既定では、何が設定されます。 ただし、いくつかのログの前と後のログのロジックを追加するように定義できます。

```
PRE macro // If defined
If (WPP_CHECK_INIT && (Level,Flag) is enabled) {
....Call TraceMessage;
}
POST macro // If defined
```

例前/後のマクロを定義する方法については、[がどのようにトレース-式が使用されている場合ですか?](how-are-trace-if-expressions-used-.md)を参照してください。

 

 





