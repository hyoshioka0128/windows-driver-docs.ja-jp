---
title: GPIO 拡張機能
description: 一般的な目的の入出力 (GPIO) の拡張機能コマンドでは、GPIO コント ローラーのソフトウェアの状態を表示します。
ms.assetid: 1703C402-D770-4D3F-AB70-F2D30712A5D9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f35df5cb6bc7b76170002ba43a3a4cfcaae20795
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370862"
---
# <a name="gpio-extensions"></a>GPIO 拡張機能


一般的な目的の入出力 (GPIO) の拡張機能コマンドでは、GPIO コント ローラーのソフトウェアの状態を表示します。 これらのコマンドは、GPIO フレームワークの拡張機能ドライバー (Msgpioclx.sys) によって管理されるデータ構造から情報を表示します。 GPIO フレームワークの拡張機能については、次を参照してください。[汎用入出力 (GPIO) ドライバー](https://go.microsoft.com/fwlink/p?LinkID=299823)します。

GPIO デバッガー拡張機能のコマンドは、gpiokd.dll で実装されます。 GPIO コマンドを読み込むには、次のように入力します。 **.load gpiokd.dll**デバッガーでします。

各 GPIO コント ローラーには、銀行のセットがあります。 各銀行では、pin のアレイを装備した暗証番号 (pin) テーブルがあります。 GPIO デバッガー拡張機能のコマンドは、GPIO コント ローラー、銀行、暗証番号 (pin) テーブル、および pin に関する情報を表示します。

## <a name="span-iddata-structures-used-by-the-gpio-commandsspanspan-iddatastructuresusedbythegpiocommandsspandata-structures-used-by-the-gpio-commands"></a><span id="data-structures-used-by-the-gpio-commands"></span><span id="DATA_STRUCTURES_USED_BY_THE_GPIO_COMMANDS"></span>GPIO コマンドで使用するデータ構造


GPIO デバッガーの拡張機能コマンドでは、Msgpioclx.sys で定義されているこれらのデータ構造を使用します。

<span id="msgpioclx__DEVICE_EXTENSION"></span><span id="msgpioclx__device_extension"></span><span id="MSGPIOCLX__DEVICE_EXTENSION"></span>**msgpioclx!\_DEVICE\_EXTENSION**  
GPIO フレームワークの拡張機能ドライバーのデバイス拡張機能の構造。 この構造体は、個々 の GPIO コント ローラーに関する情報を保持します。

<span id="msgpioclx__GPIO_BANK_ENTRY"></span><span id="msgpioclx__gpio_bank_entry"></span><span id="MSGPIOCLX__GPIO_BANK_ENTRY"></span>**msgpioclx!\_GPIO\_BANK\_ENTRY**  
この構造体は、GPIO コント ローラーの個々 の銀行に関する情報を保持します。

<span id="msgpioclx__GPIO_PIN_INFORMATION_ENTRY"></span><span id="msgpioclx__gpio_pin_information_entry"></span><span id="MSGPIOCLX__GPIO_PIN_INFORMATION_ENTRY"></span>**msgpioclx!\_GPIO\_PIN\_情報\_エントリ**  
この構造体は、GPIO コント ローラーの銀行で個々 の pin に関する情報を保持します。

## <a name="span-idgettingstartedwithgpiodebuggingspanspan-idgettingstartedwithgpiodebuggingspanspan-idgettingstartedwithgpiodebuggingspangetting-started-with-gpio-debugging"></a><span id="Getting_started_with_GPIO_debugging"></span><span id="getting_started_with_gpio_debugging"></span><span id="GETTING_STARTED_WITH_GPIO_DEBUGGING"></span>GPIO の概要のデバッグ


GPIO 問題のデバッグを開始するには、入力、 [ **! gpiokd.clientlist** ](-gpiokd-clientlist.md)コマンド。 **! Gpiokd.clientlist**コマンドは、すべての登録済みの GPIO コント ローラーおよび他の GPIO デバッガー コマンドに渡すことができる表示アドレスの概要を表示します。

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
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">!gpiokd.help</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">! Gpiokd.help</a></strong>コマンドは、GPIO デバッガーの拡張機能コマンドのヘルプを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">!gpiokd.bankinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">! Gpiokd.bankinfo</a></strong>コマンドは、GPIO 銀行に関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">!gpiokd.clientlist</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">! Gpiokd.clientlist</a></strong>コマンドは、すべての登録済みの GPIO コント ローラーを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">!gpiokd.gpioext</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">! Gpiokd.gpioext</a></strong>コマンドは、GPIO コント ローラーに関する情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">!gpiokd.pininfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">! Gpiokd.pininfo</a></strong>コマンドは、指定した GPIO ピンに関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">!gpiokd.pinisrvec</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">! Gpiokd.pinisrvec</a></strong>コマンドには、指定した pin の割り込みサービス ルーチン (ISR) ベクターの情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">!gpiokd.pintable</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">! Gpiokd.pintable</a></strong>コマンドの GPIO ピン配列に関する情報を表示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[特殊な拡張コマンド](specialized-extensions.md)

 

 






