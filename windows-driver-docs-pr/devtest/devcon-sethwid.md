---
title: DevCon SetHwID
description: 追加、削除、および、ローカルまたはリモート コンピューター上のルートで列挙されるデバイスのハードウェア Id の順序を変更します。
ms.assetid: 79948ff0-8b30-4a64-beea-e3f08aef7170
keywords:
- DevCon SetHwID ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon SetHwID
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25fb7501bde304f36b5fcf3868455ee8f2c022cd
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349119"
---
# <a name="devcon-sethwid"></a>DevCon SetHwID


追加、削除、および、ローカルまたはリモート コンピューター上のルートで列挙されるデバイスのハードウェア Id の順序を変更します。

```
    devcon [/m:\\computer] sethwid {* | ID [ID ...] | =class [ID [ID ...]]} := [ = | + | - | ! ]HardwareIDs ...
```

## <a name="span-idddkdevconsethwidtoolsspanspan-idddkdevconsethwidtoolsspanparameters"></a><span id="ddk_devcon_sethwid_tools"></span><span id="DDK_DEVCON_SETHWID_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



<span id="______________"></span> **\\***   
コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
ハードウェア ID、互換性 ID、またはデバイスのデバイス インスタンス ID のすべてまたは一部を指定します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字を含む Id (**&**) 引用符で囲む必要があります。

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
<td align="left"><p>任意の文字または文字と一致します。 ワイルドカード文字を使用して (</em>) パターンを作成する、ID、たとえば、<em>ディスク</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>@</strong></p></td>
<td align="left"><p>たとえば、デバイス インスタンス ID を示します <strong><xref href="ROOT\FTDISK\0000" data-throw-if-not-resolved="False" data-raw-source="@ROOT\FTDISK\0000"></xref></strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>'</strong></p>
<p>(一重引用符)</p></td>
<td align="left"><p>リテラル文字列と一致する (正確に表示される)。 示すアスタリスクは、ID 名の一部であるし、たとえば、ワイルドカード文字ではないは、単一引用符を含む文字列の前に<strong>' * PNP0600</strong>ここで、* PNP0600 ハードウェア ID (アスタリスクを含む) です。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>クラス</em>ルートで列挙されるデバイスのデバイス セットアップ クラスを指定します。 等号 (=) (**=**) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

<span id="_______HardwareIDs______"></span><span id="_______hardwareids______"></span><span id="_______HARDWAREIDS______"></span> *HardwareIDs*   
1 つまたは複数のハードウェア Id を指定します。

シンボル パラメーター ハードウェア Id が付いていないかどうか (**+**、 **-**、 **=**、 **!**)、DevCon を追加または指定したハードウェア Id を指定した順序でデバイスのハードウェア Id のリストの末尾に移動します。 これは、パラメーターと同じです。

<span id="_"></span>=  
デバイスのハードウェア Id の一覧を指定した順序で指定されたハードウェア Id に置き換えます。

<span id="______________"></span> **+**   
追加するか、指定されたハードウェア Id をデバイスのハードウェア Id のリストの先頭に移動します。

<span id="_______-______"></span> **-**   
追加するか、指定されたハードウェア Id をデバイスのハードウェア Id のリストの末尾に移動します。

<span id="______________"></span> **!**   
デバイスのハードウェア Id の一覧から、指定したハードウェア Id を削除します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

A*ルート列挙*デバイスは、ルートのレジストリ サブキーに表示されるデバイス (HKEY\_ローカル\_マシン\\システム\\*ControlSet* \\列挙型\\ルート)。

各コマンドでは、複数のハードウェア Id を指定できます。 **!** (削除) パラメーター プレフィックス、ハードウェア ID にのみ適用されます。 他のシンボルのパラメーターは、次のコマンドでは、次のシンボル パラメーターまで Id のすべてのハードウェアに適用されます。

DevCon 移動するではなくよりも、追加すると、指定されたハードウェア ID を既に場合は、ハードウェア ID が存在するデバイスのハードウェア Id の一覧で。

成功メッセージ、 **DevCon SetHwIDs**コマンドは、ハードウェア Id、変更されたハードウェア Id の数ではなく、変更がデバイス (またはデバイスのリスト) の数を報告します。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon sethwid @ROOT\LEGACY* := legacy
devcon sethwid @ROOT\LEGACY_AFD\0000 := =afd1 afd2 afd3
devcon sethwid legacy := devtype3 -devtype4
devcon sethwid legacy afd1 := +devtype3
devcon sethwid @ROOT\LEGACY_BEEP\0000 := !beep legacy
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[40 の使用例:レガシ デバイスのハードウェア ID を割り当てる](devcon-examples.md#ddk_example_40_assign_a_hardware_id_to_a_legacy_device_tools)

[41 の使用例:リモート コンピューター上のすべてのレガシ デバイスにハードウェア ID を追加します。](devcon-examples.md#ddk_example_41_add_a_hardware_id_to_all_legacy_devices_on_a_remote_com)

[42 の使用例:リモート コンピューター上のすべてのレガシ デバイスからのハードウェア ID を削除します。](devcon-examples.md#ddk_example_42_delete_a_hardware_id_from_all_legacy_devices_on_a_remot)

[43 の使用例:追加、削除、およびハードウェア Id を置き換えます](devcon-examples.md#ddk_example_43_add_delete_and_replace_hardwareids_tools)

[例 44:HAL を強制的に更新します。](devcon-examples.md#ddk_example_44_forcibly_update_the_hal_tools)









