---
title: トレース セッションの作成
description: トレース セッションの作成
ms.assetid: 26f75b02-d830-4e3c-bbc9-03144d194e05
keywords:
- WDK のリアルタイムのトレース セッション
- WDK のトレース ログ セッション
- Traceview で WDK、セッションを作成します。
- WDK、セッションのトレースを作成します。
- セッションの WDK ソフトウェア トレース
- ソフトウェア トレース WDK、セッションの作成
- トレース WDK、セッションの作成
- トレース ログ WDK traceview で、セッション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b16a8986a75df60548ef75b1d9cdf7efc2f18ed
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381015"
---
# <a name="creating-a-trace-session"></a>トレース セッションの作成


## <span id="ddk_creating_a_real_time_trace_session_tools"></span><span id="DDK_CREATING_A_REAL_TIME_TRACE_SESSION_TOOLS"></span>


このセクションでは、traceview でを使用して、リアルタイムのトレース セッションまたはトレース ログ セッションを作成する方法について説明します。

ときにする*作成*、[トレース セッション](trace-session.md)、traceview では、構成しトレース セッションを開始し、により、[トレース プロバイダー](trace-provider.md)でプロバイダーなど、指定した、イベント トレース用にインストルメント化はドライバー。

Traceview では、ウィザードのページを使用してトレース セッションを作成する手順について説明します。

Traceview では、トレース セッションを作成するときに、少なくとも 1 つのトレース プロバイダーを指定することが必要です。 プロバイダーの種類と使用可能なファイルを使用してトレース セッションを作成する方法が決まります。

このセクションの内容:

[PDB ファイルを使用してトレース セッションを作成します。](creating-a-trace-session-with-a-pdb-file.md)

[CTL ファイルを使用してトレース セッションを作成します。](creating-a-trace-session-with-a-ctl-file.md)

[コントロールの GUID を持つトレース セッションを作成します。](creating-a-trace-session-with-a-control-guid.md)

[登録済みのプロバイダーのトレース セッションを作成します。](creating-a-trace-session-for-a-registered-provider.md)

[NT Kernel Logger トレース セッションの作成](creating-an-nt-kernel-logger-trace-session.md)

[トレース セッションに参加します。](joining-a-trace-session.md)

[トレース プロバイダーの削除](removing-a-trace-provider.md)

[基本的なトレース セッション オプションの設定](setting-basic-trace-session-options.md)

[フラグとレベルを選択します。](selecting-flags-and-levels.md)

[設定の詳細トレース セッションのオプション](setting-advanced-trace-session-options.md)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Traceview でが必要です、 [PDB シンボル ファイル](pdb-symbol-files.md)、[トレース メッセージの形式 (TMF) ファイル](trace-message-format-file.md)、またはトレース セッションを作成するときに、TMF ディレクトリ。 Traceview では % トレースを使用しない\_形式\_検索\_%path% 環境変数。

限りウィンドウは開いたままに、トレース セッションの実行、トレース セッションを作成するのに traceview でウィンドウを使用する場合。 ウィンドウを閉じて、実行されているセッションのままにすることはできません。 Traceview でウィンドウとは無関係に実行しているトレース セッションを開始するには、使用、 [traceview でコマンド ライン インターフェイス](traceview-command-line-interface.md)します。

 

 





