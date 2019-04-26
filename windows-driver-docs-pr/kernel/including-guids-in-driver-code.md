---
title: ドライバー コードに GUID を含める
description: ドライバー コードに GUID を含める
ms.assetid: 9235f9e6-9c40-4c4b-a98b-99e6b46a11ce
keywords:
- WDK のカーネルをグローバルに一意の識別子
- Guid の WDK カーネル
- WDK の Guid 識別子
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e083ae2ec3a89eb47292dafe80ca5705a0765a7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341087"
---
# <a name="including-guids-in-driver-code"></a>ドライバー コードに GUID を含める





Guid を使用して、カーネル モード ドライバーでは、2 つの処理を行う必要があります。

1.  再定義 Initguid.h ヘッダー ファイルを含める、**定義\_GUID**マクロ。

    Initguid.h ヘッダー ファイルを再定義、**定義\_GUID**マクロ (を EXTERN に参照を宣言するだけです) と Guid をインスタンス化します。 このヘッダー ファイルは、ドライバーのソース ファイルの Guid をインスタンス化する必要があります。 (ユーザー モード アプリケーションを含む Objbase.h GUID の定義を含むヘッダー ファイルをインクルードする前にします。)

2.  Guid を定義するヘッダー ファイルが含まれます。

    Initguid.h は、ステートメントの後に、GUID の定義を含むヘッダー ファイルが含まれます。 ドライバーには、システム提供のヘッダー ファイルとサード パーティ製のヘッダー ファイルを含む、GUID の定義を含む 1 つ以上のヘッダー ファイルが含まれます。

次のコードの抜粋は、Guid を含むステートメントのシーケンスを示しています。

```cpp
:
// include system headers here such as wdm.h

#include <initguid.h>

// include system and driver-specific header files here that contain
// GUID definitions

...
```

ドライバーの 1 つのモジュールで上記のステートメントを配置します。通常メイン モジュールです。 上記のステートメントが存在する場合、ドライバーはそのシンボリック名を使用して GUID を表します。








