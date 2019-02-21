---
title: リスト
description: リスト
ms.assetid: 69b928fa-8348-437a-ac4d-677f272615dd
keywords:
- GPD ファイル エントリ WDK Unidrv、リスト
- WDK GPD ファイルの属性を一覧表示します。
- 一覧のキーワード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c21fc24a8c9c36a0c97f74496a7ea1dfec64a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527532"
---
# <a name="lists"></a>リスト





属性に割り当てる一連の値には、するには、一覧のキーワードを使用します。 形式です。

**リスト**( *Value1* 、 *Value2* 、 *Value3* ,..., * の値*)

場所*Value1*、 *Value2*、 *Value3*,..., * の値*すべて属性の指定された型の 1 つまたは複数の値のセットを表します。 たとえば、次のようにプリンターのカラー プレーン データを送信する順序を指定できます。

```cpp
*ColorPlaneOrder: LIST(YELLOW, MAGENTA, CYAN, BLACK)
```

 

 




