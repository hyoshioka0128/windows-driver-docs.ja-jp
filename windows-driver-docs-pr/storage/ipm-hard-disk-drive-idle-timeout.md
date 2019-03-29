---
title: IPM ハード ディスク ドライブのアイドル タイムアウト
description: IPM ハード ディスク ドライブのアイドル タイムアウト
ms.assetid: 1dcc261a-803c-4c0e-a68e-29b00f46cd32
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4dd731f1b57f8c4c6050431247ae0302f6286bf2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574625"
---
# <a name="ipm-hard-disk-drive-idle-timeout"></a>IPM ハード ディスク ドライブのアイドル タイムアウト


ハード ディスク ドライブ (HDD) は、標準的なモバイル PC で、プライマリ電源データ コンシューマーではありませんは、HDD メディアを回転して電源節約を実現できます。 HDD のアイドル タイムアウトは、ディスクの期間が非アクティブ状態を読み書きした後、HDD メディアを自動的に回転する Windows を使用できます。

HDD メディアのスピン ダウン時に、実現する省電力は、製造元と HDD のモデルによって異なります。 システム製造元は、特定のデバイスに最適な HDD アイドル タイムアウト値を決定する HDD ベンダーと協力することをお勧めします。

既定では、Windows Vista は、比較的長い HDD アイドル タイムアウト値を指定します。 システム製造元は、モバイル Pc で積極的なバッテリの保護を実現しようとするときに短い値を指定することを検討してください。 次の表では、HDD アイドル状態の設定の詳細をまとめたものです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>詳細</strong></p></td>
<td align="left"><p><strong>[説明]</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>フレンドリ名</p></td>
<td align="left"><p>後にハード_ディスクをオフにします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>説明</p></td>
<td align="left"><p>どのくらいの期間、ハード ドライブがアクティブでないディスクがオフにするを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PowerCfg のエイリアス</p></td>
<td align="left"><p>DISKIDLE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>グループ ポリシーのパス</p></td>
<td align="left"><p>ハード_ディスクをオフの管理システム \ 電源 Management\Hard ディスク Settings\Turn</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID</p></td>
<td align="left"><p>6738e2c4-e8a5-4a42-b16a-e040e769756e</p></td>
</tr>
<tr class="odd">
<td align="left"><p>定義されています。</p></td>
<td align="left"><p>Ntpoapi.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>バランスの取れた既定値</p></td>
<td align="left"><p>60 分 (AC) 30 分 (DC)</p></td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[モバイル バッテリの寿命に関するソリューションのモバイル プラットフォーム プロフェッショナル向けガイド。](https://go.microsoft.com/fwlink/p/?linkid=144534)

 

 




