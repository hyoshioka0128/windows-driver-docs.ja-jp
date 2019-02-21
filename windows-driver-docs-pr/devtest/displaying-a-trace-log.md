---
title: トレース ログを表示します。
description: トレース ログを表示します。
ms.assetid: c60c801a-6128-43d6-a435-4537c597177f
keywords:
- トレース ログは、WDK traceview で表示します。
- Traceview で WDK、ログを表示します。
- トレース ログを表示します。
- ログ ファイルの WDK traceview で表示します。
- イベント トレース ログは、WDK
- .etl ファイル
- etl ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3687f2b7aaa26d058684d92ffa006113ddeb5e6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559342"
---
# <a name="displaying-a-trace-log"></a>トレース ログを表示します。


Traceview でを使用すると、すべてのコンテンツを表示[イベント トレース ログ (.etl) ファイル](trace-level.md)(とも呼ばれる、*トレース ログ*)、traceview でを使用して生成されたイベント トレース ログ ファイルを含むです。

については、配置することにより traceview でに提供できるを書式設定がすべてのトレース ログを表示する必要のある、 [PDB シンボル ファイル](pdb-symbol-files.md)(.pdb)、[トレース メッセージの形式 (.tmf) ファイル](trace-message-format-file.md)、または TMF ファイルへのパストレース メッセージ。

トレース ログを表示するには、中にグループ化しトレース ログをグループ化解除、新しいトレース ログ ファイルを生成でき他の形式で表示するためのトレース メッセージをコピーできます。

このセクションの内容:

[PDB ファイルを使用してトレース ログを表示します。](displaying-a-trace-log-with-a-pdb-file.md)

[TMF ファイルを使用してトレース ログを表示します。](displaying-a-trace-log-with-a-tmf-file.md)

[トレース ログ オプションの設定](setting-trace-log-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview では、PDB ファイル、TMF ファイルまたはトレース ログの内容を表示する TMF ディレクトリが必要です。 Traceview では % トレースを使用しない\_形式\_検索\_%path% 環境変数。

トレース セッションの名前は保存されず、イベント トレース ログ (.etl) ファイルまたは、traceview でファイルまたはファイルの概要を出力します。 Traceview でを使用してトレース ログを表示するときに、既定のセッション名を使用して **LogSession * * * N*、トレース セッションの名前として (場所*N*順序を表す 0 から始まる整数が、セッションが作成されます)。

 

 





