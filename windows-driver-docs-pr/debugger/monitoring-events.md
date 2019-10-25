---
title: イベントの監視
description: イベントの監視
ms.assetid: f0381cf9-e568-4789-af08-69d8b2c3ecbf
keywords:
- デバッガーエンジン, イベント
- イベント
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecdd53b4fc34175c9f335b8aebcbd7f5d5e14c8a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834327"
---
# <a name="monitoring-events"></a>イベントの監視


## <span id="ddk_monitoring_events_dbx"></span><span id="DDK_MONITORING_EVENTS_DBX"></span>


[デバッガーエンジン](introduction.md#debugger-engine)でのイベントの概要については、「 [events](events.md)」を参照してください。

ターゲットまたはデバッガーエンジンで発生するイベントは、 [IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイスを使用して監視できます。 **IDebugEventCallbacks**オブジェクトは、 [*seteventcallbacks バック*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-seteventcallbacks)を使用してクライアントに登録できます。 各クライアントに登録できる**IDebugEventCallbacks**オブジェクトは1つだけです。

**IDebugEventCallbacks**オブジェクトがクライアントに登録されると、エンジンはオブジェクトの[**IDebugEventCallbacks:: GetInterestMask**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-getinterestmask)を呼び出して、オブジェクトが関心を持っているイベントを特定します。 オブジェクトが関心のあるイベントのみが送信されます。

エンジンは、イベントの種類ごとに、対応するコールバックメソッドを[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugeventcallbacks)で呼び出します。 ターゲットからのイベントの場合、これらの呼び出しから返される[**DEBUG\_STATUS\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-status-xxx)値は、ターゲットの実行を続行する方法を指定します。 エンジンは、呼び出された各**IDebugEventCallbacks**オブジェクトからこれらの戻り値を収集し、優先順位が最も高いものを処理します。

### <a name="span-idevents_from_the_target_that_break_into_the_debugger_by_defaultspanspan-idevents_from_the_target_that_break_into_the_debugger_by_defaultspanevents-from-the-target-that-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>既定でデバッガーに中断するターゲットからのイベント

既定では、次のイベントがデバッガーに分割されます。

-   ブレークポイントイベント

-   例外イベント (ここでは説明されていません)

-   システム エラー

### <a name="span-idevents_from_the_target_that_do_not_break_into_the_debugger_by_defaultspanspan-idevents_from_the_target_that_do_not_break_into_the_debugger_by_defaultspanevents-from-the-target-that-do-not-break-into-the-debugger-by-default"></a><span id="events_from_the_target_that_do_not_break_into_the_debugger_by_default"></span><span id="EVENTS_FROM_THE_TARGET_THAT_DO_NOT_BREAK_INTO_THE_DEBUGGER_BY_DEFAULT"></span>既定でデバッガーに中断されないターゲットからのイベント

既定では、次のイベントはデバッガーに分割されません。

-   プロセスイベントの作成

-   プロセスの終了イベント

-   スレッドイベントの作成

-   スレッドイベントの終了

-   モジュールイベントの読み込み

-   モジュールイベントのアンロード

### <a name="span-idinternal_engine_changesspanspan-idinternal_engine_changesspaninternal-engine-changes"></a><span id="internal_engine_changes"></span><span id="INTERNAL_ENGINE_CHANGES"></span>内部エンジンの変更

次に示すのは実際のイベントではありませんが、単なる内部エンジンの変更です。

-   ターゲットの変更

-   エンジンの変更

-   エンジンシンボルの変更

-   セッション状態の変更

 

 





