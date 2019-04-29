---
title: '#DisablePPDirective プリプロセッサ ディレクティブ'
description: '#DisablePPDirective プリプロセッサ ディレクティブ'
ms.assetid: 5f85a6b1-a72f-45e2-901a-7bce94b4793c
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- DisablePPDirective ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a549073bed18cc5981ca1e931c9409a85ffe3366
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331786"
---
# <a name="disableppdirective-preprocessor-directive"></a>\#DisablePPDirective プリプロセッサ ディレクティブ


```GDL
#DisablePPDirective:    Directive
```

\#DisablePPDirective ディレクティブを有効になっているディレクティブを無効にします。 新しい GDL ファイルには、古い GDL ファイル持つ 1 つまたは複数の新しいディレクティブ名、名前空間の競合にはが含まれている場合は、新しいディレクティブをファイルをインクルードする前に無効になっているし、し、後で再び有効にします。 基本名では、必須の値です。

このプリプロセッサ ディレクティブは GDL の新機能です。

次のコード例では、このディレクティブを使用する方法を示します。

```GDL
#DisablePPDirective: duplicateDirective
#Include: "OlderFile.gdl"  *%  This file uses the name 
    *%  duplicateDirective because it does not expect that name to be interpreted by 
    *%  the preprocessor.
#EnablePPDirective: duplicateDirective
    *%  Reactivate  duplicateDirective  so it can be used by 
    *%  the newer host file.
```

 

 




