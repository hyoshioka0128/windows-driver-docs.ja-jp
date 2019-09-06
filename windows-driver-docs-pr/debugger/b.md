---
title: B (Windows デバッガー用語集)
description: 用語集のページ-B
ms.assetid: 5ba110fc-1a12-4cbd-adc9-ef9441e257cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e8af541a1cb72c072cb139f6fd45e3b8fd82e10
ms.sourcegitcommit: 48c4b6d3a504583d2f588ed892a4a281d4b58301
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/06/2019
ms.locfileid: "70387059"
---
# <a name="b"></a>B


<span id="blue_screen"></span><span id="BLUE_SCREEN"></span>**ブルースクリーン**  
バグチェックが発生した後に表示される青い文字モード画面。

<span id="breakpoint"></span><span id="BREAKPOINT"></span>**ブレーク**  
イベントがトリガーされたときに発生する、ターゲットまたはターゲット操作内の場所。

詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

<span id="breakpoint_id"></span><span id="BREAKPOINT_ID"></span>**ブレークポイント ID**  
ブレークポイントの一意の識別子。

詳細については、「[ブレークポイントの使用](using-breakpoints.md)」を参照してください。

<span id="breakpoint_type"></span><span id="BREAKPOINT_TYPE"></span>**ブレークポイントの種類**  
ブレークポイントを実装するために使用されるメソッド。 ブレークポイントには、プロセッサブレークポイントとソフトウェアブレークポイントの2種類があります。

<span id="break_status"></span><span id="BREAK_STATUS"></span>**状態の中断**  
イベントの後にデバッガーエンジンがどのように動作するかに影響する設定。 ブレークステータスは、イベントがデバッガーで中断されるか、デバッガーコンソールに通知が出力されるか、または無視されるかを示します。 ブレークステータスは、イベントフィルターの一部です。

「[*処理状態*](h.md#handling-status)」も参照してください。

詳細については、[例外、イベント](controlling-exceptions-and-events.md)、[イベントフィルター](event-filters.md)の制御に関するトピックを参照してください。

<span id="bug_check"></span><span id="BUG_CHECK"></span>**バグチェック**  
Windows でハードウェアの問題が発生した場合、その操作に必要なデータの不整合や、その他の重大なエラーが発生した場合は、シャットダウンされ、青い文字モード画面にエラー情報が表示されます。

このシャットダウンは、バグチェック、カーネルエラー、システムクラッシュ、stop エラー、または場合によってはトラップとして知られています。 画面に表示される画面は、ブルースクリーンまたは停止画面と呼ばれます。 画面に表示される最も重要な情報は、クラッシュに関する情報を提供するメッセージコードです。これは、バグチェックコードまたは停止コードと呼ばれます。

WinDbg または KD では、このようなエラーが発生したときにデバッガーに自動的に接続するようにシステムを構成できます。 または、このようなエラーが発生した場合に自動的に再起動するようにシステムに指示することもできます。

詳細については、「[Bug Checks (Blue Screens)](bug-checks--blue-screens-.md)」(バグ チェック (ブルー スクリーン)) を参照してください。

<span id="bug_check_code"></span><span id="BUG_CHECK_CODE"></span>**バグチェックコード**  
特定の種類のバグチェックを示す16進数コード。

 

 





