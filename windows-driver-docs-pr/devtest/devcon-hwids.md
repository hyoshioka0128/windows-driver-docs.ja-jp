---
title: DevCon HwIDs
description: 指定したデバイスのハードウェア Id、互換性 Id、およびデバイスインスタンス Id が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。
ms.assetid: b76de01e-fedf-41c2-ba2e-837b442ab93f
keywords:
- DevCon HwIDs ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon HwIDs
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a4058f972ff8ec9e45a3c82fc6b00d7e833f53f
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038025"
---
# <a name="devcon-hwids"></a>DevCon HwIDs

指定したデバイスのハードウェア Id、互換性 Id、およびデバイスインスタンス Id が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] hwids {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_hwids_toolsspanspan-idddk_devcon_hwids_toolsspanparameters"></a><span id="ddk_devcon_hwids_tools"></span><span id="DDK_DEVCON_HWIDS_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

**メモ**  リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista および Windows 7 を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモートアクセスは使用できません。

<span id="______________"></span> **\*** コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span>*Id*識別子を使用して1つ以上のデバイスを指定します。

デバイスのハードウェア ID、互換性 ID、またはデバイスインスタンス ID のすべてまたは一部を入力します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字 ( **&** ) を含む id は引用符で囲む必要があります。

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

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、セットアップクラスを使用して1つ以上のデバイスを指定します。

デバイスのセットアップクラスの名前のすべてまたは一部を入力します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**/M**パラメーターは操作名 (**hwids**) の前に記述する必要があります。 それ以外の場合、DevCon は **/m**パラメーターを無視し、構文エラーを返さずにローカルコンピューター上のデバイスのハードウェア id を表示します。

ルートで列挙されたデバイスのハードウェア ID を作成するには、 [**DevCon SetHwID**](devcon-sethwid.md)コマンドを使用します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon hwids *
devcon /m:\\server01 hwids acpi*
devcon hwids acpi* *port*
devcon hwids =usb
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 1: すべてのハードウェア Id を検索する](devcon-examples.md#ddk_example_1_find_all_hardware_ids_tools)

[例 2: パターンを使用してハードウェア Id を検索する](devcon-examples.md#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[例 3: クラスを使用してハードウェア Id を検索する](devcon-examples.md#ddk_example_3_find_hardware_ids_by_using_a_class_tools)
