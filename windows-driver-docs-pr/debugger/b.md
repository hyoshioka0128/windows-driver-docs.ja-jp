---
title: B (Windows デバッガーの用語集)
description: 用語集ページ - B
Robots: noindex, nofollow
ms.assetid: 5ba110fc-1a12-4cbd-adc9-ef9441e257cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23a9888c606525e9611a88f8fae4087c9ba0ceb7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570645"
---
# <a name="b"></a>B


<span id="blue_screen"></span><span id="BLUE_SCREEN"></span>**ブルー スクリーン**  
バグ チェックが行われた後に表示される青い文字モード画面。

<span id="breakpoint"></span><span id="BREAKPOINT"></span>**ブレークポイント**  
ターゲットまたはターゲットの操作がトリガーされたときにイベントを発生する場所です。

詳細については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。

<span id="breakpoint_id"></span><span id="BREAKPOINT_ID"></span>**ブレークポイントの ID**  
ブレークポイントの一意の識別子。

詳細については、[を使用してブレークポイント](using-breakpoints.md)を参照してください。

<span id="breakpoint_type"></span><span id="BREAKPOINT_TYPE"></span>**ブレークポイントの種類**  
ブレークポイントを実装するために使用するメソッド。 ブレークポイントの 2 種類があります。 プロセッサ ブレークポイントとブレークポイントのソフトウェア。

<span id="break_status"></span><span id="BREAK_STATUS"></span>**中断状態**  
デバッガー エンジンのイベントの後に続行方法に影響する設定です。 中断状態では、デバッガーのコンソール出力に通知があるイベントは、デバッガーを中断する必要があります、かどうかを示すか、無視されます。 中断状態には、イベント フィルターの一部です。

参照してください[*処理ステータス*](h.md#handling-status)します。

詳細については、トピックを参照してください。[を制御する例外とイベント](controlling-exceptions-and-events.md)と[イベント フィルター](event-filters.md)します。

<span id="bug_check"></span><span id="BUG_CHECK"></span>**バグ チェック**  
Windows ハードウェアの問題、その操作、またはその他の重大なエラーを必要となるデータ内で不整合が発生したときにシャット ダウンされ、キャラクター モードのブルー スクリーンにエラー情報が表示されます。

このシャット ダウンの既知のバグ チェック、カーネルのエラー、システムのクラッシュ、stop エラーの場合は、さまざまなや、場合によっては、トラップします。 画面自体がブルー スクリーンや停止画面と呼ばれます。 画面上に表示される最も重要な情報は、クラッシュ; に関する情報を提供するメッセージ コードです。これは、バグの確認コードまたは停止コードと呼ばれます。

WinDbg、KD または、デバッガーは、このようなエラーが発生したときに自動的に接続できるようにシステムを構成することができます。 または、このようなエラーが発生した場合に自動的に再起動する、システムに指示できます。

詳細については、「[Bug Checks (Blue Screens)](bug-checks--blue-screens-.md)」(バグ チェック (ブルー スクリーン)) を参照してください。

<span id="bug_check_code"></span><span id="BUG_CHECK_CODE"></span>**バグ チェック コード**  
バグの特定の種類を示す 16 進コードを確認します。

 

 





