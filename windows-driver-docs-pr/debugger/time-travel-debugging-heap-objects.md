---
title: TTD ヒープ オブジェクト
description: このセクションでは、タイム トラベルのデバッグに関連付けられているヒープ モデル オブジェクトについて説明します。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29bbd1e05ed966095eebff5655db0e72c885592f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528778"
---
# <a name="ttd-heap-objects"></a>TTD ヒープ オブジェクト
## <a name="description"></a>説明
*TTD ヒープ*オブジェクトを使用して、トレースの過程で発生するヒープ呼び出しに関する情報を提供します。


## <a name="properties"></a>プロパティ
ヒープのすべてのオブジェクトには、これらのプロパティがあります。

| プロパティ | 説明 |
| --- | --- |
| アクション | 発生したアクションをについて説明します。 設定可能な値は、次のとおりです。アロケーション、ReAlloc、Free、作成、保護、ロック、ロックを解除、破棄します。 |
| ヒープ | Win32 ヒープのハンドル。 |

### <a name="conditional-properties"></a>条件付きのプロパティ
ヒープ オブジェクトに応じて次のプロパティの一部があります。

| プロパティ | 説明 |
| --- | --- |
| Address | 割り当てられたオブジェクトのアドレス。 |
| PreviousAddress | そのが再割り当てされる前に、割り当てられたオブジェクトのアドレス。 アドレスがない PreviousAddress と同じ場合は、再割り当てに移動するメモリが原因。 |
| サイズ | サイズやオブジェクトの割り当て済みの要求されたサイズ。 |
| BaseAddress | ヒープで割り当てられたオブジェクトのアドレス。  アドレスを表すことができます (無料) を解放は、前にオブジェクトのアドレスが再割り当て (再割り当てします)。 |
| フラグ | 意味は、API によって異なります。 |
| 結果 | ヒープの API の結果を呼び出します。 成功を 0 以外の値の意味と 0 個の障害を意味します。 |
| ReserveSize | ヒープ用に予約するメモリの量。 |
| CommitSize | ヒープの初期コミット サイズです。 |
| MakeReadOnly | 0 以外の値を読み取り専用ヒープに要求を示します値が 0 では、ヒープが読み取り/書き込みをする必要がありますを示します。 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| TimeStart | A[位置オブジェクト](time-travel-debugging-position-objects.md)割り当ての開始位置をについて説明します。 |
| 時刻終了 | A[位置オブジェクト](time-travel-debugging-position-objects.md)割り当ての末尾に位置するについて説明します。 |


## <a name="example-usage"></a>使用例

-G オプションを使用して、グリッドにヒープのメモリを表示するのにには、この dx コマンドを使用します。

```dbgcmd
0:0:000> dx -g @$cursession.TTD.Data.Heap()
==================================================================================================================================
=           = (+) Function               = (+) FunctionAddress = (+) ReturnValue  = (+) Parameters = (+) TimeStart = (+) TimeEnd =
==================================================================================================================================
= [0x0]     - UnknownOrMissingSymbols    - 0x7ffbe3daae00      - 0x16c7d7b4050    - {...}          - 50C74:8E      - 50C76:3B    =
= [0x1]     - UnknownOrMissingSymbols    - 0x7ffbe3db0dd0      - 0x1              - {...}          - 50C76:1E9     - 50C78:1D    =
= [0x2]     - UnknownOrMissingSymbols    - 0x7ffbe3daae00      - 0x16c7d7be400    - {...}          - 51C95:21F3    - 51CA6:81    =
```


出力は、選択したヒープ操作を表す Api のセットがあるため、「正規化されたデータ」として記述できます。 適切なパラメーターから抽出されたデータは、一貫した方法で表示されます。

TimeStart または時刻終了 をクリックと、トレースには、そのポイントにする移動はします。  

使用可能なパラメーター情報を表示する特定のエントリの横にあるパラメーターのフィールドをクリックします。

```dbgcmd
dx -r1 @$cursession.TTD.Data.Heap()[2].@"Parameters"
@$cursession.TTD.Data.Heap()[2].@"Parameters"                
    [0x0]            : 0x16c7d780000
    [0x1]            : 0x280000
    [0x2]            : 0x20
    [0x3]            : 0x0
```





## <a name="see-also"></a>参照

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


