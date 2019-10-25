---
title: Windows カーネルモード セーフ文字列ライブラリ
description: Windows カーネルモード セーフ文字列ライブラリ
ms.assetid: a54cd20c-2c2d-462d-b9fc-112e99562e52
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c12ea9f8d32229a958974a15bde295957e8b68f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835694"
---
# <a name="windows-kernel-mode-safe-string-library"></a>Windows カーネルモード セーフ文字列ライブラリ


ソフトウェアセキュリティの主な問題の1つは、文字列を操作する際の脆弱性に関連しています。 セキュリティを強化するために、Windows には安全な文字列ライブラリが用意されています。

安全な文字列ライブラリルーチンには、"**Rtl**" という文字がプレフィックスとして付けられます。カーネルのすべての安全な文字列ライブラリルーチンの一覧については、「 [Unicode および ANSI 文字の安全な文字列関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicode-and-ansi-characters)」および「 [UNICODE_STRING 構造体の安全な文字列関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_kernel/#safe-string-functions-for-unicodestring-structures)」を参照してください。

安全な文字列の使用方法の詳細については、「[安全な文字列関数の使用](using-safe-string-functions.md)」を参照してください。

また、カーネルには、文字列機能を持つ C プログラミング全般用の別のランタイムライブラリもあります。 ランタイムライブラリ (RTL) の詳細については、「 [Windows カーネルモードランタイムライブラリ](windows-kernel-mode-run-time-library.md)」を参照してください。 両方のライブラリの先頭に "**Rtl**" が付いている場合でも、ライブラリは同じではないことに注意してください。

 

 




