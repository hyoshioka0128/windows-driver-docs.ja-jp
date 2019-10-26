---
title: タイムトラベルナビゲーションコマンド
description: ここでは、タイムトラベルナビゲーションコマンドについて説明します。
ms.date: 09/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb47543b30234a31feff4e9bafc1ed929cb3775
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916191"
---
# <a name="time-travel-navigation-commands"></a>タイムトラベルナビゲーションコマンド

![時計を示す短いタイムトラベルロゴ](images/ttd-time-travel-debugging-logo.png)

ここでは、タイムトラベルナビゲーションコマンドについて説明します。

## <a name="spanspan-idpspan-p--step-back"></a></span><span id="P"></span> p-(ステップバック)

*P*コマンドは、前の1つの命令またはソース行を実行します。 サブルーチン呼び出しまたは割り込みが発生すると、1つのステップとして扱われます。 このコマンドは、WinDbg Preview の **[ホーム]** リボンの **[ステップオーバー]** ボタンを使用して呼び出すことができます。

## <a name="spanspan-idtspan-t--trace-back"></a></span><span id="T"></span> t-(トレースバック)

*T*コマンドは、前の1つの命令またはソース行を実行します。 サブルーチン呼び出しまたは割り込みが発生すると、各ステップもトレースされます。 このコマンドは、WinDbg Preview の **[ホーム]** リボンにある **[戻る]** ボタンを使用して呼び出すことができます。

## <a name="spanspan-idgospan-g--go-back"></a></span><span id="Go"></span> g-(戻る)

*G*コマンドは、現在のプロセスの実行を逆に開始します。 プログラムの終了時、BreakAddress がヒットしたとき、または別のイベントによってデバッガーが停止したときに、実行が停止します。 このコマンドは、WinDbg Preview の **[ホーム]** リボンにある **[戻る]** ボタンを使用して呼び出すことができます。

## <a name="spanspan-idadditional_informationspanadditional-information"></a>追加<span id="ADDITIONAL_INFORMATION"></span>情報の </span>

タイムトラベルナビゲーションコマンドは、タイムトラベルトレースでのみ機能します。 タイムトラベルの詳細については、「[タイムトラベルデバッグ-概要](time-travel-debugging-overview.md)」を参照してください。

## <a name="see-also"></a>参照

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

[タイムトラベルデバッグ-トレースを再生する](time-travel-debugging-replay.md)
