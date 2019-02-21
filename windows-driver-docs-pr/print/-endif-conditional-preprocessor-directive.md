---
title: '#Endif 条件付きプリプロセッサ ディレクティブ'
description: '#Endif 条件付きプリプロセッサ ディレクティブ'
ms.assetid: dfbfdb4a-955b-4ccf-b496-c8c5ddc42d2b
keywords:
- プリプロセッサ ディレクティブ WDK GDL、条件付きディレクティブ
- WDK GDL、条件付きディレクティブのディレクティブ
- 条件付きディレクティブ WDK GDL
- Endif ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e0cdd94f53537150477bfb32ba482c1df14ad1f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557077"
---
# <a name="endif-conditional-preprocessor-directive"></a>\#Endif 条件付きプリプロセッサ ディレクティブ


```GDL
#Endif:
```

\#Endif ディレクティブは、前のセクションと、条件付きコンストラクトの end を定義します。 シンボルは使用されません。 値として、偽のシンボル名を使用することができます、 \#Endif ディレクティブを読者にします。 次のコード例を検討してください。

```GDL
    #Ifdef: symbolA

        #Ifdef: symbolB

        #Elseifdef: symbolD

        #Endif: symbolB

    #Endif: symbolA
```

入れ子になった各構成体のインデントもリーダーに役立つ場合があります。
