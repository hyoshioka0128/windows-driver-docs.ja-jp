---
title: カーネルモード セーフ文字列関数のインポート
description: カーネルモード セーフ文字列関数のインポート
ms.assetid: f1cee7e0-151b-4e03-bf4d-400f328083fa
keywords:
- 安全な文字列関数をインポートします。
- インライン安全な文字列関数のバージョンの WDK カーネル
- ライブラリ安全な文字列関数のバージョンの WDK カーネル
- バイト カウント関数 WDK カーネル
- 関数の文字カウント WDK カーネル
- WDK の安全な文字列関数
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21e11c0e1275bb629dba89a6ddc32622f53ee0b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384258"
---
# <a name="importing-kernel-mode-safe-string-functions"></a>カーネルモード セーフ文字列関数のインポート





以降 Windows XP では、カーネル モードの文字列を安全なライブラリは Ntstrsafe.h ヘッダー ファイルで定義されているインライン関数のコレクションとして使用できます。

### <a href="" id="to-use-the-inline-versions-of-the-kernel-mode--safe-string-functions"></a>カーネル モードの安全な文字列関数を使用するには

ように、ヘッダー ファイルが含まれます。

```cpp
#include <ntstrsafe.h>
```

だけのバイト数または安全な文字列の文字カウント関数のみに使用可能なを作成できます。

### <a name="to-allow-only-byte-counted-functions"></a>バイト カウント関数のみを許可するには

Ntstrsafe.h ヘッダー ファイルをインクルードする前に、コードで次の行を含めます。

```cpp
#define NTSTRSAFE_NO_CCH_FUNCTIONS
```

### <a name="to-allow-only-character-counted-functions"></a>関数の文字カウントのみを許可するには

Ntstrsafe.h ヘッダー ファイルをインクルードする前に、コードで次の行を含めます。

```cpp
#define NTSTRSAFE_NO_CB_FUNCTIONS
```

NTSTRSAFE いずれかを定義することができます\_いいえ\_CB\_関数または NTSTRSAFE\_いいえ\_CCH\_両方ではなく、機能します。

行うことができます、 [ **UNICODE\_文字列**](https://msdn.microsoft.com/library/windows/hardware/ff564879)関数を使用できない構造体します。

### <a href="" id="to-make-unicode-string-structure-functions-unavailable"></a>UNICODE に\_文字列構造体の関数が使用できません。

Ntstrsafe.h ヘッダー ファイルをインクルードする前に、コードで次の行を含めます。

```cpp
#define NTSTRSAFE_NO_UNICODE_STRING_FUNCTIONS
```

任意の ANSI または Unicode 文字列に含めることができる文字の最大数は NTSTRSAFE\_最大\_CCH します。 文字の最大数、 **UNICODE\_文字列**構造に含めることができますが NTSTRSAFE\_UNICODE\_文字列\_最大\_CCH します。 これらの定数は、Ntstrsafe.h で定義されます。

ドライバーが NTSTRSAFE に小さい値を割り当てることができます\_最大\_CCH と NTSTRSAFE\_UNICODE\_文字列\_最大\_インクルードする前に、コードで、次の行を含めることによって CCHNtstrsafe.h します。

```cpp
#define NTSTRSAFE_MAX_CCH  <new-value>
#define NTSTRSAFE_UNICODE_STRING_MAX_CCH  <new-value>
```

Ntstrsafe.h ディレクティブは、新しい値が既定値を超えていないことを確認します。

 

 




