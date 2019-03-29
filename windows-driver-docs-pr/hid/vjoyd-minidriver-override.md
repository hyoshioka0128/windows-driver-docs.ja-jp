---
title: VJoyD ミニドライバーの上書き
description: VJoyD ミニドライバーの上書き
ms.assetid: a77d2464-7785-44a9-b527-2224d261feac
keywords:
- ジョイスティックに WDK を非表示に上書き
- 仮想ジョイスティックのドライバー WDK を非表示に上書き
- VJoyD WDK HID、上書き
- 仮想ミニドライバー WDK ジョイスティックをオーバーライドします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7121ec7f010308e588cfed6a580301ee6f5e0de5
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464174"
---
# <a name="vjoyd-minidriver-override"></a>VJoyD ミニドライバーの上書き





JoyHID.VxD デバイス ドライバーを読み込まない/非表示の USB デバイスでは、その他の USB/非表示デバイスを使用すると、ゲーム オプションのコントロール パネルの 存在する重複するデバイス エントリを表示できる場合があります。 これには、JoyHID 準拠デバイスが非 JoyHID デバイスと同時に、システムに接続されているときに発生します。

デバイスは、おそらく、デバイスの製造元または関連--によって開発された--JoyHID 以外 VJoyD ミニドライバーを使用している場合、デバイスの種類のキーとレジストリに関連する名前付きの値を正しく設定してこれらの問題を回避できます。 このトピックで説明する機能は、フォームの型のキーを持つデバイスにのみ使用可能な"VID\_*vvvv*& PID\_*pppp*"という文字*v*と*p*はゼロで埋めますベンダーと製品の製品 ID の値。

デバイスからデータを取得しようとしています。 または、コントロール パネル/追加のリストに不要なデバイスのエントリを表示する JoyHID を防ぐため、次の手順を正しく書式設定された種類のキーを指定するには。

-   OEMData を設定する\_HWS\_自動読み込みします。 これは、デバイス名がデバイスを追加する 一覧に表示されていることを防ぎます。

-   OEMCallout をデバイスに読み込む必要のあるドライバーに設定します。 これは JoyHID.VxD がデバイスで読み込まれていることを防ぎます。

-   デバイスの適切な名前に OEMName を設定します。

必要な場合は、JoyHID がデバイスからデータを読み取ることを防ぐために任意の値をレジストリ値を設定できます。 たとえば、次の値を使用する可能性があります。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>名前</th>
<th>値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OEMName</p></td>
<td><p>「IHV デバイス X、未使用のエントリは削除しないでください」</p></td>
</tr>
<tr class="even">
<td><p>OEMData</p></td>
<td><p>OEMData は、2 つの Dword を格納しているバイナリのレジストリ フィールドです。 最初は JOY_HWS_ * フラグのセットで、2 番目は、デバイス上のボタンの数です。 JOY_HWS_AUTOLOAD フラグの値は、ある 0x10000000 dinput.h で定義されます。 ここで関連するはボタンの数であるため、8 バイト (16 進数) で 00,00,00,10,00,00,00,00 必要があります。</p></td>
</tr>
<tr class="odd">
<td><p>OEMCallout</p></td>
<td><p>「未使用」</p></td>
</tr>
</tbody>
</table>

 

上記のような値は、デバイスからのデータの読み取りを試行する JoyHID を単なるように注意してください。 デバイスが VJoyD ミニドライバーを使用する場合は、正しく読み込まれるドライバーとデバイスの名前を反映するように前述の値を設定してください。

 

 




