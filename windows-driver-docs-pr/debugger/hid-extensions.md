---
title: HID 拡張機能
description: このセクションでは、ヒューマン インターフェイス デバイス (HID) デバッガー拡張機能のコマンドについて説明します。
ms.assetid: 796DB87B-1E04-40FA-90F9-699EE7032B3C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60eee0bf524d43a6c5ee68dd7bc427fe916709b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342450"
---
# <a name="hid-extensions"></a>HID 拡張機能


このセクションでは、ヒューマン インターフェイス デバイス (HID) デバッガー拡張機能のコマンドについて説明します。

HID デバッガー拡張機能のコマンドは、Hidkd.dll で実装されます。 HID コマンドを読み込むには、次のように入力します。 **.load hidkd.dll**デバッガーでします。

## <a name="span-idgettingstartedwiththehidextensionsspanspan-idgettingstartedwiththehidextensionsspanspan-idgettingstartedwiththehidextensionsspangetting-started-with-the-hid-extensions"></a><span id="Getting_started_with_the_HID_extensions_"></span><span id="getting_started_with_the_hid_extensions_"></span><span id="GETTING_STARTED_WITH_THE_HID_EXTENSIONS_"></span>HID の拡張機能の概要


HID の問題のデバッグを開始するには、入力、 [ **! hidtree** ](-hidkd-hidtree.md)コマンド。 **! Hidtree**コマンドがコマンドの一覧を表示し、preparsed デバイス オブジェクトを調査するために使用できるアドレスが、データを非表示しレポート記述子を非表示にします。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-help.md" data-raw-source="[!hidkd.help](-hidkd-help.md)">!hidkd.help</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-help.md" data-raw-source="[!hidkd.help](-hidkd-help.md)">! Hidkd.help</a></strong>コマンドは、HID デバッガーの拡張機能コマンドのヘルプを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">!hidkd.hidfdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidfdo.md" data-raw-source="[!hidkd.hidfdo](-hidkd-hidfdo.md)">! Hidkd.hidfdo</a></strong>コマンドには、機能のデバイス オブジェクト (FDO) に関連付けられた HID 情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">!hidkd.hidpdo</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidpdo.md" data-raw-source="[!hidkd.hidpdo](-hidkd-hidpdo.md)">! Hidkd.hidpdo</a></strong>コマンドには、物理デバイス オブジェクト (PDO) に関連付けられた HID 情報が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">!hidkd.hidtree</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidtree.md" data-raw-source="[!hidkd.hidtree](-hidkd-hidtree.md)">! Hidkd.hidtree</a></strong>コマンドは、その子ノードと共に HID 機能ドライバーを持つすべてのデバイス ノードの一覧を表示します。 子ノードでは、親ノードの HID 関数ドライバーによって作成された、物理デバイス オブジェクト (PDO) が存在します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">!hidkd.hidppd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidppd.md" data-raw-source="[!hidkd.hidppd](-hidkd-hidppd.md)">! Hidkd.hidppd</a></strong>コマンド preparsed HID データを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">!hidkd.hidrd</a></strong></p></td>
<td align="left"><p><strong><a href="-hidkd-hidrd.md" data-raw-source="[!hidkd.hidrd](-hidkd-hidrd.md)">! Hidkd.hidrd</a></strong>コマンドは、生と解析の両方の形式で、HID レポート記述子を表示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RCDRKD 拡張機能](rcdrkd-extensions.md)

[特殊な拡張コマンド](specialized-extensions.md)

 

 






