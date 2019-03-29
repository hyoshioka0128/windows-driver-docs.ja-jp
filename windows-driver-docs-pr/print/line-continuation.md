---
title: 行継続
description: 行継続
ms.assetid: ee4dbb3d-ba9d-45bb-82dd-ecee4682ae63
keywords:
- GPD ファイル エントリ WDK Unidrv、行連結文字
- 行連結文字 WDK GPD ファイル
- 継続的な行 WDK GPD ファイル
- WDK GPD ファイルの連結文字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: facfa623fa383c257d7e505e4df6c97975ace68e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570527"
---
# <a name="line-continuation"></a>行継続





[GPD ファイル エントリ](gpd-file-entries.md)は長すぎて 1 つに収まらない行は、後続の行で続行することができます。 エントリを続行するには、プラス記号 (+)、最初より後の各行を前する必要があります。 プラス記号は、次の例に示すように、上記のホワイト スペースのない行の最初の文字にすることがあります。

```cpp
*DeviceFonts:
+    LIST(
+        =RC_FONT_Courier_10pt_regular,
+        =RC_FONT_CGTimes_regular,
+        =RC_FONT_Univers_regular,
+        =RC_FONT_Univers_condensed_regular,
+        =RC_FONT_Antique_Olive_regular,
+        =RC_FONT_Albertus_Medium,
+        =RC_FONT_Albertus_Extra_Bold,
+        =RC_FONT_Courier_regular,
+        =RC_FONT_Letter_Gothic_regular,
+        =RC_FONT_Wingdings)
```

次の行の先頭行継続文字を使用する必要はありません。

-   アスタリスクで始まる行。

-   左中かっこで始まる行。

 

 




