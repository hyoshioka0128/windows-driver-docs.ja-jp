---
title: TTD オブジェクトを呼び出す
description: このセクションには、呼び出しがについて説明しますタイム トラベルのデバッグに関連するオブジェクトをモデル化します。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9300b2b472ac0a354f9e0a08f1c1f7c5d914a8de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366188"
---
# <a name="ttd-calls-objects"></a>TTD オブジェクトを呼び出す
## <a name="description"></a>説明
*TTD 呼び出し*オブジェクトを使用して、トレースの過程で発生する関数呼び出しに関する情報を提供します。

## <a name="parameters"></a>パラメーター

| プロパティ | 説明 |
| --- | --- |
| 関数。シンボル | 1 つ以上に二重引用符、コンマで区切って含まれています。 たとえば dx @$ cursession します。TTD です。呼び出し ("モジュール symbol1"、"モジュール。 symbol2",...)。 |

## <a name="properties"></a>プロパティ

| プロパティ | 説明 |
| --- | --- |
| EventType  |  イベントの種類。 これは"Call"TTD 呼び出しのすべてのオブジェクトです。 |
| スレッド Id   |  OS スレッドは、要求を作成したスレッドの ID。 |
| UniqueThreadId |   トレースの間でのスレッドの一意の ID。 プロセスの有効期間にわたって正規スレッド Id を再利用を取得できますが、UniqueThreadIds ことはできません。 |
| 関数 | 関数のシンボリック名。 |
| FunctionAddress | メモリ内の関数のアドレス。 |
| 戻り値 | 関数の戻り値。 関数が void 型の場合、このプロパティは存在できません。 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| パラメーター | 関数に渡されるパラメーターを含む配列。 要素の数は、関数の型シグネチャによって異なります。 |
| TimeStart | A[位置オブジェクト](time-travel-debugging-position-objects.md)呼び出しの開始位置をについて説明します。 |
| 時刻終了 | A[位置オブジェクト](time-travel-debugging-position-objects.md)呼び出しの最後の位置をについて説明します。 |

## <a name="remarks"></a>注釈
タイム トラベルのデバッグは、Pdb で提供されるシンボル情報を使用して、関数とその型、戻り値の型と呼び出し規則のパラメーターの数を決定します。 シンボル情報が利用できないか、シンボルは、パブリック シンボル情報が制限されていること、クエリを実行することも可能です。 タイム トラベル クエリ エンジンはこのシナリオではいくつかの想定を行います。
* 関数に次の 4 つの 64 ビット符号なし整数パラメーターがあります。
* 戻り値は 64 ビット符号なし整数です。
* 関数名は、固定文字列に設定されます。"UnknownOrMissingSymbols"

これらの前提は、適切なシンボル情報がない場合にクエリを許可します。 ただし、最適な結果を得るには、可能な場合は、完全な PDB シンボルを使用します。

呼び出し関数は、計算をトレースのサイズによって実行するときにかかることに注意してください。 CPU 使用率は、計算中にスパイクし、計算が進行していることを示す値は、タスク マネージャーでは、CPU 使用率を監視します。  クエリの結果は、照会された以前の呼び出しに対する後続のクエリが大幅に高速であるために、メモリにキャッシュされます。



## <a name="example-usage"></a>使用例

この例は ucrtbase の呼び出しオブジェクトを示します。 initterm します。

```dbgcmd
0:000> dx -r2 @$cursession.TTD.Calls("ucrtbase!initterm")
@$cursession.TTD.Calls("ucrtbase!initterm")
    [0x0]
        EventType        : Call
        ThreadId         : 0x2074
        UniqueThreadId   : 0x2
        TimeStart        : 1E:5D0
        TimeEnd          : 2D:E
        Function         : ucrtbase!_initterm
        FunctionAddress  : 0x7ffb345825d0
        ReturnAddress    : 0x7ff6a521677e
        Parameters
```




## <a name="see-also"></a>関連項目

[タイム トラベル デバッグ - オブジェクトのタイム トラベルのデバッグの概要](time-travel-debugging-object-model.md)

[旅行時間 - デバッグの概要](time-travel-debugging-overview.md)

---


