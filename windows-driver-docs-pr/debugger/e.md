---
title: E (Windows デバッガー用語集)
description: 用語集のページ-E
ms.assetid: 1e32bd40-8c77-4c6b-913c-6ec26707ed36
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3eb798f05c3c0bf5440ff4344fbf565f6642d12
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387079"
---
# <a name="e"></a>E


<span id="effective_processor_type"></span><span id="EFFECTIVE_PROCESSOR_TYPE"></span>**有効なプロセッサの種類**  
対象のコンピューターを処理するときにデバッガーが使用するプロセッサの種類。 有効なプロセッサの種類は、デバッガーがブレークポイントを設定する方法、レジスタにアクセスする方法、スタックトレースを取得する方法、およびその他のプロセッサ固有のアクションを実行する方法に影響します。

<span id="engine"></span><span id="ENGINE"></span>**双発**  
「デバッガーエンジン」を参照してください。

<span id="event"></span><span id="EVENT"></span>**場合**  
デバッガーエンジンは、ターゲットで発生するイベントの一部を監視します。 これには、トリガーされるブレークポイント、例外、スレッドとプロセスの作成、モジュールの読み込み、および内部デバッガーエンジンの変更が含まれます。

<span id="event_filter"></span><span id="EVENT_FILTER"></span>**イベントフィルター**  
ターゲットでイベントが発生した後のデバッガーエンジンの処理方法に影響を与えるルールのコレクション。 イベントフィルターには、特定のイベントフィルター、特定の例外フィルター、任意の例外フィルターの3種類があります。

<span id="event_callback_objects"></span><span id="EVENT_CALLBACK_OBJECTS"></span>**イベントコールバックオブジェクト**  
クライアントに登録されている[IDebugEventCallbacks](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugeventcallbacks)インターフェイスのインスタンス。 イベントが発生するたびに、エンジンによってイベントコールバックが通知されます。

<span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>**イベントコールバック**  
「イベントコールバックオブジェクト」を参照してください。

<span id="event_process"></span><span id="EVENT_PROCESS"></span>**イベントプロセス**  
最後のイベントが発生したプロセス。

<span id="event_target"></span><span id="EVENT_TARGET"></span>**イベントターゲット**  
最後のイベントが発生した対象。

<span id="event_thread"></span><span id="EVENT_THREAD"></span>**イベントスレッド**  
最後のイベントが発生したスレッド。

<span id="executing_processor_type"></span><span id="EXECUTING_PROCESSOR_TYPE"></span>**実行中のプロセッサの種類**  
現在のプロセッサコンテキストでのプロセッサの種類。

<span id="exception"></span><span id="EXCEPTION"></span>**例外的**  
特定のコンピューター命令を実行した結果、またはターゲットからエラーが発生したことを示すエラー状態。 例外には、ハードウェアまたはソフトウェアに関連するエラーがあります。

例外はであり、によって識別されます。

<span id="exception_code"></span><span id="EXCEPTION_CODE"></span>**例外コード**  
例外イベントの種類を決定する識別子。

<span id="exception_filter"></span><span id="EXCEPTION_FILTER"></span>**例外フィルター**  
例外コードによって指定された例外イベントのイベントフィルター。

<span id="extension"></span><span id="EXTENSION"></span>**番号**  
「デバッガー拡張機能」を参照してください。

<span id="extension_command"></span><span id="EXTENSION_COMMAND"></span>**拡張コマンド**  
「デバッガー拡張機能」を参照してください。

 

 





