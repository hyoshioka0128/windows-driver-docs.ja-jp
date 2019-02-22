---
title: '#EnablePPDirective プリプロセッサ ディレクティブ'
description: '#EnablePPDirective プリプロセッサ ディレクティブ'
ms.assetid: aebb11ec-b281-461e-b3fd-65e9b2773049
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- EnablePPDirective ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1605a374a3fb3165f9909cc0d707c61956c3b6e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532908"
---
# <a name="enableppdirective-preprocessor-directive"></a>\#EnablePPDirective プリプロセッサ ディレクティブ


```GDL
#EnablePPDirective: Directive
```

\#EnablePPDirective により、無効なディレクティブを有効にします。 GDL パーサーの将来のバージョンでは、その他のプリプロセッサ ディレクティブを定義します。 GDL の既存のファイルは、独自の目的でその新しいディレクティブ名を使用しても場合、既存 GDL 解析ファイルでしたが、新しいパーサーで予期しない結果。 この将来の互換性の問題を回避する任意の新しいディレクティブは既定で無効になり、を使用して有効にする必要があります、 \#EnablePPDirective ディレクティブ。 *ディレクティブ*値は (プレフィックス) を指定せずに有効にするディレクティブの基本名です。 ディレクティブの名前は、必須の値です。

このプリプロセッサ ディレクティブは GDL の新機能です。
