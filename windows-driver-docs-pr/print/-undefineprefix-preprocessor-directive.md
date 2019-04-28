---
title: '#UndefinePrefix プリプロセッサ ディレクティブ'
description: '#UndefinePrefix プリプロセッサ ディレクティブ'
ms.assetid: 7c99c2cf-6609-4fec-ae21-1477699ba5c8
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- UndefinePrefix ディレクティブ WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82adc4b5554b15f883f8e728cfbc1f9664cfa693
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372915"
---
# <a name="undefineprefix-preprocessor-directive"></a>\#UndefinePrefix プリプロセッサ ディレクティブ


```GDL
#UndefinePrefix:
```

\#UndefinePrefix ディレクティブは、現在のプレフィックスを削除します。 以前に定義されたプレフィックスでは、現在プレフィックスになります。 使用して定義したプレフィックスのみ、 [ \#SetPPPrefix](-setppprefix-preprocessor-directive.md)ディレクティブを定義できます。 システムの既定のプレフィックスを未定義にすることはできません。 このディレクティブは、シンボルを使用しません。

このプリプロセッサのプレフィックスは GDL の新機能です。
