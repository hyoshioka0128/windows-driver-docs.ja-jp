---
title: スマート カード リーダー デバイス設計ガイド
description: スマート カード リーダー デバイスのドライバーを開発するための設計ガイドです。
ms.assetid: e0827569-6c76-42a1-b94f-29235646519f
keywords:
  - スマート カード ドライバー WDK
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# <a name="smart-card-reader-devices-design-guide"></a>スマート カード リーダー デバイス設計ガイド


スマート カード リーダー デバイスのドライバーを開発するための設計ガイドです。

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
<td align="left"><p><a href="smart-card-driver-environment.md" data-raw-source="[Smart Card Driver Environment](smart-card-driver-environment.md)">スマート カード ドライバー環境</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="management-of-ioctl-requests-in-a-smart-card-reader-driver.md" data-raw-source="[Management of IOCTL Requests in a Smart Card Reader Driver](management-of-ioctl-requests-in-a-smart-card-reader-driver.md)">スマート カード リーダー ドライバーでの IOCTL 要求の管理</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-reader-driver.md" data-raw-source="[WDM Reader Driver](wdm-reader-driver.md)">WDM リーダー ドライバー</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="smart-card-minidrivers.md" data-raw-source="[Smart Card Minidrivers](smart-card-minidrivers.md)">スマート カード ミニドライバー</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="smart-card-reader-states.md" data-raw-source="[Smart Card Reader States](smart-card-reader-states.md)">スマート カード リーダーの状態</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="installing-smart-card-reader-drivers.md" data-raw-source="[Installing Smart Card Reader Drivers](installing-smart-card-reader-drivers.md)">スマート カード リーダー ドライバーをインストールする</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="registering-a-wdm-smart-card-reader-driver.md" data-raw-source="[Registering a WDM Smart Card Reader Driver](registering-a-wdm-smart-card-reader-driver.md)">WDM スマート カード リーダー ドライバーを登録する</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enabling-smart-card-event-logging-in-the-registry.md" data-raw-source="[Enabling Smart Card Event Logging in the Registry](enabling-smart-card-event-logging-in-the-registry.md)">スマート カードのイベント ログをレジストリで有効にする</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-device-names-for-smart-card-readers.md" data-raw-source="[WDM Device Names for Smart Card Readers](wdm-device-names-for-smart-card-readers.md)">スマート カード リーダーの WDM デバイス名</a></p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="smart-card-driver-debugging.md" data-raw-source="[Smart Card Driver Debugging](smart-card-driver-debugging.md)">スマート カード ドライバーのデバッグ</a></p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="specifications-and-resources.md" data-raw-source="[Specifications and Resources](specifications-and-resources.md)">仕様とリソース</a></p></td>
<td align="left"><p>Microsoft Windows オペレーティング システムでスマート カードのサポートを使用するには、「Interoperability Specification for ICCs and Personal Computer Systems (ICC およびパーソナル コンピューター システムの互換性の仕様)」に対応したスマート カード リーダーおよびカードが必要です。 また、スマート カード リーダーとデバイス ドライバーはプラグ アンド プレイに対応している必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





