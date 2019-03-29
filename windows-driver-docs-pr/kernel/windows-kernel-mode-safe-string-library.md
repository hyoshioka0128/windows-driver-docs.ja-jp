---
title: Windows カーネルモード セーフ文字列ライブラリ
description: Windows カーネルモード セーフ文字列ライブラリ
ms.assetid: a54cd20c-2c2d-462d-b9fc-112e99562e52
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 65f17fabfd5ec34940e77be5a4c66e57559c8b78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582043"
---
# <a name="windows-kernel-mode-safe-string-library"></a>Windows カーネルモード セーフ文字列ライブラリ


ソフトウェアのセキュリティの主要な問題の 1 つは、文字列の操作の脆弱性に関連します。 セキュリティの強化を提供するには、Windows は、安全な文字列のライブラリを提供します。

ライブラリ ルーチンの安全な文字列の文字が付いて"**Rtl**"は、カーネルのすべての安全な文字列ライブラリ ルーチンの一覧を参照してください[Unicode と ANSI 文字の文字列関数を安全な](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#safe-string-functions-for-unicode-and-ansi-characters)と[。UNICODE_STRING 構造体の安全な文字列関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_kernel/#safe-string-functions-for-unicodestring-structures)します。

詳細については safe の文字列を使用して、次を参照してください。[安全な文字列関数を使用して](using-safe-string-functions.md)します。

文字列の同様の機能のあるカーネルの一般的な C プログラミングの個別のランタイム ライブラリも注意してください。 ランタイム ライブラリ (RTL) の詳細については、次を参照してください。 [Windows カーネル モードのランタイム ライブラリ](windows-kernel-mode-run-time-library.md)します。 両方のライブラリが付いている場合でもなお"**Rtl**"同じライブラリではありません。

 

 




