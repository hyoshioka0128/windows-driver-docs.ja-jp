---
title: NT カーネル ロガー トレース セッション
description: NT カーネル ロガー トレース セッション
ms.assetid: d805ae15-8946-4bb6-83b6-d5d31aacd456
keywords:
- WDK、NT Kernel Logger のセッションをトレースします。
- トレース セッションの NT Kernel Logger WDK
- Windows カーネル トレース プロバイダー WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8a03d693785cf574d5b11af39ab1ea9746f676b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560015"
---
# <a name="nt-kernel-logger-trace-session"></a>NT カーネル ロガー トレース セッション


NT Kernel Logger トレース セッションでは、Windows のカーネル イベントのトレースを生成します。 Windows に組み込まれている予約済みのトレース セッションです。 このトレース セッションを別々 に実行したり、ドライバーの実行中には、Windows のアクションを表示するためのドライバーのトレース中に実行できます。 [トレース プロバイダー](trace-provider.md)カーネル モード ドライバーまたはユーザー モード アプリケーションは、このトレース セッションに直接ログインできないなど、します。

予約済みのセッション名を"NT Kernel Logger"と GUID は、定数で表される、プロバイダーを使用してこのトレース セッション**SystemTraceControlGuid**します。

NT Kernel Logger セッションを作成するには使用[Tracelog](tracelog.md)または[traceview で](traceview.md)します。

NT Kernel Logger のトレース セッション中にトレース イベントの種類が、EnableFlags の値によって制御される**メンバー**イベントの\_トレース\_プロパティ構造体。 この構造体は、Microsoft Windows SDK ドキュメントで説明します。

既定では、トレース ログ、NT Kernel Logger セッションの開始時に、プロセス、スレッド、物理ディスク I/O、トレースと TCP/IP イベントを有効。 にします。 ただしを有効にするか、次の方法で特定のイベントのトレースを無効にします。

-   トレース ログ コマンド ライン パラメーターを使用します。 詳細については、[ **Tracelog コマンド構文**](tracelog-command-syntax.md)を参照してください。

-   チェック ボックスを設定して、 [traceview で](traceview.md)GUI です。

NT Kernel Logger プロバイダーは、他のトレース セッションやその他のログインできない[トレース プロバイダー](trace-provider.md) NT Kernel Logger トレース セッションにログオンできません。 使用することはできません、 **- guid**パラメーターで NT Kernel Logger トレース セッションの GUID を使用できない場合は、NT Kernel Logger のトレース セッションを開始、 **- guid**標準トレース セッションのパラメーター。

NT Kernel Logger トレース セッションからのトレース メッセージの書式を設定するには、system.tmf ファイルと共に Tracefmt を使用します。 このファイルは、WDK に含まれます。

システムの起動中のカーネル イベントをトレースするには、NT Kernel Logger のトレース セッションをシステムの起動中にトレース、グローバル ロガー トレース セッションを変換します。 詳しくは、次を参照してください[起動時のロガーのグローバルなセッション。](boot-time-global-logger-session.md)

 

 





