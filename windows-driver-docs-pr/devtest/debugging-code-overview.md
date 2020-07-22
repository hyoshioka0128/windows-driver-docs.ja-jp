---
title: コードのデバッグの概要
description: コードのデバッグの概要
ms.assetid: 2c76e569-61cd-44b0-b8e5-032ab2c48fdb
keywords:
- ドライバーのデバッグ WDK, コードのデバッグ
- コードのデバッグ WDK
- コードのデバッグ, コードのデバッグについて
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: f866194ba98dd08b40cde834a1b21fa00f62b9c4
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873835"
---
# <a name="debugging-code-overview"></a>コードのデバッグの概要

特別なデバッグルーチン、マクロ、およびグローバル変数は、ユーザーモードドライバーとカーネルモードドライバーの両方で使用できます。 これらのルーチンをドライバーコードで使用することにより、デバッガーにメッセージを送信し、デバッグに役立つブレークポイントを設定できます。

[条件付きコンパイルとビルド環境](conditional-compilation-and-the-build-environment.md)

デバッグの詳細については、ドキュメントの次のトピックを参照してください。

[デバッガーへの割り込み](..\debugger\breaking-into-the-debugger.md)

[デバッガーへの出力の送信](..\debugger\sending-output-to-the-debugger.md)

[デバッグ メッセージの読み取りとフィルター処理](..\debugger\reading-and-filtering-debugging-messages.md)

[デバッガーがアタッチされているかどうかの判別](..\debugger\determining-if-a-debugger-is-attached.md)
