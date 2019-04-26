---
title: DevCon HwIDs
description: ハードウェア Id、互換性 Id、および、指定したデバイスのデバイス インスタンス Id が表示されます。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: b76de01e-fedf-41c2-ba2e-837b442ab93f
keywords:
- DevCon HwIDs ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon HwIDs
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 011bd34e2fe64b228485b341bed5330079ff1620
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348318"
---
# <a name="devcon-hwids"></a>DevCon HwIDs


ハードウェア Id、互換性 Id、および、指定したデバイスのデバイス インスタンス Id が表示されます。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] hwids {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconhwidstoolsspanspan-idddkdevconhwidstoolsspanparameters"></a><span id="ddk_devcon_hwids_tools"></span><span id="DDK_DEVCON_HWIDS_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



<span id="______________"></span> **\\***   
コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
1 つまたは複数のデバイスを指定するには、識別子を使用します。

ハードウェア ID、互換性 ID、またはデバイスのデバイス インスタンス ID のすべてまたは一部を入力します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字を含む Id (**&**) 引用符で囲む必要があります。

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
<td align="left"><p>任意の文字または文字と一致します。 ワイルドカード文字を使用して (<strong></em></strong>) パターンを作成する、ID、たとえば、 <strong><em>ディスク</em></strong>します。</p></td>
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



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>クラス</em>セットアップ クラスを使用して 1 つまたは複数のデバイスを指定します。

デバイスのセットアップ クラスの名前の全部または一部を入力します。 等号 (=) (**=**) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**hwids**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター、構文エラーを返さずに、ローカル コンピューター上のデバイスのハードウェア Id が表示されます。

ルートで列挙されるデバイスのハードウェア ID を作成するには、使用、 [ **DevCon SetHwID** ](devcon-sethwid.md)コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon hwids *
devcon /m:\\server01 hwids acpi* 
devcon hwids acpi* *port*
devcon hwids =usb
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 1:すべてのハードウェア Id を検索します。](devcon-examples.md#ddk_example_1_find_all_hardware_ids_tools)

[例 2:パターンを使用して、ハードウェア Id を検索します。](devcon-examples.md#ddk_example_2_find_hardware_ids_by_using_a_pattern_tools)

[例 3:クラスを使用して、ハードウェア Id を検索します。](devcon-examples.md#ddk_example_3_find_hardware_ids_by_using_a_class_tools)









