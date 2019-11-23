---
title: DevCon Stack
description: 指定したデバイスに予想されるドライバースタック、および各デバイスのデバイスセットアップクラスの GUID と名前を表示します。
ms.assetid: c06436d2-da66-4eb2-89ed-a1832967cdbb
keywords:
- DevCon Stack ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Stack
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6046e59f21922d230a86bc3d9d85dd2c45c4c00
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038080"
---
# <a name="devcon-stack"></a>DevCon Stack

指定したデバイスに予想されるドライバースタック、および各デバイスのデバイスセットアップクラスの GUID と名前を表示します。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] stack {* | ID [ID ...] | =class [ID [ID...]]}
```

## <a name="span-idddk_devcon_stack_toolsspanspan-idddk_devcon_stack_toolsspanparameters"></a><span id="ddk_devcon_stack_tools"></span><span id="DDK_DEVCON_STACK_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

**メモ**  リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista および Windows 7 を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモートアクセスは使用できません。

<span id="______________"></span> **\*** コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span>*Id*は、デバイスのハードウェア id、互換性 ID、またはデバイスインスタンス ID のすべてまたは一部を指定します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字 ( **&** ) を含む id は引用符で囲む必要があります。

次の特殊文字は、ID パラメーターを変更します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">文字</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><em></strong></p></td>
<td align="left"><p>任意の文字または文字を検索しません。 ワイルドカード文字 (</em>) を使用して、<em>ディスク</em>などの ID パターンを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>デバイスインスタンス ID ( <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>など) を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>(単一引用符)</p></td>
<td align="left"><p>文字列を文字どおり (表示されているとおりに) 照合します。 アスタリスクが ID 名の一部で、ワイルドカード文字ではないことを示すには、文字列の前に単一引用符を付けます。たとえば、 <strong>' * PNP0600</strong>,、* PNP0600 (アスタリスクを含む) はハードウェア ID です。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。 また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**/M**パラメーターは操作名 (**stack**) の前に記述する必要があります。 それ以外の場合、DevCon は **/m**パラメーターを無視し、構文エラーを返さずに、ローカルコンピューター上のデバイスドライバーのスタックを表示します。

**DevCon stack**操作は、デバイスに予想されるドライバースタックを表示します。 実際のドライバースタックは通常、予想されるスタックに一致しますが、バリエーションが可能です。

デバイスの問題を調査するには、必要なドライバースタックとスタック操作を、デバイスが使用する実際のドライバーと比較します。これは、 [**DevCon DriverFiles**](devcon-driverfiles.md)操作によって示されます。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon /m:\\Server01 stack * > Server01Stack.txt
devcon stack ISAPNP\ReadDataPort
devcon /m:\\Server01 stack pci*
devcon stack =multifunction
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 14: 記憶装置のドライバースタックを表示する](devcon-examples.md#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[例 15: デバイスのセットアップクラスを検索する](devcon-examples.md#ddk_example_15_find_the_setup_class_of_a_device_tools)

[例 16: リモートコンピューター上の関連するデバイスのスタックを表示する](devcon-examples.md#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)
