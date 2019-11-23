---
title: DevCon SetHwID
description: ローカルコンピューターまたはリモートコンピューター上のルートで列挙されたデバイスのハードウェア Id の追加、削除、および順序の変更を行います。
ms.assetid: 79948ff0-8b30-4a64-beea-e3f08aef7170
keywords:
- DevCon SetHwID ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon SetHwID
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: afd80c6b8557f80d474ba0bfa4048b384864aee4
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038047"
---
# <a name="devcon-sethwid"></a>DevCon SetHwID

ローカルコンピューターまたはリモートコンピューター上のルートで列挙されたデバイスのハードウェア Id の追加、削除、および順序の変更を行います。

```
    devcon [/m:\\computer] sethwid {* | ID [ID ...] | =class [ID [ID ...]]} := [ = | + | - | ! ]HardwareIDs ...
```

## <a name="span-idddk_devcon_sethwid_toolsspanspan-idddk_devcon_sethwid_toolsspanparameters"></a><span id="ddk_devcon_sethwid_tools"></span><span id="DDK_DEVCON_SETHWID_TOOLS"></span>パラメータ

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

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、ルートで列挙されたデバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

<span id="_______HardwareIDs______"></span><span id="_______hardwareids______"></span><span id="_______HARDWAREIDS______"></span>*ハードウェア id*1つ以上のハードウェア Id を指定します。

ハードウェア id の前にシンボルパラメーター ( **+** 、 **-** 、 **=** 、 **!** ) が指定されていない場合は、指定された順序でデバイスのハードウェア id の一覧の末尾に、指定したハードウェア id が追加または移動されます。 これは、-パラメーターと同じです。

<span id="_"></span>=  
指定された順序で、指定したハードウェア Id を持つデバイスのハードウェア Id の一覧を置き換えます。

<span id="______________"></span> **+** 指定されたハードウェア Id をデバイスのハードウェア Id の一覧の先頭に追加または移動します。

<span id="_______-______"></span> **-** 指定されたハードウェア Id をデバイスのハードウェア Id の一覧の末尾に追加または移動します。

<span id="______________"></span> **!**
デバイスのハードウェア Id の一覧から、指定されたハードウェア Id を削除します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

*ルートで列挙*されたデバイスとは、ルートレジストリサブキー (HKEY\_LOCAL\_MACHINE\\System\\*ControlSet*\\Enum\\root) に表示されるデバイスです。

各コマンドに複数のハードウェア Id を指定できます。 **!** (delete) パラメーターは、プレフィックスとして指定されているハードウェア ID にのみ適用されます。 その他のシンボルパラメーターは、コマンドの次のシンボルパラメーターまで続くすべてのハードウェア Id に適用されます。

指定したハードウェア ID がデバイスのハードウェア id の一覧に既に存在する場合、DevCon は追加ではなく、ハードウェア ID を移動します。

**DevCon SetHwIDs**コマンドの成功メッセージは、変更されたハードウェア id の数ではなく、ハードウェア id が変更されたデバイス (またはデバイスの一覧) の数を報告します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon sethwid @ROOT\LEGACY* := legacy
devcon sethwid @ROOT\LEGACY_AFD\0000 := =afd1 afd2 afd3
devcon sethwid legacy := devtype3 -devtype4
devcon sethwid legacy afd1 := +devtype3
devcon sethwid @ROOT\LEGACY_BEEP\0000 := !beep legacy
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 40: レガシデバイスにハードウェア ID を割り当てる](devcon-examples.md#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[例 41: リモートコンピューター上のすべてのレガシデバイスにハードウェア ID を追加する](devcon-examples.md#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[例 42: リモートコンピューター上のすべてのレガシデバイスからハードウェア ID を削除する](devcon-examples.md#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[例 43: ハードウェア Id を追加、削除、交換する](devcon-examples.md#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[例 44: HAL を強制的に更新する](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)
