---
title: カーネルモード セーフ整数関数のインポート
description: カーネル モードの安全な整数関数 ntintsafe.h、または、コードをリンクするライブラリに含まれるインライン コードとして利用できます。
ms.assetid: C6696C4E-952A-4162-B2BE-F262496FFBD2
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ecb667fc5ffd86f52c62eb1db13ec8f21c9558cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341066"
---
# <a name="importing-kernel-mode-safe-integer-functions"></a>カーネルモード セーフ整数関数のインポート


カーネル モードの安全な整数関数 ntintsafe.h、または、コードをリンクするライブラリに含まれるインライン コードとして利用できます。 このヘッダー ファイルでは、Windows Driver Kit (WDK) で使用することができます。

符号なしの値に対する算術演算を使用する必要がありますに注意してください。 符号付きの値を使用するのにには、最初に変換する符号付きの値を符号なしの値に安全に、算術関数を使用する前に変換関数を使用する必要があります。

## <a name="to-use-the-inline-versions-of-the-kernel-mode-safe-integer-functions"></a>カーネル モードの整数の安全な関数のインライン バージョンを使用するには


ように、ヘッダー ファイルが含まれます。

```ManagedCPlusPlus
#include <ntintsafe.h>
```

 

 




