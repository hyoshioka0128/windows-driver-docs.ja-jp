---
title: Visual SourceSafe によるデバッグ
description: Visual SourceSafe によるデバッグ
ms.assetid: 65cc4eda-7aed-489f-a622-27a42afc0e4a
keywords:
- Visual SourceSafe は、デバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51bcaa59549706d4dba145703e77408299e5e18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346315"
---
# <a name="debugging-with-visual-sourcesafe"></a>Visual SourceSafe によるデバッグ


デバッガーで適切に機能する Visual SourceSafe を使用してインデックス付きソース ファイルで、適切にシステムを構成する必要があります。

Visual SourceSafe データベースは、アクセスのユーザーと省略可能なパスワードを必要とする場合、使用および SSPWD 環境変数を使用してこれらの値を設定する必要があります。 さらに、Visual Studio 2005 で SrcSrv に付属しているのバージョンがかどうか Visual SourceSafe は資格情報を求める、これにより、アプリケーションが応答を停止を検出することはできません. SrcSrv に付属しているデバッグ ツールの Windows をこれを防ぐために使用のバージョンにアップグレードします。

エントリを追加して、この問題を回避取得できます Visual SourceSafe は、デバッグのコンピューターのパスに設定されていない場合、 [Srcsrv.ini](the-srcsrv-ini-file.md)デバッガーで動作するファイル。 このファイルを配置する必要がありますを Visual Studio の標準的なインストールを使用する場合

```text
%PROGRAMFILES%\Microsoft Visual Studio 8\Common7\IDE\srcsrv.ini
```

\[コマンドを信頼された\]セクション、Srcsrv.ini のフォームのエントリを追加

```ini
ss.exe="Path"
```

場所*パス*Ss.exe の場所です。

 

 





