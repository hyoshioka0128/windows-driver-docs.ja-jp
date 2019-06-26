---
title: ボタンのレポート
description: ボックスで汎用入出力 (GPIO) ボタン ドライバーは、Windows に報告ボタン配列の定義済みの GPIO リソースで受信した割り込みに基づいています。
ms.assetid: 7D96E1CB-3406-4D61-9D5C-65BC6BFD1FFA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3850e9d4e623abf71b21064d7732c3b99a8917ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385167"
---
# <a name="button-reporting"></a>ボタンのレポート


ボックスで汎用入出力 (GPIO) ボタン ドライバーは、Windows に報告ボタン配列の定義済みの GPIO リソースで受信した割り込みに基づいています。

インボックス GPIO ボタン ドライバーは、ボタンを押すとに掲載されている組み合わせを報告*テーブル 1 GPIO ボタン Reporting*します。

**表 1. GPIO ボタンのレポート**

| Button        | 必要があります\_CRS ウェイク アップ可能 | SOC の GPIO が必要です。 | エッジのレポート (と仮定して ActiveLow) |
|---------------|-------------------------|----------------------|-------------------------------------|
| Windows       | 〇                     | 〇                  | どちらもオン                                |
| 音量増     | 〇                     | 〇                  | どちらもオン                                |
| 音量-   | 〇                     | 〇                  | どちらもオン                                |
| 回転ロック | X                      | 〇                  | どちらもオン                                |
| Power         | 〇                     | 〇                  | どちらもオン                                |

 

すべての非 GPIO ベースの実装は、レポートの同じスキームに従う必要があります。

定義の順序は、Power、Windows、Volume Up、Volume Down、回転ロックは。 これらの HID 記述子を作成する方法の例については、次を参照してください。 [HID ボタンのレポート記述子](hid-button-report-descriptors.md)します。

**注**  前の要件の使い方を説明した**Win + O**回転ロックします。 キーボード レイアウトの変更、あくまではいないこの組み合わせはまだ機能ですが、一方**Win + F14**レイアウトに依存しないのです。

 

**レポートはトリガー GPIO ボタン以外の 2 つのテーブルにします。**

| 個々 のボタンのレポート | Source              | 使用法の要件      | レポートのトリガー         | 繰り返し |
|-----------------------------|---------------------|-------------------------|------------------------|----------|
| Power                       | システム コントロール      | 0x84 (power)            | 物理ボタン – 最大   | X       |
| Windows                     | キーボード            | 0xE3 (Win)              | 物理ボタン – 最大   | X       |
| 音量増                   | コンシューマー コレクション | 0xE9 (ボリュームを)        | 物理ボタン-下 | 〇      |
| 音量-                 | コンシューマー コレクション | 0 xea (ボリューム ダウン)      | 物理ボタン-下 | 〇      |
| 回転ロック               | キーボード            | 0xE3 = 0x69 (Win + F14) | 物理ボタン-下 | X       |

 

次のキーボードの組み合わせを報告する必要は、完了するに基づいており、組み合わせが保持されているかどうかは繰り返すことはできません必要があります。

**表 3 レポートはトリガーのない-GPIO ボタンの組み合わせ**

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ボタンの組み合わせの報告</th>
<th align="left">使用法の要件</th>
<th align="left">レポートのトリガー</th>
<th align="left">繰り返し</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Windows + 電源</td>
<td align="left"><p>0xE0 + 0xE2 + 0x4C</p>
<p>(<strong>Ctrl + Alt + Del</strong>)</p></td>
<td align="left">物理的な電源ボタン-下</td>
<td align="left">X</td>
</tr>
<tr class="even">
<td align="left">Windows + 音量増</td>
<td align="left"><p>0xE3 + 0xE0 + 0x69</p>
<p>(<strong>Win + Ctrl + F14</strong>)</p></td>
<td align="left">物理ボリューム ボタンの下</td>
<td align="left">X</td>
</tr>
<tr class="odd">
<td align="left">Windows + ボリューム ダウン</td>
<td align="left"><p>0xE3 + 0x6A</p>
<p>(<strong>Win + F15</strong>)</p></td>
<td align="left">物理ボリューム ボタンの下</td>
<td align="left">X</td>
</tr>
</tbody>
</table>

 

**注:**  
-   完全なガイダンスと、電源ボタンの実装では、次を参照してください。[電源ボタンの動作と実装](https://aka.ms/connect-redirect?DownloadID=47452)します。
-   ボタンのコネクト スタンバイのガイダンスについては、次を参照してください。[スタンバイ状態の接続されたソースのスリープ解除](https://aka.ms/connect-redirect?DownloadID=49891)します。
-   ACPI の実装の詳細については、次を参照してください。 [ACPI 設計ガイド](https://aka.ms/connect-redirect?DownloadID=48755)します。

 

 

 




