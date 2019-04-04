---
title: タイム トラベル ナビゲーション コマンド
description: このセクションでは、タイム トラベル ナビゲーション コマンドについて説明します。
ms.date: 09/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b07f9dbc2b5f447ad6229fd6782ed0d3e019bb9b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528097"
---
![クロックが表示された短い時間旅行ロゴ](images/ttd-time-travel-debugging-logo.png)

# <a name="time-travel-navigation-commands"></a>タイム トラベル ナビゲーション コマンド

このセクションでは、タイム トラベル ナビゲーション コマンドについて説明します。


## <a name="spanspan-idpspan-p--step-back"></a></span><span id="P"></span> p – (バックアップの手順)

*P-* コマンドは、前の 1 つの命令またはソース行を実行します。 ときにサブルーチンの呼び出しまたは割り込みが発生する、1 つのステップとして扱われます。 使用してこのコマンドを呼び出すことができます、**ステップ経由でバック**のボタンでは、**ホーム**WinDbg プレビューでリボンです。
 

## <a name="spanspan-idtspan-t--trace-back"></a></span><span id="T"></span> t-(さかのぼって)

*T-* コマンドは、前の 1 つの命令またはソース行を実行します。 ときにサブルーチンの呼び出しまたは割り込みが発生する、その手順のそれぞれにもトレースされます。 使用してこのコマンドを呼び出すことができます、**バックアップ手順に**のボタンでは、**ホーム**WinDbg プレビューでリボンです。


## <a name="spanspan-idgospan-g--go-back"></a></span><span id="Go"></span> g: (戻る)

*G-* コマンドは、逆の順序で、現在のプロセスの実行を開始します。 BreakAddress に達したら、または別のイベントにより、デバッガーを停止するときに、プログラムの最後に実行を停止します。 使用してこのコマンドを呼び出すことができます、**戻る**のボタンでは、**ホーム**WinDbg プレビューでリボンです。


## <a name="spanspan-idadditionalinformationspanadditional-information"></a></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

旅行ナビゲーション コマンドは、時間でのみ動作時間は、トレースを移動します。 タイム トラベルの詳細については、[時出張デバッグ - 概要](time-travel-debugging-overview.md)を参照してください。

## <a name="see-also"></a>参照

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

[タイム トラベル デバッグ - トレースの再生](time-travel-debugging-replay.md)

---






