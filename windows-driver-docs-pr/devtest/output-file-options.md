---
title: 出力ファイルのオプション
description: 出力ファイルのオプション
ms.assetid: f53785d8-2a91-47da-945c-8c52d6345ae9
keywords:
- トレース セッション WDK、詳細オプション
- 概要メッセージ WDK traceview でをファイルします。
- WDK のファイルを一覧表示します。
- WDK traceview で出力ファイルの出力
- WDK traceview でのファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24c3fd226dc1906d7d729bfc5ac39a9a77e32ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356353"
---
# <a name="output-file-options"></a>出力ファイルのオプション


**出力ファイル** タブで、テキスト ファイルを作成することができます、[トレース セッション](trace-session.md)します。 設定し、トレース セッションを作成するときにのみ、次のオプションを変更できます。 セッションが開始した後は、これらのオプションを変更できません。

<span id="Create_Listing_File"></span><span id="create_listing_file"></span><span id="CREATE_LISTING_FILE"></span>**リスティング ファイルを作成します。**  
リアルタイムのトレース セッションから、トレース メッセージの書式設定された、読み取り可能なテキスト ファイルのバージョンを作成します。 または、[トレース ログ](trace-log.md)します。

関連付けられているテキスト ボックスで、リスティング ファイルのパスとファイル名を入力します。 既定値は LogSession*N*.out、ローカルのディレクトリ場所*N*セッションが作成された順序を表す 0 から始まる整数します。

<span id="Create_Summary_File"></span><span id="create_summary_file"></span><span id="CREATE_SUMMARY_FILE"></span>**概要ファイルを作成します。**  
リアルタイムのトレース セッションやトレース ログの統計情報のテキスト ファイルを生成します。

関連付けられているテキスト ボックスで、概要ファイルのパスとファイル名を入力します。 既定値は LogSession*N*.sum、ローカルのディレクトリ場所*N*セッションが作成された順序を表す 0 から始まる整数します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

これらのオプションは、トレース セッションのグループに、トレース セッションを含める場合でも作成する場合は、トレース セッションにのみ適用されます。 グループ内のトレース セッションでは、そのトレース セッションのオプションは共有しないでください。

既存の出力または概要ファイルのパスとファイル名を指定する場合、traceview では、警告なしには、そのファイルを上書きします。

Traceview では、トレース セッションを停止すると、概要ファイルを作成します。 Traceview でウィンドウを閉じるには、トレース セッションを停止する前に場合、traceview では、セッションの概要ファイルを作成できません。

 

 





