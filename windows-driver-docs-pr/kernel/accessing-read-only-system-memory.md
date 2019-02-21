---
title: 読み取り専用のシステム メモリへのアクセス
description: 読み取り専用のシステム メモリへのアクセス
ms.assetid: d2c1f933-3a7e-4e82-b96d-4f019b27abd5
keywords:
- メモリ管理の WDK カーネル、読み取り専用メモリ
- 読み取り専用メモリ WDK カーネル
- システムの呼び出しをインターセプト
- グローバル文字列の WDK メモリ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe62862df9133eb15f054dd1c8eebcbd230d34a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548801"
---
# <a name="accessing-read-only-system-memory"></a>読み取り専用のシステム メモリへのアクセス





Windows[メモリ マネージャー](windows-kernel-mode-memory-manager.md)書き込み可能としてマークされていないページの読み取り専用アクセスを許可します。

ユーザー モードで、読み取り専用メモリは常に保護されています。 ただし、Windows NT 4.0 およびそれ以前のバージョンでは、読み取り専用メモリ保護されなかったカーネル モードでします。

Windows カーネル モード ドライバーまたはアプリケーションが読み取り専用メモリ セグメントへの書き込みを試みると、バグ チェックが発行されます。 詳細については、次を参照してください。 [ **0xBE のバグ チェック。試行\_書き込み\_TO\_READONLY\_メモリ**](https://msdn.microsoft.com/library/windows/hardware/ff560161)します。

### <a name="intercepting-system-calls"></a>システムの呼び出しをインターセプト

ドライバーのコードを上書きし、ジャンプ手順やその他の変更を挿入していくつかのドライバーのインターセプト システムを呼び出します。 ドライバーのコードが読み取り専用のため、この手法が発行されるバグ チェックになります。

### <a name="global-strings"></a>グローバル文字列

グローバル文字列を変更すると、定数値へのポインターとして宣言しない必要があります。

```cpp
CHAR *myString = "This string cannot be modified.";
```

ここでは、リンカーは、読み取り専用メモリのセグメントに文字列を格納する可能性があります。 文字列を変更しようとすると、バグ チェックが発生します。

代わりに、文字列は、左辺値の文字の配列として明示的に宣言する必要があります。

```cpp
CHAR myString[] = "This string can be modified.";
```

この宣言を使用するが、文字列を書き込み可能なメモリに格納されることを確認します。

 

 




