---
title: GPIO 拡張機能
description: General Purpose の入出力 (GPIO) 拡張コマンドは、GPIO コントローラーのソフトウェアの状態を表示します。
ms.assetid: 1703C402-D770-4D3F-AB70-F2D30712A5D9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f8a268a1a9b6dc58382500fb371f5021a2e603
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534357"
---
# <a name="gpio-extensions"></a>GPIO 拡張機能


General Purpose の入出力 (GPIO) 拡張コマンドは、GPIO コントローラーのソフトウェアの状態を表示します。 これらのコマンドは、GPIO フレームワーク拡張機能ドライバー (Msgpioclx .sys) によって管理されているデータ構造の情報を表示します。 GPIO framework 拡張機能の詳細については、「[汎用 i/o (gpio) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_gpio/)」を参照してください。

GPIO デバッガー拡張機能のコマンドは、gpiokd .dll に実装されています。 GPIO コマンドを読み込むには、デバッガーで「」と入力します **。**

各 GPIO コントローラーには、一連の銀行があります。 各銀行には、ピンの配列を持つピンテーブルがあります。 GPIO デバッガー拡張機能のコマンドでは、GPIO コントローラー、銀行、ピン留めテーブル、ピンに関する情報が表示されます。

## <a name="span-iddata-structures-used-by-the-gpio-commandsspanspan-iddata_structures_used_by_the_gpio_commandsspandata-structures-used-by-the-gpio-commands"></a><span id="data-structures-used-by-the-gpio-commands"></span><span id="DATA_STRUCTURES_USED_BY_THE_GPIO_COMMANDS"></span>GPIO コマンドで使用されるデータ構造


GPIO デバッガー拡張機能のコマンドでは、これらのデータ構造を使用します。これらのデータ構造は、Msgpioclx .sys によって定義されています。

<span id="msgpioclx__DEVICE_EXTENSION"></span><span id="msgpioclx__device_extension"></span><span id="MSGPIOCLX__DEVICE_EXTENSION"></span>**msgpioclx! \_デバイス \_ 拡張機能**  
GPIO framework 拡張機能ドライバーのデバイス拡張構造。 この構造体は、個々の GPIO コントローラーに関する情報を保持します。

<span id="msgpioclx__GPIO_BANK_ENTRY"></span><span id="msgpioclx__gpio_bank_entry"></span><span id="MSGPIOCLX__GPIO_BANK_ENTRY"></span>**msgpioclx! \_GPIO \_ BANK \_ エントリ**  
この構造体は、GPIO コントローラーの個々の銀行に関する情報を保持します。

<span id="msgpioclx__GPIO_PIN_INFORMATION_ENTRY"></span><span id="msgpioclx__gpio_pin_information_entry"></span><span id="MSGPIOCLX__GPIO_PIN_INFORMATION_ENTRY"></span>**msgpioclx! \_GPIO \_ PIN \_ 情報 \_ エントリ**  
この構造体は、GPIO コントローラーのバンクにある個々の pin に関する情報を保持します。

## <a name="span-idgetting_started_with_gpio_debuggingspanspan-idgetting_started_with_gpio_debuggingspanspan-idgetting_started_with_gpio_debuggingspangetting-started-with-gpio-debugging"></a><span id="Getting_started_with_GPIO_debugging"></span><span id="getting_started_with_gpio_debugging"></span><span id="GETTING_STARTED_WITH_GPIO_DEBUGGING"></span>GPIO デバッグの概要


GPIO の問題のデバッグを開始するには、 [**! gpiokd clientlist**](-gpiokd-clientlist.md)コマンドを入力します。 **! Gpiokd clientlist**コマンドは、登録されているすべての gpio コントローラーの概要を表示し、他の gpio デバッガーコマンドに渡すことができるアドレスを表示します。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


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
<td align="left"><p><strong><a href="-gpiokd-help.md" data-raw-source="[!gpiokd.help](-gpiokd-help.md)">! Gpiokd help</a></strong>コマンドは、GPIO デバッガー拡張機能コマンドのヘルプを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">!gpiokd.bankinfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-bankinfo.md" data-raw-source="[!gpiokd.bankinfo](-gpiokd-bankinfo.md)">! Gpiokd</a></strong>コマンドを実行すると、GPIO bank に関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">!gpiokd.clientlist</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-clientlist.md" data-raw-source="[!gpiokd.clientlist](-gpiokd-clientlist.md)">! Gpiokd clientlist</a></strong>コマンドは、登録されているすべての GPIO コントローラーを表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">!gpiokd.gpioext</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-gpioext.md" data-raw-source="[!gpiokd.gpioext](-gpiokd-gpioext.md)">! Gpiokd gpiokd</a></strong>コマンドを実行すると、GPIO コントローラーに関する情報が表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">!gpiokd.pininfo</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pininfo.md" data-raw-source="[!gpiokd.pininfo](-gpiokd-pininfo.md)">! Gpiokd pininfo</a></strong>コマンドは、指定された GPIO pin に関する情報を表示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">!gpiokd.pinisrvec</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pinisrvec.md" data-raw-source="[!gpiokd.pinisrvec](-gpiokd-pinisrvec.md)">! Gpiokd</a></strong>コマンドは、指定された Pin の割り込みサービスルーチン (ISR) ベクター情報を表示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">!gpiokd.pintable</a></strong></p></td>
<td align="left"><p><strong><a href="-gpiokd-pintable.md" data-raw-source="[!gpiokd.pintable](-gpiokd-pintable.md)">! Gpiokd</a></strong>コマンドは、GPIO ピンの配列に関する情報を表示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[特殊な拡張機能のコマンド](specialized-extensions.md)

 

 






