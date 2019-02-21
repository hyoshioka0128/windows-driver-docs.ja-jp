---
title: '#Elseifdef 条件付きプリプロセッサ ディレクティブ'
description: '#Elseifdef 条件付きプリプロセッサ ディレクティブ'
ms.assetid: 0239696a-ea6a-4fd4-b4ca-870a87022c81
keywords:
- プリプロセッサ ディレクティブ WDK GDL、条件付きディレクティブ
- WDK GDL、条件付きディレクティブのディレクティブ
- 条件付きディレクティブ WDK GDL
- Elseifdef ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f3e30c20e9dc1b300cdc46f0ffd8f94ad152abc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530333"
---
# <a name="elseifdef-conditional-preprocessor-directive"></a>\#Elseifdef 条件付きプリプロセッサ ディレクティブ


```GDL
#Elseifdef: symbol
```

\#Elseifdef ディレクティブは、前のセクションの終わりと新しい条件付きセクションの先頭を定義します。 セクションには、プリプロセッサ シンボル ディクショナリで、シンボルが検出された場合は、構造内の前のセクションは保持されませんが保持されます。 シンボルが見つからない場合、コンス トラクターは削除されます。 *シンボル*値が必要です。
