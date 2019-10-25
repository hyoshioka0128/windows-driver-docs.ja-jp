---
title: カーネルモード セーフ文字列関数のインポート
description: カーネルモード セーフ文字列関数のインポート
ms.assetid: f1cee7e0-151b-4e03-bf4d-400f328083fa
keywords:
- 安全な文字列関数のインポート
- インラインセーフ文字列関数バージョン WDK カーネル
- ライブラリの安全な文字列関数のバージョン WDK カーネル
- バイトカウント関数 WDK カーネル
- 文字カウント関数 WDK カーネル
- 安全な文字列関数 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cb386f4c92bbcc2133be9ca330464af2d4547c5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828308"
---
# <a name="importing-kernel-mode-safe-string-functions"></a>カーネルモード セーフ文字列関数のインポート





Windows XP 以降では、カーネルモードのセーフ文字列ライブラリは、、Ntstrsafe.h ヘッダーファイルで定義されているインライン関数のコレクションとして使用できます。

### <a href="" id="to-use-the-inline-versions-of-the-kernel-mode--safe-string-functions"></a>カーネルモードの安全な文字列関数を使用するには

次に示すように、ヘッダーファイルをインクルードします。

```cpp
#include <ntstrsafe.h>
```

バイトカウントのみを使用できます。または、文字がカウントされた安全な文字列関数だけを使用できます。

### <a name="to-allow-only-byte-counted-functions"></a>バイトカウント関数のみを許可するには

、Ntstrsafe.h ヘッダーファイルをインクルードする前に、コードに次の行を追加します。

```cpp
#define NTSTRSAFE_NO_CCH_FUNCTIONS
```

### <a name="to-allow-only-character-counted-functions"></a>文字カウント関数のみを許可するには

、Ntstrsafe.h ヘッダーファイルをインクルードする前に、コードに次の行を追加します。

```cpp
#define NTSTRSAFE_NO_CB_FUNCTIONS
```

、NTSTRSAFE.H\_NO\_CB\_FUNCTIONS または\_、NTSTRSAFE.H を定義して、\_CCH\_関数を使用することはできませんが、両方を定義することはできません。

[**UNICODE\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)構造関数を使用できないようにすることができます。

### <a href="" id="to-make-unicode-string-structure-functions-unavailable"></a>UNICODE\_文字列構造体関数を使用できないようにするには

、Ntstrsafe.h ヘッダーファイルをインクルードする前に、コードに次の行を追加します。

```cpp
#define NTSTRSAFE_NO_UNICODE_STRING_FUNCTIONS
```

ANSI または Unicode 文字列に含めることができる最大文字数は、、NTSTRSAFE.H\_MAX\_CCH です。 **Unicode\_文字列**構造に含めることができる最大文字数は、、NTSTRSAFE.H\_UNICODE\_STRING\_MAX\_cch です。 これらの定数は、、Ntstrsafe.h で定義されています。

ドライバーでは、、Ntstrsafe.h を含める前に次の行をコードに含めることにより、、NTSTRSAFE.H\_MAX\_CCH および、NTSTRSAFE.H\_UNICODE\_STRING\_MAX\_CCH に小さい値を割り当てることができます。

```cpp
#define NTSTRSAFE_MAX_CCH  <new-value>
#define NTSTRSAFE_UNICODE_STRING_MAX_CCH  <new-value>
```

、Ntstrsafe.h のディレクティブは、新しい値が既定値よりも大きくないことを確認します。

 

 




