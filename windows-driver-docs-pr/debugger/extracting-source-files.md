---
title: ソース ファイルの抽出
description: ソース ファイルの抽出
ms.assetid: b7c859a9-5264-401c-ad96-ad044bcc140e
keywords:
- ソース ファイルを抽出します。
- ソース サーバー、ソース ファイルを抽出します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: acd9accb0cec0ee66680071bbdd607f14ad9ee29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375407"
---
# <a name="extracting-source-files"></a>ソース ファイルの抽出


ソースを提供するすべてのモジュールからすべてのソース ファイルを抽出するには、コマンドを使用します。

```console
srctool.exe -x
```

バージョン コントロールのアクセス権を持つコンピューターでバージョン コントロール システムのソース インデックス作成済みの .pdb ファイルには、このツールを実行する必要があります。 これは、一般的なディレクトリ ツリーにすべてのソース ファイルを配置します。 Web サイトのルートには、このツリーの内容をコピーします。 これは、新しい製品や追加するモジュールに好きなだけ何度でも実行できます。 ファイルが互いを分離して一意にアクセスできるように、ディレクトリ ツリーの構造が異種ファイルを保持しているために上書き心配はありません。

### <a name="span-idwalkspanspan-idwalkspanwalk"></a><span id="walk"></span><span id="WALK"></span>方法について説明します

Windows ツールのデバッグにはにウォーク (Walk.cmd) スクリプトが含まれます。 このスクリプトでは、ディレクトリ ツリーを再帰的に検索し、指定したファイル マスクに一致するすべてのファイルで、指定したコマンドを実行します。 構文は次のとおりです。

```console
walk.cmd FileMask Command
```

場所*FileMask*有無にかかわらず、付随する開始ディレクトリ、ファイル マスクを指定し、*コマンド*実行するコマンドを指定します。

すべての .pdb ファイルを c: で srctool.exe ファイル抽出コマンドを実行する例を次に示します\\シンボルとそのサブディレクトリ。

```console
walk.cmd c:\symbols\*.pdb srctool.exe -x
```

 

 





