---
title: '#PreCompiled プリプロセッサ ディレクティブ'
description: '#PreCompiled プリプロセッサ ディレクティブ'
ms.assetid: 639db56d-7677-4d21-8329-a0f35d68151e
keywords:
- WDK GDL、キーワードのプリプロセッサ ディレクティブ
- WDK GDL キーワード
- WDK の予約済みキーワード
- プリコンパイル済みディレクティブ WDK GDL
- GDL WDK、ソース ファイル
- ソース ファイル WDK GDL
- プリコンパイル済みのソース ファイルを WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34ab932722f694e8d59dfcb5d6fba449fcd8afaf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372904"
---
# <a name="precompiled-preprocessor-directive"></a>\#プリコンパイル済みのプリプロセッサ ディレクティブ


```GDL
#PreCompiled:  BOOL
```

\#プリコンパイル済みディレクティブは、ソース ファイルがプリコンパイル済みかどうかを指定します。

場合*BOOL*は**TRUE**、ソース ファイルは、事前にコンパイルすると見なされます。 それ以外の場合、ソース ファイルがを通じて参照されている場合、 [ \#Include](-include-preprocessor-directive.md)ファイルが含まれるディレクティブ、行にします。

\#プリコンパイル済みディレクティブは、任意の前に記述する必要があります[ \#Include](-include-preprocessor-directive.md)ディレクティブ GDL ソース ファイル内で、それ以外は無視されます。 *BOOL*値が必要です。

としてマークされているファイルのプリコンパイルはルート コンテキストで解析できません。 これは、ホストまたは GDL ファイルなどに確立されている任意のコンテキストはすべて失われます。 たとえば、ホストの GDL ファイルには、プリコンパイル済みファイルをインクルードする前にプリプロセッサ シンボルが定義されている、これらのシンボルがプリコンパイル済みファイルの解析時に存在しません。 この種類の解析では、プリコンパイル済みファイルの複数のバージョンを使用して作成できないことにより、 [ \#Ifdef](-ifdef-conditional-preprocessor-directive.md)ブロックを異なるホストにアクセスするさまざまな異なるシンボルを定義します\#Ifdef ブロック. プリコンパイル済みファイルが再解析しないために、1 つだけの一意のバージョンがあります。 したがって、プリコンパイル済みファイルのライターでは、任意の外部で定義されたプリプロセッサ シンボルに依存する必要があります。

また、コンパイル済みのファイルは、一意である必要があり、それらを含むホストに依存しない必要があることに注意してください。 プリコンパイル済みファイルは、ホスト ファイルの参照を任意に含まれるコンテンツまたはホスト ファイルで定義されたコンテンツに依存しないでください。

このプリプロセッサ ディレクティブは GDL の新機能です。
