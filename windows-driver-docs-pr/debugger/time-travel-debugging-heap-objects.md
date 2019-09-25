---
title: TTD Heap オブジェクト
description: このセクションでは、タイムトラベルデバッグに関連付けられているヒープモデルオブジェクトについて説明します。
ms.date: 09/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21d1e2be8456ba705f68337196bc41b442a6692e
ms.sourcegitcommit: e94e072ef90fc1c4f343055098920463fbf5c630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2019
ms.locfileid: "71227725"
---
# <a name="ttd-heap-objects"></a>TTD Heap オブジェクト
## <a name="description"></a>説明
*TTD heap*オブジェクトは、トレースの過程で発生するヒープ呼び出しに関する情報を提供するために使用されます。


## <a name="properties"></a>Properties
各ヒープオブジェクトには、これらのプロパティがあります。

| プロパティ | 説明 |
| --- | --- |
| 操作 | 発生したアクションについて説明します。 指定できる値は次のとおりです。Alloc、ReAlloc、Free、Create、Protect、Lock、Unlock、Destroy。 |
| ヒープ | Win32 ヒープのハンドル。 |

### <a name="conditional-properties"></a>条件付きプロパティ
ヒープオブジェクトによっては、以下のいくつかのプロパティが含まれている場合があります。

| プロパティ | 説明 |
| --- | --- |
| Address | 割り当てられたオブジェクトのアドレス。 |
| 前のアドレス | 再割り当てされる前に割り当てられたオブジェクトのアドレス。 アドレスが前のアドレスと同じでない場合、再割り当てによってメモリの移動が発生します。 |
| サイズ | 割り当てられたオブジェクトのサイズまたは要求されたサイズ。 |
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





## <a name="see-also"></a>関連項目

[タイムトラベルデバッグ-タイムトラベルデバッグオブジェクトの概要](time-travel-debugging-object-model.md)

[タイムトラベルのデバッグ-概要](time-travel-debugging-overview.md)

---


