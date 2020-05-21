---
title: 除外一覧の設定
description: 除外一覧の設定
ms.assetid: 0b50e8a6-f68c-43e5-b8d5-4b2c40252d38
keywords:
- SymProxy、除外リスト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 908d875e40f19fdf0ff547971066f420bf17a4a4
ms.sourcegitcommit: 1b77487f8ef5dcf8219df05524e322c27f9dcad8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83707705"
---
# <a name="setting-up-exclusion-lists"></a>除外一覧の設定


環境によっては、シンボルを取得できない多数のモジュールが読み込まれたシステムをデバッグしている場合があります。 これは、サードパーティベンダーから呼び出されたコードがある場合によく発生します。 これにより、多くの場合、シンボルの検索に失敗することがあります。これは、時間がかかり、ネットワークリソースをログに記録するためです。 このような状況を軽減するには、*除外リスト*を使用して、検索から除外するシンボルを指定します。 この機能はクライアントデバッガーに存在しますが、独自の除外リストを使用するように SymProxy フィルターを構成し、リソースを占有する可能性が最も高いネットワークアクティビティを防ぐこともできます。

除外リストは、処理を禁止するファイルの名前で構成されます。 ファイル名にはワイルドカードを含めることができます。 たとえば、次のように入力します。

```console
dbghelp.pdb
symsrv.*
mso*
```

この一覧は、次の2つの方法で実装できます。 1つ目は、.ini ファイル (% WINDIR% \\ system32 \\ inetsrv config administration.config) \\ にあります。 "除外" という名前のセクションには、次の一覧が含まれている必要があります。

```console
[exclusions]
dbghelp.pdb
symsrv.*
mso*
```

または、除外をレジストリに格納することもできます。 という名前のキーを作成します。

```text
HKLM\Software\Microsoft\Symbol Server\Exclusions
```

このキー内にファイル名リストを文字列値 (REG SZ) として格納し \_ ます。 文字列値の名前は、除外するファイル名として機能します。 文字列値の内容は、ファイルが除外されている理由を説明するコメントとして使用できます。

SymProxy は、30分ごとに除外リストから読み取りを行い、変更を反映するために Web サービスを再起動する必要がないようにします。 レジストリまたは .ini ファイルの一覧にファイルを追加し、除外が使用されるまで短い期間待機します。

**メモ**   SymProxy は、Symproxy .ini とレジストリの両方の使用をサポートしていません。 .Ini ファイルが存在する場合は、それが使用されます。 それ以外の場合は、レジストリがチェックされます。

 

 

 





