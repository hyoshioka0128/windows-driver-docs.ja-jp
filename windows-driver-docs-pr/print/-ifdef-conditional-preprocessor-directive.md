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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553745"
---
# <a name="ifdef-conditional-preprocessor-directive"></a>\#Ifdef 条件付きプリプロセッサ ディレクティブ


```GDL
#Ifdef: symbol
```

\#Ifdef ディレクティブは、条件付きコンストラクトとセクションの先頭を定義します。 シンボルはプリプロセッサ シンボル ディクショナリで見つかった場合は、セクションが保持されます。 シンボルが見つからない場合は削除されます。 *シンボル*値が必要です。
