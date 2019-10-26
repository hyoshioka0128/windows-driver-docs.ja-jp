---
title: TTD 呼び出しオブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられたモデルオブジェクトを呼び出す方法について説明します。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3576f064e7baddd963cedb6593c7b4ac96b4e4
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916220"
---
# <a name="ttd-calls-objects"></a>TTD 呼び出しオブジェクト

## <a name="description"></a>説明
*TTD calls*オブジェクトは、トレースの過程で発生する関数呼び出しに関する情報を提供するために使用されます。

## <a name="parameters"></a>パラメーター

| プロパティ | 説明 |
| --- | --- |
| プロシージャ!SymbolName | コンマで区切られた、二重引用符で囲まれた1つ以上の。 たとえば、dx @ $cursession です。TTD.呼び出し ("module! symbol1", "module! symbol2",...) |

## <a name="properties"></a>[プロパティ]

| プロパティ | 説明 |
| --- | --- |
| EventType  |  イベントの種類。 これは、すべての TTD 呼び出しオブジェクトの "呼び出し" です。 |
| スレッド Id   |  要求を行ったスレッドの OS スレッド ID。 |
| UniqueThreadId |   トレース全体のスレッドの一意の ID。 通常のスレッド Id は、プロセスの有効期間にわたって再利用できますが、UniqueThreadIds することはできません。 |
| 関数 | 関数のシンボル名。 |
| FunctionAddress | メモリ内の関数のアドレス。 |
| ReturnValue | 関数の戻り値。 関数に void 型がある場合、このプロパティは存在しません。 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| パラメーター [] | 関数に渡されたパラメーターを格納している配列。 要素の数は、関数の型シグネチャによって異なります。 |
| TimeStart | 呼び出しの開始位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |
| TimeEnd | 呼び出しの終了位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |

## <a name="remarks"></a>注釈
タイムトラベルデバッグでは、Pdb に用意されているシンボル情報を使用して、関数のパラメーターの数とその型、戻り値の型、および呼び出し規約を決定します。 シンボル情報が使用できない場合、またはシンボルがパブリックシンボル情報に制限されている場合でも、クエリを実行できます。 このシナリオでは、タイムトラベルクエリエンジンによっていくつかの仮定が行われます。
* 関数には、4 64 ビットの符号なし整数パラメーターがあります
* 戻り値は、64ビットの符号なし整数です。
* 関数名は固定文字列 "UnknownOrMissingSymbols" に設定されます。

これらの前提により、十分なシンボル情報がない場合にクエリを実行できます。 ただし、最適な結果を得るには、可能であれば完全な PDB シンボルを使用します。

呼び出し関数は計算を行い、トレースのサイズによっては実行に時間がかかる場合があることに注意してください。 CPU 使用率は、計算中にスパイクし、タスクマネージャーでの CPU 使用率を監視して、計算が進行中であることを示します。  クエリの結果はメモリにキャッシュされるため、クエリを実行した呼び出しに対する後続のクエリは大幅に高速化されます。

## <a name="example-usage"></a>使用例

この例は、ucrtbase! initterm の呼び出しオブジェクトを示しています。

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

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
