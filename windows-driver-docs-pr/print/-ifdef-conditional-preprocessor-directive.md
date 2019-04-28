---
title: '#Ifdef 条件付きプリプロセッサ ディレクティブ'
description: '#Ifdef 条件付きプリプロセッサ ディレクティブ'
ms.assetid: 57c59bf8-19bd-47bc-858d-ea500d44fb4d
keywords:
- プリプロセッサ ディレクティブ WDK GDL、条件付きディレクティブ
- WDK GDL、条件付きディレクティブのディレクティブ
- 条件付きディレクティブ WDK GDL
- Ifdef ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c5bc44b021319f0d12036748b2ba9cd25a7a4f7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372912"
---
# <a name="ifdef-conditional-preprocessor-directive"></a>\#Ifdef 条件付きプリプロセッサ ディレクティブ


```GDL
#Ifdef: symbol
```

\#Ifdef ディレクティブは、条件付きコンストラクトとセクションの先頭を定義します。 シンボルはプリプロセッサ シンボル ディクショナリで見つかった場合は、セクションが保持されます。 シンボルが見つからない場合は削除されます。 *シンボル*値が必要です。
