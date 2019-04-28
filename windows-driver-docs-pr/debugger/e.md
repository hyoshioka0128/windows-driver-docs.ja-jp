---
title: E (Windows デバッガーの用語集)
description: 用語集ページ - E
Robots: noindex, nofollow
ms.assetid: 1e32bd40-8c77-4c6b-913c-6ec26707ed36
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb7fe4c28beb6985435d191da4eb8370843d77c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378480"
---
# <a name="e"></a>E


<span id="effective_processor_type"></span><span id="EFFECTIVE_PROCESSOR_TYPE"></span>**有効なプロセッサの種類**  
プロセッサの種類、デバッガーは、対象のコンピュータを扱うときに使用します。 有効なプロセッサの種類は、どのデバッガー ブレークポイントを設定します、レジスタにアクセス、スタック トレースを取得およびその他のプロセッサに固有の操作を実行しますに影響します。

<span id="engine"></span><span id="ENGINE"></span>**エンジン**  
デバッガー エンジンを参照してください。

<span id="event"></span><span id="EVENT"></span>**イベント**  
デバッガー エンジンは、いくつかのターゲットで発生するイベントを監視します。 トリガーされるブレークポイント、例外、スレッドとプロセスの作成、モジュールの読み込み、および内部デバッガー エンジンの変更が含まれます。

<span id="event_filter"></span><span id="EVENT_FILTER"></span>**イベント フィルター**  
デバッガー エンジンがターゲットのイベントが発生した後に続行方法に影響する規則のコレクション。 イベント フィルターの 3 つの種類があります。 特定のイベントのフィルター、特定の例外フィルター、および任意の例外フィルター。

<span id="event_callback_objects"></span><span id="EVENT_CALLBACK_OBJECTS"></span>**イベントのコールバック オブジェクト**  
インスタンス、 [IDebugEventCallbacks](https://msdn.microsoft.com/library/windows/hardware/ff550550)クライアントに登録されているインターフェイス。 エンジンは、イベントが発生するイベントのコールバックを通知します。

<span id="event_callbacks"></span><span id="EVENT_CALLBACKS"></span>**イベントのコールバック**  
イベントのコールバック オブジェクトを参照してください。

<span id="event_process"></span><span id="EVENT_PROCESS"></span>**イベント処理**  
最後のイベントが発生したプロセスです。

<span id="event_target"></span><span id="EVENT_TARGET"></span>**イベント ターゲット**  
最後のイベントが発生したターゲット。

<span id="event_thread"></span><span id="EVENT_THREAD"></span>**イベントのスレッド**  
最後のイベントが発生したスレッドです。

<span id="executing_processor_type"></span><span id="EXECUTING_PROCESSOR_TYPE"></span>**プロセッサの種類を実行します。**  
プロセッサの現在のコンテキストでプロセッサの種類。

<span id="exception"></span><span id="EXCEPTION"></span>**exception**  
特定のマシン命令の実行から、またはエラーが発生したことを示す、ターゲットからの結果としてエラー条件。 例外は、ハードウェアまたはソフトウェアに関連するエラーを指定できます。

例外で識別されると、します。

<span id="exception_code"></span><span id="EXCEPTION_CODE"></span>**例外コード**  
例外イベントの種類を決定するための識別子です。

<span id="exception_filter"></span><span id="EXCEPTION_FILTER"></span>**例外フィルター**  
例外コードで指定された例外イベントのイベント フィルター。

<span id="extension"></span><span id="EXTENSION"></span>**拡張機能**  
デバッガーの拡張機能を参照してください。

<span id="extension_command"></span><span id="EXTENSION_COMMAND"></span>**拡張機能コマンド**  
デバッガーの拡張機能を参照してください。

 

 





