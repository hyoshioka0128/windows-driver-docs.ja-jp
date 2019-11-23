---
title: DevCon DriverFiles
description: インストールされている INF ファイルの完全なパスとファイル名と、指定したデバイスのデバイスドライバーファイルが表示されます。 ローカルコンピューター上でのみ有効です。
ms.assetid: 8f8394e4-1ee4-4356-9f4d-ecc70deeaab1
keywords:
- DevCon DriverFiles ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon DriverFiles
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97f5e23f828e1e0b38dc37b4bc6b4a26ffa2c79f
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038092"
---
# <a name="devcon-driverfiles"></a>DevCon DriverFiles

インストールされている INF ファイルの完全なパスとファイル名と、指定したデバイスのデバイスドライバーファイルが表示されます。 ローカルコンピューター上でのみ有効です。

```
    devcon driverfiles {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_driverfiles_toolsspanspan-idddk_devcon_driverfiles_toolsspanparameters"></a><span id="ddk_devcon_driverfiles_tools"></span><span id="DDK_DEVCON_DRIVERFILES_TOOLS"></span>パラメータ

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
<td align="left"><p>任意の文字または文字を検索しません。 ワイルドカード文字 (<strong></em></strong>) を使用して、<strong><em>ディスク</em></strong>などの ID パターンを作成します。</p></td>
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

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**DevCon DriverFiles**操作は、ローカルコンピューター上でのみ実行されます。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon driverfiles *
devcon driverfiles FDC\GENERIC_FLOPPY_DRIVE pci*
devcon driverfiles =media
devcon driverfiles =media isapnp*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 8: すべてのドライバーファイルを一覧表示する](devcon-examples.md#ddk_example_8_list_all_driver_files_tools)

[例 9: 特定のデバイスのドライバーファイルを一覧表示する](devcon-examples.md#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)
