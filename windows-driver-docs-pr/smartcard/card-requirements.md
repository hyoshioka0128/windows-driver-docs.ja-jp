---
title: カードの要件
description: カードの要件
ms.assetid: 3BE887F9-4B35-4A83-9E98-DD7555DF2953
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c46911e0aa0fe77815b353f52e3e44ec665d00f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373541"
---
# <a name="card-requirements"></a>カードの要件


その他の要件には、いくつかのコンテキストを提供するには、ここでは、カードがプロビジョニングされ、使用方法に関する情報をします。

## <a name="span-idwhatablankcardisspanspan-idwhatablankcardisspanspan-idwhatablankcardisspanwhat-a-blank-card-is"></a><span id="What_a__Blank_Card__Is"></span><span id="what_a__blank_card__is"></span><span id="WHAT_A__BLANK_CARD__IS"></span>何が"Blank カード"


「空白の名刺」および可能な「作成」で、Microsoft スマート カード Base CSP または KSP を使用して、カードとですが。

-   カードのオペレーティング システムが含まれています。
-   含まれているか、必要なファイルおよびファイル システムを実装するためにデータを仮想化できます。
-   既定値を持つ管理者やユーザーの Pin またはキー。
-   まだありません「カードの作成」(次のセクション) で説明されているファイル。
-   さらにない準備でカードの作成の準備ができました。
-   将来のためでは、ISO 7816 4 パート 8 で定義されている参考情報を提供できます。

## <a name="span-idcardcreationspanspan-idcardcreationspanspan-idcardcreationspan-card-creation"></a><span id="_Card__Creation_"></span><span id="_card__creation_"></span><span id="_CARD__CREATION_"></span> カード「作成」


カードの暗号化操作に便利ですが、id 展開の目的で認識されることを許可する必要があり、管理し、それを Base CSP または KSP を使用することが可能にする必要があります。 これには、カードの ID ファイルと、カードに格納される Base CSP または KSP を必要とする特定のファイルが必要です。 カードにこれらの必要なファイルを作成する操作は、カードを「作成」と呼ばれます。 これは、展開ツールによって行われます、次の手順で構成されています。

1.  読のすべてのユーザーと、管理者書き込みアクセス許可が、カードのルート ディレクトリに"cardid"、カード ID ファイルを作成します。 このファイルには、カードの一意の 16 バイト バイナリ識別子が含まれています。 更新またはカードがまったくリサイクルされない限り、上書きされません。
2.  読み取り/書き込みアクセス許可を持つすべてのユーザーと、ルート ディレクトリで"cardcf"、キャッシュ ファイルを作成します。 最初の内容は、0 の値を持つ 6 バイトです。
3.  読のすべてのユーザーと書き込みのアクセス許可を持つユーザー、ルート ディレクトリで"cardapps"のアプリケーション マップを作成します。 最初の内容は、4 で 0 バイトの後に文字列"mscp"で構成される 8 バイト レコードです。
4.  呼び出して、Base CSP または CNG KSP アプリケーションを作成[ **CardCreateDirectory**](https://msdn.microsoft.com/library/windows/hardware/dn468710)読のすべてのユーザーと、ユーザーには、書き込み権限を持つ、"mscp"アプリケーションを参照します。
5.  読のすべてのユーザーと書き込みのアクセス許可を持つユーザーと同じディレクトリに"mscp"で、証明書のマップ ファイル"cmapfile"を作成します。 最初は空です。

技術的には、カードが「作成」手順 2 の後に、定義のすべてのカードが、mscp"Microsoft"アプリケーションが予約されますが、実際に使用するかどうか。 これには、通常とは異なるファクト"mscp"アプリケーションが常に作成されると、ファイルが"mscp"アプリケーション内で作成されたことについて説明します。 カード管理 Microsoft が提供する DLL 内の関数によって実装される、カードの作成を想定どおり、この情報は、そのコンテキストでこれらの操作を正しくサポートできるカード ミニドライバーの作成者向け参照情報として提供されます。

 

 





