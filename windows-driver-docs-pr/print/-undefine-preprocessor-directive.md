---
title: '#Undefine プリプロセッサ ディレクティブ'
description: '#Undefine プリプロセッサ ディレクティブ'
ms.assetid: 78f6a895-2c30-4a6f-8916-4c18e22e4e70
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- 未定義の WDK GDL ディレクティブ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 182639dbe6432a355349c51b5a24eb8782dfd4a9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372916"
---
# <a name="undefine-preprocessor-directive"></a>\#プリプロセッサ ディレクティブを未定義します。


```GDL
#Undefine: symbol
```

\#ディレクティブの削除の未定義、*シンボル*プリプロセッサ シンボルをディクショナリからの値。 シンボルが定義されている場合は、複数回、最新の定義のみ*シンボル*が削除されます。

*シンボル*値は省略可能です。 この値を省略すると、最近に定義されたシンボルは削除されます。 ただし、区切り記号のコロン (:)必要です。
