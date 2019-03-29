---
title: DevCon Status
description: コンピューター上のデバイス ドライバーの状態 (実行中、停止、または無効になっている) を表示します。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: 97da6df4-ad93-440a-9136-13f2b79cbe9c
keywords:
- DevCon 状態ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Status
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc953b6321d7ab703d139dfb8926d213fab39866
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349683"
---
# <a name="devcon-status"></a>DevCon Status


コンピューター上のデバイス ドライバーの状態 (実行中、停止、または無効になっている) を表示します。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] status {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconstatustoolsspanspan-idddkdevconstatustoolsspanparameters"></a><span id="ddk_devcon_status_tools"></span><span id="DDK_DEVCON_STATUS_TOOLS"></span>パラメーター


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



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>クラス</em>デバイスのデバイス セットアップ クラスを指定します。 等号 (=) (**=**) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**状態**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーターと、構文エラーを返さずに、ローカル コンピューター上のデバイス ドライバーの状態を表示します。

DevCon、ときに、デバイスは、コンピューターにアタッチされなくなど、デバイスの状態を判断できない場合、DevCon は状態の表示からステータスを記述する行を省略します。

次の例では、正常な状態のコマンドを示します。 デバイスの状態を説明するテキストが太字で表示されます。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
    Driver is running.
1 matching device(s) found.
```

これに対し、次の例では、DevCon が含まれていないデバイスの状態を表示する方法を示しています。 状態の説明が表示されません。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
1 matching device(s) found.
```

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon /m:\\Server01 status *
devcon status pci*
devcon status "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon status =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[17 の使用例:ローカル コンピューターのすべてのデバイスの状態を表示します。](devcon-examples.md#ddk_example_17_display_the_status_of_all_devices_on_the_local_computer)

[18 の使用例:デバイス インスタンス ID の状態を表示します。](devcon-examples.md#ddk_example_18_display_the_status_of_a_device_by_device_instance_id_to)

[19 の使用例:リモート コンピューターに関連するデバイスの状態を表示します。](devcon-examples.md#ddk_example_19_display_the_status_of_related_devices_on_a_remote_compu)









