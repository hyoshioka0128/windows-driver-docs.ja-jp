---
title: S (Windows デバッガーの用語集)
description: 用語集ページ - S
Robots: noindex, nofollow
ms.assetid: 94cbf33b-e975-49eb-a266-774798955a48
keywords:
- 中断されたスレッド
- 中断されたプロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c583ab9cf7b5c6c1bbd8244d028ce2667b026ce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366407"
---
# <a name="s"></a>S


<span id="scope"></span><span id="SCOPE"></span>**スコープ**  
ローカル変数を定義するコンテキスト。 スコープが 3 つのコンポーネント: スタック フレームを現在の命令およびレジスタのコンテキスト。

呼ば*ローカル コンテキスト*または*構文のスコープ*します。

<span id="second_chance_exception"></span><span id="SECOND_CHANCE_EXCEPTION"></span>**次の例外**  
例外を処理する 2 番目のチャンスです。 この機会が提供されるは、ファースト チャンスでは、例外が処理しない場合のみです。

<span id="smart_client"></span><span id="SMART_CLIENT"></span>**スマート クライアント**  
ホストとして機能するデバッガー エンジンのインスタンス。 スマート クライアントは、プロセス サーバーに接続されます。 または、KD、接続サーバー。

<span id="specific_exception_filter"></span><span id="SPECIFIC_EXCEPTION_FILTER"></span>**特定の例外フィルター**  
エンジンが組み込みフィルター例外イベント フィルター。 最も固有の例外フィルターは、特定の種類の例外 (例外コードによって識別される) を参照してくださいが特定の例外フィルターとしても既定の例外フィルターを修飾します。

<span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>**特定のイベント フィルター**  
例外ではないイベントのイベント フィルター。 特定のイベントのフィルターは、「 [**デバッグ\_フィルター\_XXX**](https://docs.microsoft.com/windows-hardware/drivers/debugger/debug-filter-xxx)します。

<span id="specific_filter"></span><span id="SPECIFIC_FILTER"></span>**特定のフィルター**  
エンジンが組み込みのフィルター、イベントのイベント フィルター。

<span id="software_breakpoint"></span><span id="SOFTWARE_BREAKPOINT"></span>**ソフトウェアのブレークポイント**  
デバッガーによって実装されているブレークポイント エンジンのターゲットの実行可能コードを一時的に変更します。 コードが実行されたときに、ブレークポイントがトリガーされます。 コードの変更では、デバッガーやデバッガー エンジン API のユーザーに表示されません。

<span id="stack"></span><span id="STACK"></span>**スタック**  
参照呼び出し履歴。

<span id="stack_frame"></span><span id="STACK_FRAME"></span>**スタック フレーム**  
1 つの関数呼び出しのデータを含むコール スタックのメモリ。 これには、戻り値のアドレスでは、関数、およびローカル変数に渡されるパラメーターが含まれます。

<span id="stop_code"></span><span id="STOP_CODE"></span>**停止コード**  
バグ チェック コードを参照してください。

<span id="stop_error"></span><span id="STOP_ERROR"></span>**停止エラー**  
バグの確認を参照してください。

<span id="stop_screen"></span><span id="STOP_SCREEN"></span>**画面を停止します。**  
ブルー スクリーンを参照してください。

<span id="subregister"></span><span id="SUBREGISTER"></span>**subregister**  
別のレジスタ内に含まれる登録します。 Subregister の変更、subregister を格納するレジスタの部分も変更されたとき。

<span id="suspended"></span><span id="SUSPENDED"></span>**中断**  
ターゲット、プロセス、またはスレッドが中断された場合、実行をブロックします。

<span id="symbol"></span><span id="SYMBOL"></span>**シンボル**  
デバッグ、デバッグ セッションで、ターゲットの解釈型情報を提供する情報の単位です。 シンボルの例には、変数 (ローカルおよびグローバル) 関数、型および関数のエントリが含まれます。 シンボルに関する情報は、名前、型 (存在する場合)、およびアドレスまたは regisgter 格納場所だけでなく、親または子のシンボルを含めることができます。 この情報は、シンボル ファイルに格納され、通常は、モジュール自体では使用できません。

デバッガー エンジンは、シンボル ファイルは使用できません (たとえば、エクスポートされたシンボル)、これらのシンボルは一般に最小限の情報を提供する場合、特定の記号を合成することができます。

<span id="symbol_file"></span><span id="SYMBOL_FILE"></span>**シンボル ファイル**  
補足ファイルは、アプリケーション、ライブラリ、ドライバー、またはオペレーティング システムの構築時に作成します。 シンボル ファイルには、これは実際には必要ありません、バイナリの実行時に、これは、デバッグ プロセスで非常に有用ですが、データが含まれています。

<span id="symbol_group"></span><span id="SYMBOL_GROUP"></span>**シンボルのグループ**  
一般に、スコープ内のすべてのローカル変数を表すシンボルのグループ。

<span id="symbol_type"></span><span id="SYMBOL_TYPE"></span>**記号の型**  
メモリ内のレイアウトなどのシンボルの表現についての説明。 これは、コンパイラがシンボルを操作するコードの生成に使用する情報の一部です。 シンボルを操作するデバッガー エンジンによっても使用されます。 記号の型は、シンボル ファイルで分散されます。

<span id="synthetic_module"></span><span id="SYNTHETIC_MODULE"></span>**統合モジュール**  
エンジンは、モジュールと同様に扱われるメモリの領域。 統合モジュールには、合成のシンボルが含まれている可能性があります。

<span id="synthetic_symbol"></span><span id="SYNTHETIC_SYMBOL"></span>**合成のシンボル**  
記号のようなエンジンが扱われるメモリ アドレス。

<span id="system_crash"></span><span id="SYSTEM_CRASH"></span>**システムのクラッシュ**  
バグの確認を参照してください。

 

 





