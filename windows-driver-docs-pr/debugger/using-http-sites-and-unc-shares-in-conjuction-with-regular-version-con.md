---
title: 通常のバージョン管理と組み合わせた HTTP サイトと UNC 共有の使用
description: 通常のバージョン管理と組み合わせた HTTP サイトと UNC 共有の使用
ms.assetid: 1b045a00-45e7-47e8-9447-7d94f70253fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0332d15c5fc349d86c63882fa5e84a4a90d8ef63
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378796"
---
# <a name="using-http-sites-and-unc-shares-in-conjuction-with-regular-version-control"></a>通常のバージョン管理と組み合わせた HTTP サイトと UNC 共有の使用


SrcSrv の標準機能がバージョン コントロールからファイルを抽出する必要がありますもソース ファイルで使用できるように、Web サイトまたは UNC 共有を使用して、開発者をサポートする必要があります。 これは、バージョン管理へのアクセスがないテスト ラボを設定している場合に発生する可能性があります。 ユーザーが同じ .pdb ファイルのセットを使用して両方をサポートできるようになります。

まず、付けて SrcTool; を使用して、ソース ファイルを抽出します。参照してください[ソース ファイルの抽出](extracting-source-files.md)詳細についてはします。 共有として使用できるようにするか、Web サイトまたは UNC 共有です。 現在の目的は、Cv2http.cmd スクリプトを使用して .pdb ファイルを変換する必要があります。

HTTP/UNC 共有を使用するコンピューター、編集、 [Srcsrv.ini](the-srcsrv-ini-file.md)デバッガー ディレクトリにあるファイル。 ファイルの variables セクションでは、次の 3 つのステートメントを追加します。

```ini
MY_SOURCE_ROOT=\\server\share
 SRCSRVCMD=
 SRCSRVTRG=%MY_SOURCE_ROOT%\%var2%\%var3%\%var4%\%fnfile%(%var1%)
```

置き換える必要があります\\ \\server\\を提供する UNC 共有のルートまたはソース ファイルを含む Web サイトの URL を共有します。 MY を変更することもできます。\_ソース\_ルートがこの場所を記述する任意のエイリアスです。 これらの例外を除き、他のすべて入力することの説明に従って正確に。

この方法で設定するすべてのデバッガーでは、標準のバージョン コントロールの抽出手順を無視し、代わりに指定された場所からソース ファイルにアクセスします。 その一方で、Srcsrv.ini に含まれるこれらのアイテムのすべてのデバッガーは、ソース ファイルを抽出するのに通常のバージョン コントロール機構を使用します。

 

 





