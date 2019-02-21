---
title: '#プリプロセッサ ディレクティブを未定義します。'
description: '#プリプロセッサ ディレクティブを未定義します。'
ms.assetid: 78f6a895-2c30-4a6f-8916-4c18e22e4e70
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- 未定義の WDK GDL ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 182639dbe6432a355349c51b5a24eb8782dfd4a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530329"
---
# <a name="undefine-preprocessor-directive"></a>\#プリプロセッサ ディレクティブを未定義します。


```GDL
#Undefine: symbol
```

\#ディレクティブの削除の未定義、*シンボル*プリプロセッサ シンボルをディクショナリからの値。 シンボルが定義されている場合は、複数回、最新の定義のみ*シンボル*が削除されます。

*シンボル*値は省略可能です。 この値を省略すると、最近に定義されたシンボルは削除されます。 ただし、区切り記号のコロン (:)必要です。
