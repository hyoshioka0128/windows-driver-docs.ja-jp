---
title: 最上位のコレクションの HIDClass ハードウェア ID
description: このセクションでは、ハードウェア、HID クラス ドライバーが最上位のコレクション用に生成する Id を指定します。
ms.assetid: a90eea17-0a63-4786-a31f-740bcc670c2a
keywords:
- ヒューマン インターフェイス デバイス WDK、ハードウェア Id
- HID WDK、ハードウェア Id
- 対話型の入力デバイス WDK、ハードウェア Id
- 入力デバイス WDK、ハードウェア Id
- ベンダーのハードウェア Id WDK を非表示
- ハードウェア Id WDK を非表示
- ID は、WDK を非表示に書式設定します。
- ヒューマン インターフェイス デバイス WDK、コレクション
- HID WDK、コレクション
- 対話型の入力デバイス WDK、コレクション
- デバイス コレクション、WDK を入力します。
- WDK を非表示にハードウェア Id のコレクション
- WDK を非表示に最上位のコレクション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 697277bf4f3e3de70e04242c87fb22c7d545d718
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579320"
---
# <a name="hidclass-hardware-ids-for-top-level-collections"></a>最上位のコレクションの HIDClass ハードウェア ID


このセクションでは、ハードウェア、HID クラス ドライバーが最上位のコレクション用に生成する Id を指定します。

仕入先として指定されている形式を使用する必要があります*ベンダーのハードウェア ID の形式*最上位のコレクションを識別するためにします。 他のすべての*デバイス ID*形式は内部使用専用に予約されています。




ハードウェア devnode 用 HID クラス ドライバーに生成する Id は、次に依存します。

1.  基になるトランスポートによってサポートされる関数の数
2.  レポート記述子の最上位レベルのコレクションの数

これらの要因に基づいて、ハードウェア Id の 4 つのカテゴリがあります。

|                 | 1 つ TLC | 複数の TLC |
|-----------------|------------|--------------|
| 単一関数 | ケース 1     | ケース 2       |
| 複数の関数  | ケース 3     | ケース 4       |

 

## <a name="case-1-single-function-device-with-single-tlc"></a>ケース 1:単一関数のデバイス シングル TLC を


このハードウェア ID の形式を使用する条件:

1.  基になるトランスポートによってサポートされる関数の数 = 1 (& a) (& a)
2.  TLC の数 = 1

ハードウェア ID の形式:

-   HID\\Vid\_v(4) & Pid\_d(4) & Rev\_r(4)
-   HID\\Vid\_v(4) & Pid\_d(4)
-   HID\_デバイス\_UP:p(4)\_U:u(4)
-   HID\_デバイス

## <a name="case-2-single-function-device-with-multiple-tlc"></a>ケース 2:複数 TLC でデバイスを単一関数


このハードウェア ID の形式を使用する条件:

1.  基になるトランスポートによってサポートされる関数の数 = 1 (& a) (& a)
2.  TLC 数&gt;1

ハードウェア ID の形式:

-   HID\\Vid\_v(4) & Pid\_d(4) & Rev\_r(4) & Colb(2)
-   HID\\Vid\_v(4) & Pid\_d(4) & Colb(2)
-   HID\_デバイス\_UP:p(4)\_U:u(4) \[WINDOWS Inf のみ用に予約されています\]
-   HID\_デバイス\[WINDOWS Inf のみ用に予約されています\]

## <a name="case-3-multi-function-device-with-single-tlc"></a>ケース 3:単一 TLC の多機能デバイス


このハードウェア ID の形式を使用する条件:

1.  基になるトランスポートによってサポートされる関数の数&gt;1 (& a) (& a)
2.  TLC の数 = 1

ハードウェア ID の形式:

-   HID\\Vid\_v(4) & Pid\_d(4) & Rev\_r(4) & MI\_z(2)
-   HID\\Vid\_v(4) & Pid\_d(4) & MI\_z(2)
-   HID\_デバイス\_UP:p(4)\_U:u(4) \[WINDOWS Inf のみ用に予約されています\]
-   HID\_デバイス\[WINDOWS Inf のみ用に予約されています\]

## <a name="case-4-multi-function-device-with-multiple-tlc"></a>ケース 4:複数 TLC の多機能デバイス


このハードウェア ID の形式を使用する条件:

1.  基になるトランスポートによってサポートされる関数の数&gt;1 (& a) (& a)
2.  TLC 数&gt;1

ハードウェア ID の形式:

-   HID\\Vid\_v(4)&Pid\_d(4)&Rev\_r(4)&MI\_z(2)&Colb(2)
-   HID\\Vid\_v(4)&Pid\_d(4)&MI\_z(2)&Colb(2)
-   HID\_デバイス\_UP:p(4)\_U:u(4) \[WINDOWS Inf のみ用に予約されています\]
-   HID\_デバイス\[WINDOWS Inf のみ用に予約されています\]

## <a name="special-purpose-hardware-id"></a>特殊な目的のハードウェア ID


次にハードウェア Id (内部使用のみ) の既定のシステム機能を提供する Windows を使用します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>デバイスの種類</th>
<th>使用状況 ページ</th>
<th>使用方法</th>
<th>Hardware ID (ハードウェア ID)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ポインター</p></td>
<td><p>0x01</p></td>
<td><p>0x01</p></td>
<td><p>HID_DEVICE_SYSTEM_MOUSE</p></td>
</tr>
<tr class="even">
<td><p>マウス</p></td>
<td><p>0x01</p></td>
<td><p>0x02</p></td>
<td><p>HID_DEVICE_SYSTEM_MOUSE</p></td>
</tr>
<tr class="odd">
<td><p>ジョイスティック</p></td>
<td><p>0x01</p></td>
<td><p>0x04</p></td>
<td><p>HID_DEVICE_SYSTEM_GAME</p></td>
</tr>
<tr class="even">
<td><p>ゲーム パッド</p></td>
<td><p>0x01</p></td>
<td><p>0x05</p></td>
<td><p>HID_DEVICE_SYSTEM_GAME</p></td>
</tr>
<tr class="odd">
<td><p>キーボード</p></td>
<td><p>0x01</p></td>
<td><p>0x06</p></td>
<td><p>HID_DEVICE_SYSTEM_KEYBOARD</p></td>
</tr>
<tr class="even">
<td><p>キーパッド</p></td>
<td><p>0x01</p></td>
<td><p>0x07</p></td>
<td><p>HID_DEVICE_SYSTEM_KEYBOARD</p></td>
</tr>
<tr class="odd">
<td><p>システム コントロール</p></td>
<td><p>0x01</p></td>
<td><p>0x80</p></td>
<td><p>HID_DEVICE_SYSTEM_CONTROL</p></td>
</tr>
<tr class="even">
<td><p>コンシューマー オーディオ コントロール</p></td>
<td><p>0x0C</p></td>
<td><p>0x01</p></td>
<td><p>HID_DEVICE_SYSTEM_CONSUMER</p></td>
</tr>
</tbody>
</table>

 

重要な注意事項:

-   HIDClass によって生成された互換性 Id がないです。
-   仕入先のサード パーティの Inf は、ハードウェア Id に対してのみ一致する必要があります。
-   ハードウェア Id を含む HID\_デバイス\_システム\_\*に使用するため、オペレーティング システムを開く「特殊な」デバイスします。 これらの特殊なハードウェア Id の INF に一致しないベンダーが提供されています。
-   ベンダーは、サード パーティの HID トランスポート ミニドライバーは、HIDClass が適切なハードウェア Id を生成できることを確認するフィールドが以下に指定する必要があります提供されています。

凡例:

|       |                 |                   |                                                          |
|-------|-----------------|-------------------|----------------------------------------------------------|
| フィールド | Contains        | 16 進数の値 | 説明                                                  |
| v(4)  | 次の 4 つの 16 進数です。 | 0x0000-0 xffff     | ベンダ ID                                                |
| d(4)  | 次の 4 つの 16 進数です。 | 0x0000-0 xffff     | 製品 ID                                               |
| r(4)  | 次の 4 つの 16 進数です。 | 0x0000-0 xffff     | リビジョン番号                                          |
| z(2)  | 2 つの 16 進数です。  | 0x00-0 xff の場合         | インターフェイスの数 (だけ使用複合 USB デバイスの使用)。 |
| b(2)  | 2 つの 16 進数です。  | 0x00-0 xff の場合         | コレクションの数 (デバイスでしか使用複数 TLC。) |
| p(4)  | 次の 4 つの 16 進数です。 | 0x0000-0 xffff     | TLC の使用状況 ページの数                                |
| u(4)  | 次の 4 つの 16 進数です。 | 0x0000-0 xffff     | TLC の使用状況の数                                      |

 

 

 




