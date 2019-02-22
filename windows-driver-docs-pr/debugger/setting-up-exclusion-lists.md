---
title: 除外リストを設定します。
description: 除外リストを設定します。
ms.assetid: 0b50e8a6-f68c-43e5-b8d5-4b2c40252d38
keywords:
- SymProxy、除外リスト
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59e2ed0d6c3b2e7cd06779dc7cabae84c310cf9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550031"
---
# <a name="setting-up-exclusion-lists"></a>除外リストを設定します。


一部の環境では、自分でデバッグ シンボルを取得することはできませんを大量に読み込まれたモジュールを搭載したシステムを見つける可能性があります。 サード パーティ ベンダーによって呼び出されるコードがある場合は多くの場合、ケースになります。 これは、時間がかかるうえ、ネットワーク リソースに負荷が多く、シンボルを検索する試行失敗の結果します。 この問題を軽減するを使用できます、*除外リスト*検索から除外するシンボルを指定します。 クライアントのデバッガーでこの機能が存在しますも独自に使用する SymProxy フィルターを構成するには、除外リストと、リソースを占有する可能性が、このようなネットワーク アクティビティを防ぐことができます。

処理されないようにファイルの名前の除外一覧が構成されます。 ファイル名には、ワイルドカードを含めることができます。 次に、例を示します。

```console
dbghelp.pdb
symsrv.*
mso*
```

一覧は、2 つの方法で実装できます。 1 つは、.ini ファイルを %windir% で\\system32\\inetsrv\\Symsrv.ini します。 「除外」という名前のセクションでは、リストを含める必要があります。

```console
[exclusions]
dbghelp.pdb
symsrv.*
mso*
```

または、レジストリで、除外リストを格納できます。 という名前のキーを作成します。

```text
HKLM\ Software\Microsoft\Symbol Server\Exclusions
```

文字列値としてファイル名の一覧を格納 (REG\_SZ) このキー内で。 文字列値の名前は、除外するファイル名として機能します。 文字列値の内容は、ファイルが除外されている理由を説明するコメントとして使用できます。

SymProxy を読み取り、除外リストから 30 分ごとを有効にするための変更を表示する Web サービスを再起動する必要はありません。 レジストリまたは .ini ファイルの一覧にファイルを追加し、除外するための短い期間を待機します。

**注**   SymProxy が Symsrv.ini とレジストリの使用をサポートしていません。 .Ini ファイルが存在する場合に使用されます。 それ以外の場合、レジストリをチェックします。

 

 

 





