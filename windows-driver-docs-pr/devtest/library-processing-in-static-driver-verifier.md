---
title: 静的ドライバー検証ツールでのライブラリ処理
description: 静的ドライバー検証ツールでのライブラリ処理
ms.assetid: d95ccdc2-aa00-4671-87fb-6f0f77d2ba8d
keywords:
- Static Driver Verifier WDK、ライブラリ
- StaticDV WDK、ライブラリ
- SDV の WDK、ライブラリ
- ライブラリ WDK Static Driver Verifier
- ライブラリの処理に関するライブラリ WDK の Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 477b8fdf07195cebd7f1f6927c903d477f4943c5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572358"
---
# <a name="library-processing-in-static-driver-verifier"></a>静的ドライバー検証ツールでのライブラリ処理


多くのドライバーは、関数の動的および静的にリンクされたライブラリに依存します。 通常、ライブラリは、一般的な処理の関数を含めるが、場合によっては、ドライバーに不可欠な機能が含まれます。

ライブラリは、ドライバーがインターフェイス規則に準拠しているかどうかを決定するために不可欠です。 たとえば、ライブラリ コードがないは、ライブラリに含まれている必要な呼び出しが失敗するドライバーが表示されます可能性があります。 または、ライブラリなど、ロックの解放を 2 回の繰り返しのエラーの原因で、ドライバーが重複する呼び出しを含めることができます。

ドライバーの検証で、ライブラリは、SDV は、まず[ライブラリを処理](processing-a-library.md)ドライバーの検証に使用するための準備をしています。

SDV は、自動的に検出し、ドライバーが依存するすべてのライブラリの処理を試みますが、これらのライブラリを自動的に処理できない一部ライブラリのソース ファイルの場所がわからないため、ドライバーの検証に含めるとします。 SDV には、ドライバーを最も正確な分析を提供するためには、する必要があります手動で参照を追加するすべてのライブラリ、ドライバー SDV のライブラリのキャッシュをクリックして、**ライブラリ**タブおよび選択**Add Library**、ライブラリを処理します。  コマンドラインを実行している場合に sdv を実行してライブラリを追加することがあります、 **/lib**ライブラリ プロジェクトに対するコマンド。

SDV は、ライブラリで処理が、その処理はファイルをそのライブラリを保持およびライブラリを必要とするすべてのドライバーの検証で自動的にライブラリ コードが含まれます。 ライブラリ コードを変更しない限り、ライブラリを再処理する必要はありません。 ライブラリを再処理する方法については、次を参照してください。[ライブラリを再処理](reprocessing-a-library.md)します。

このセクションの内容:

[ライブラリの処理](processing-a-library.md)

[ライブラリを再処理](reprocessing-a-library.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

SDV には、システム ライブラリの処理済みのライブラリ ファイルが含まれています。 これらのライブラリを処理する SDV を指示する必要はありません。 SDV は、ドライバーがこれらのライブラリに依存することを検出すると警告メッセージを表示することがなくこれらのライブラリ、処理対象のファイルを使用します。 ライブラリの要件については、次を参照してください。 [Static Driver Verifier に、ドライバーまたはライブラリがサポートしているかを決定する](determining-if-static-driver-verifier-supports-your-driver-or-library.md)します。

 

 





