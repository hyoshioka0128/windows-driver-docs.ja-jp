---
title: TTD Heap オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられているヒープモデルオブジェクトについて説明します。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 473e6f5f199e9633d98e58200d85e8ba4d1754c6
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916205"
---
# <a name="ttd-heap-objects"></a>TTD Heap オブジェクト

## <a name="description"></a>説明
*TTD heap*オブジェクトは、トレースの過程で発生するヒープ呼び出しに関する情報を提供するために使用されます。

## <a name="properties"></a>[プロパティ]
各ヒープオブジェクトには、これらのプロパティがあります。

| プロパティ | 説明 |
| --- | --- |
| [操作] | 発生したアクションについて説明します。 指定できる値は、Alloc、ReAlloc、Free、Create、Protect、Lock、Unlock、Destroy です。 |
| ヒープ | Win32 ヒープのハンドル。 |

### <a name="conditional-properties"></a>条件付きプロパティ
ヒープオブジェクトによっては、以下のいくつかのプロパティが含まれている場合があります。

| プロパティ | 説明 |
| --- | --- |
| Address | 割り当てられたオブジェクトのアドレス。 |
| 前のアドレス | 再割り当てされる前に割り当てられたオブジェクトのアドレス。 アドレスが前のアドレスと同じでない場合、再割り当てによってメモリの移動が発生します。 |
| Size | 割り当てられたオブジェクトのサイズまたは要求されたサイズ。 |
| BaseAddress | ヒープ内の割り当てられたオブジェクトのアドレス。  解放 (解放) されるアドレス、または再割り当てされる前にオブジェクトのアドレスを表すことができます (ReAlloc)。 |
| フラグ | 意味は API によって異なります。 |
| 結果 | ヒープ API 呼び出しの結果。 0以外の場合は成功を意味し、ゼロは失敗を意味します。 |
| ReserveSize | ヒープ用に予約するメモリの量。 |
| CommitSize | ヒープの初期コミットサイズ。 |
| MakeReadOnly | 0以外の値は、ヒープを読み取り専用にする要求を示します。ゼロの値は、ヒープが読み取り/書き込み可能であることを示します。 |

## <a name="children"></a>Children

| オブジェクト | 説明 |
| --- | --- |
| TimeStart | 割り当ての開始位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |
| TimeEnd | 割り当ての終了位置を示す[位置オブジェクト](time-travel-debugging-position-objects.md)。 |


## <a name="example-usage"></a>使用例

この dx コマンドを使用して、-g オプションを使用してグリッドにヒープメモリを表示します。

```dbgcmd
0:0:000> dx -g @$cursession.TTD.Data.Heap()
=======================================================================================================================================================
=                          = Action     = Heap          = Address       = Size      = Flags  = (+) TimeStart = (+) TimeEnd = Result = PreviousAddress =
=======================================================================================================================================================
= [0x0] : [object Object]  - Alloc      - 0xaf0000      - 0xb0cfd0      - 0x4c      - 0x0    - FAB:17B1      - FAD:40      -        -                 =
= [0x1] : [object Object]  - Alloc      - 0xaf0000      - 0xb07210      - 0x34      - 0x8    - FB1:9         - FB3:74      -        -                 =
= [0x2] : [object Object]  - Alloc      - 0xaf0000      - 0xb256d8      - 0x3c      - 0x8    - E525:174      - E526:E1     -        -                 =
```


ヒープ操作を表す Api のセットが選択されているため、出力を "正規化されたデータ" として記述できます。 適切なパラメーターから抽出されたデータは、一貫した方法で提示されます。

TimeStart または Timestart をクリックすると、トレースのその時点に移動します。  

特定のエントリの横にある [パラメーター] フィールドをクリックすると、使用可能なパラメーター情報が表示されます。

```dbgcmd
dx -r1 @$cursession.TTD.Data.Heap()[2].@"Parameters"
@$cursession.TTD.Data.Heap()[2].@"Parameters"                
    [0x0]            : 0x16c7d780000
    [0x1]            : 0x280000
    [0x2]            : 0x20
    [0x3]            : 0x0
```

## <a name="see-also"></a>参照

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)
