---
title: Visual SourceSafe を使用します。
description: Visual SourceSafe を使用します。
ms.assetid: a315a1c5-1427-4432-aec0-314dbb6d7ae5
keywords:
- Visual SourceSafe
- 移行元サーバーでは、Visual SourceSafe
- SrcSrv、Visual SourceSafe
- Visual SourceSafe、SrcSrv
- Visual SourceSafe, 概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e01291cad2de04560bff449c193966648c1e82c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527802"
---
# <a name="using-visual-sourcesafe"></a>Visual SourceSafe を使用します。


Visual SourceSafe は x86 ベースのアプリケーションと、x86 でのみ、ソースのインデックス作成スクリプトと関連付けられているツールがインストールされているパッケージの Windows のツールをデバッグします。

正常に SrcSrv で Visual SourceSafe を使用して、Visual SourceSafe の既定のデータベース、現在のプロジェクトおよび作業フォルダーを含む、システムでいくつかの既定値を設定する必要があります。 Visual SourceSafe は、指定されたファイルのバージョンを区別できるように、ラベルが各ビルドのプロジェクトをスタンプする必要があります。 最後に、Visual SourceSafe データベースにアクセスするために必要な資格情報を設定する必要があります。

### <a name="span-idvisualsourcesafedatabasespanspan-idvisualsourcesafedatabasespanvisual-sourcesafe-database"></a><span id="visual_sourcesafe_database"></span><span id="VISUAL_SOURCESAFE_DATABASE"></span>Visual SourceSafe データベース

SSDIR 環境変数には、既定の Visual SourceSafe データベースを設定できます。 設定されていない場合があります、SrcSrv のインデックス作成スクリプトは、通常を判断できます、レジストリから。 できない場合は、スクリプトでは、SSDIR を設定するように求められます。 かに関係なく、このデータベースの値を表示する必要があります、 [Srcsrv.ini](the-srcsrv-ini-file.md)ファイルと共に、データベースを識別する単純なエイリアスです。 詳細な手順については、Srcsrv.ini 内のコメントで確認できます。 次の構文を使用して Srcsrv.ini の variables セクションでは、エントリを追加する必要があります。

```ini
MYDATABASE=\\server\VssShare
```

### <a name="span-idcurrentprojectspanspan-idcurrentprojectspancurrent-project"></a><span id="current_project"></span><span id="CURRENT_PROJECT"></span>現在のプロジェクト

Visual SourceSafe の概念を使用して、*現在プロジェクト*します。 SrcSrv のインデックス作成スクリプトでは、この値と現在のプロジェクトの一部であるこれらのソース ファイルを処理の制限を考慮します。 現在のプロジェクトを表示するには、次のコマンドを使用します。

```console
ss.exe project
```

現在のプロジェクトを変更するには、次のコマンドを使用します。

```console
ss.exe cp Project
```

場所*プロジェクト*現在のプロジェクトを示します。 たとえば、すべてのプロジェクトを処理するルートに、現在のプロジェクトを設定します。

```console
ss.exe cp $/
```

### <a name="span-idworkingfolderspanspan-idworkingfolderspanworking-folder"></a><span id="working_folder"></span><span id="WORKING_FOLDER"></span>作業フォルダー

関連付けられている visual SourceSafe プロジェクト*作業フォルダー*します。 作業フォルダーは、プロジェクトのルートに対応するクライアント コンピューター上の場所です。 ただしこのようなコンピューターを入手して作業フォルダーを通常、Visual Studio インターフェイスを通じて、または、コマンドを使用してプロジェクトを作成するときに指定されていないソースを構築することができます。

```console
ss.exe get -R
```

ただし、この操作モードでは、SrcSrv のインデックス作成と互換性がありません。 SrcSrv では、作業フォルダーを指定する必要があります。 作業フォルダーを設定するには、コマンドを使用します。

```console
ss.exe workfold Project Folder
```

場所*プロジェクト*、現在のプロジェクトを示すと*フォルダー*プロジェクトのルートに対応する場所を示します。

### <a name="span-idlabelsspanspan-idlabelsspanlabels"></a><span id="labels"></span><span id="LABELS"></span>ラベル

Visual SourceSafe では、ビルド コンピューターの作業ディレクトリ内に存在するファイルのバージョンを判断できません。 したがって、デバッガー クライアント上のソース ファイルの抽出に使用される識別子でプロジェクトをスタンプするのにラベルを使用する必要があります。 したがって、インデックス作成、する前に、すべての変更がデータベースにチェックインされ、プロジェクトにラベルを適用を確認する必要があります。 コマンドを使用して、ラベルを適用できます。

```console
ss.exe label Project
```

場所*プロジェクト*現在のプロジェクトを示します。

次の例では、ラベル"バージョン\_3""$/sdktools"と呼ばれるプロジェクトに適用されます。

```console
E:\nt\user>ss.exe label $/sdktools
 Label for $/sdktools: VERSION_3
 Comment for $/sdktools:
 This is a comment.
```

ラベルが適用された後、SSLABEL、環境変数を設定して、または次の例のように、コマンド ライン パラメーターとして渡すことによって、スクリプトをインデックス作成 SrcSrv するこのラベルを指定できます。

```console
vssindex.cmd -label=VERSION_3
```

ここでも、このラベルは SrcSrv させるインデックス作成に必要です。 プロジェクトに存在しないラベルを渡した場合、スクリプトが完了する時間がかかることができ、結果が使用されない場合は注意してください。

### <a name="span-idcredentialsspanspan-idcredentialsspancredentials"></a><span id="credentials"></span><span id="CREDENTIALS"></span>資格情報

Visual SourceSafe データベースは、アクセスのユーザーと省略可能なパスワードを必要とする場合、使用および SSPWD 環境変数を介してこれらの値を設定する必要があります。 これは、ビルドのインデックスを作成時にだけでなく、デバッガーのクライアントにも適用されます。

 

 





