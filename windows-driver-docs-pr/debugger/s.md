---
title: S (Windows デバッガー用語集)
description: 用語集のページ-S
ms.assetid: 94cbf33b-e975-49eb-a266-774798955a48
keywords:
- 中断されたスレッド
- 中断されたプロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73c307d82851059f40c72c9d05a23c46b2bdb415
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387039"
---
# <a name="s"></a>S


<span id="scope"></span><span id="SCOPE"></span>**検索**  
ローカル変数を定義するコンテキスト。 スコープには、スタックフレーム、現在の命令、およびレジスタコンテキストという3つのコンポーネントがあります。

*ローカルコンテキスト*または*構文のスコープ*と呼ばれることもあります。

<span id="second_chance_exception"></span><span id="SECOND_CHANCE_EXCEPTION"></span>**セカンドチャンス例外**  
例外を処理する2番目の機会。 この機会は、例外が最初に処理されなかった場合にのみ提供されます。

<span id="smart_client"></span><span id="SMART_CLIENT"></span>**スマートクライアント**  
ホストとして動作するデバッガーエンジンのインスタンス。 スマートクライアントがプロセスサーバーに接続されている。 または KD 接続サーバー。

<span id="specific_exception_filter"></span><span id="SPECIFIC_EXCEPTION_FILTER"></span>**特定の例外フィルター**  
エンジンに組み込みフィルターがある例外のイベントフィルターです。 特に具体的な例外フィルターは、特定の種類の例外 (例外コードによって識別されます) を参照しますが、既定の例外フィルターも特定の例外フィルターとして修飾されます。

<span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>**特定のイベントフィルター**  
例外ではないイベントのイベントフィルター。 特定のイベントフィルターは、 [ **\_デバッグフィルター\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)に一覧表示されます。

<span id="specific_filter"></span><span id="SPECIFIC_FILTER"></span>**特定のフィルター**  
エンジンに組み込みフィルターがあるイベントのイベントフィルターです。

<span id="software_breakpoint"></span><span id="SOFTWARE_BREAKPOINT"></span>**ソフトウェアブレークポイント**  
ターゲットの実行可能コードを一時的に変更するデバッガーエンジンによって実装されるブレークポイント。 ブレークポイントは、コードが実行されるとトリガーされます。 コード変更は、デバッガーまたはデバッガーエンジン API のユーザーには表示されません。

<span id="stack"></span><span id="STACK"></span>**スタック**  
「呼び出し履歴」を参照してください。

<span id="stack_frame"></span><span id="STACK_FRAME"></span>**スタックフレーム**  
1つの関数呼び出しのデータを格納している呼び出し履歴内のメモリ。 これには、リターンアドレス、関数に渡されるパラメーター、およびローカル変数が含まれます。

<span id="stop_code"></span><span id="STOP_CODE"></span>**コードの停止**  
「バグチェックコード」を参照してください。

<span id="stop_error"></span><span id="STOP_ERROR"></span>**停止エラー**  
「バグチェック」を参照してください。

<span id="stop_screen"></span><span id="STOP_SCREEN"></span>**画面の停止**  
「ブルースクリーン」を参照してください。

<span id="subregister"></span><span id="SUBREGISTER"></span>**サブ登録**  
別のレジスタ内に格納されているレジスタ。 Subregister が変更されると、サブレジスタを含むレジスタの部分も変更されます。

<span id="suspended"></span><span id="SUSPENDED"></span>**状態**  
ターゲット、プロセス、またはスレッドは、実行がブロックされている場合、中断されます。

<span id="symbol"></span><span id="SYMBOL"></span>**表す**  
デバッグセッションのターゲットに関する解釈型情報を提供するデバッグ情報の単位。 シンボルの例としては、変数 (ローカルとグローバル)、関数、型、および関数のエントリがあります。 シンボルに関する情報には、名前、種類 (該当する場合)、アドレスまたは regisgter (格納場所)、および親または子のシンボルを含めることができます。 この情報はシンボルファイルに格納され、通常はモジュール自体では使用できません。

シンボルファイルが使用できない場合 (エクスポートされたシンボルなど)、デバッガーエンジンは特定のシンボルを合成できますが、これらのシンボルは一般に最小限の情報のみを提供します。

<span id="symbol_file"></span><span id="SYMBOL_FILE"></span>**シンボルファイル**  
アプリケーション、ライブラリ、ドライバー、またはオペレーティングシステムがビルドされるときに作成される補助ファイル。 シンボルファイルには、バイナリの実行時には実際には必要ではないが、デバッグプロセスで非常に便利なデータが含まれています。

<span id="symbol_group"></span><span id="SYMBOL_GROUP"></span>**シンボルグループ**  
シンボルのグループ。通常は、スコープ内のすべてのローカル変数を表します。

<span id="symbol_type"></span><span id="SYMBOL_TYPE"></span>**シンボルの種類**  
メモリ内のレイアウトなど、シンボルの表現に関する説明情報。 これは、シンボルを操作するコードを生成するためにコンパイラが使用する情報の一部です。 また、シンボルを操作するためにデバッガーエンジンによって使用されます。 シンボルの種類は、シンボルファイルで配布されます。

<span id="synthetic_module"></span><span id="SYNTHETIC_MODULE"></span>**合成モジュール**  
エンジンがモジュールとして扱うメモリの領域。 合成モジュールには、合成シンボルを含めることができます。

<span id="synthetic_symbol"></span><span id="SYNTHETIC_SYMBOL"></span>**合成シンボル**  
エンジンがシンボルとして扱うメモリアドレス。

<span id="system_crash"></span><span id="SYSTEM_CRASH"></span>**システムクラッシュ**  
「バグチェック」を参照してください。

 

 





