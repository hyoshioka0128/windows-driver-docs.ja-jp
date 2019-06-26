---
title: イベントの監視
description: イベントの監視
ms.assetid: f0381cf9-e568-4789-af08-69d8b2c3ecbf
keywords:
- デバッガー エンジン イベント
- イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70567197d721b5ea5dba8fddbab7eebb6983f867
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366460"
---
# <a name="monitoring-events"></a>イベントの監視


## <span id="ddk_monitoring_events_dbx"></span><span id="DDK_MONITORING_EVENTS_DBX"></span>


内のイベントの概要については、[デバッガー エンジン](introduction.md#debugger-engine)を参照してください[イベント](events.md)します。

使用して、ターゲットまたはデバッガー エンジンで発生するイベントを監視することがあります、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイス。 **IDebugEventCallbacks**クライアントを使用したオブジェクトが登録されて[ *SetEventCallbacks*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)します。 各クライアントでは 1 つだけができますのみ**IDebugEventCallbacks**登録されるオブジェクト。

ときに、 **IDebugEventCallbacks**オブジェクトがクライアントに登録されている、エンジンはオブジェクトの呼び出しは[ **IDebugEventCallbacks::GetInterestMask** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-getinterestmask)判断するためにイベント オブジェクトに関心があります。 オブジェクトが必要とするイベントのみに送信されます。

イベントの種類ごとに、エンジンはの対応するコールバック メソッドを呼び出す[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)します。 ターゲットからのイベント、 [**デバッグ\_状態\_XXX** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-status-xxx)これらの呼び出しから返される値は、ターゲットの実行を続ける方法を指定します。 エンジンは、それぞれからこれらの戻り値を収集します**IDebugEventCallbacks**オブジェクトと呼び出しの優先順位が最も高いものは機能します。

### <a name="span-ideventsfromthetargetthatbreakintothedebuggerbydefaultspanspan-ideventsfromthetargetthatbreakintothedebuggerbydefaultspanevents-from-the-target-that-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>既定ではデバッガーに割り込むターゲットからのイベント

次のイベントは、既定では、デバッガーに割り込みます。

-   ブレークポイント イベント

-   (ここで説明しませんが) 例外イベント

-   システム エラー

### <a name="span-ideventsfromthetargetthatdonotbreakintothedebuggerbydefaultspanspan-ideventsfromthetargetthatdonotbreakintothedebuggerbydefaultspanevents-from-the-target-that-do-not-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_do_not_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_DO_NOT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>既定では、デバッガーに割り込みを行わないはターゲットからのイベント

次のイベントは、既定ではデバッガーに割り込んでいないは。

-   プロセス イベントを作成します。

-   終了プロセスのイベント

-   スレッドのイベントを作成します。

-   終了スレッド イベント

-   読み込みモジュール イベント

-   アンロード モジュール イベント

### <a name="span-idinternalenginechangesspanspan-idinternalenginechangesspaninternal-engine-changes"></a><span id="internal_engine_changes"></span><span id="INTERNAL_ENGINE_CHANGES"></span>内部エンジンの変更

次は実際のイベントがだけで内部エンジンの変更します。

-   ターゲットの変更

-   エンジンの変更

-   エンジンのシンボルの変更

-   セッション状態の変更

 

 





