---
title: DevCon Remove
description: デバイスが、デバイス ツリーから削除し、デバイスのデバイス スタックを削除します。
ms.assetid: 02236d0d-4628-4b5b-9a15-331905f07358
keywords:
- Driver DevCon 開発ツール
topic_type:
- apiref
api_name:
- DevCon Remove
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ceb1c89eda188a0620a65486bb93c8c51f1a3d14
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350411"
---
# <a name="devcon-remove"></a>DevCon Remove


デバイスが、デバイス ツリーから削除し、デバイスのデバイス スタックを削除します。 これらのアクションの結果として子デバイスは、デバイス ツリーから削除され、デバイスをサポートするドライバーは読み込まれません。

この操作では、デバイス ドライバーまたはデバイスにインストールされているすべてのファイルは削除されません。 デバイスを削除した後には、デバイス ツリーから、ファイルは残り、デバイスが再度を列挙することができますが、存在デバイスとして内部的に表現もします。

ローカル コンピューターでのみ有効です。

```
    devcon [/r] remove {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconremovetoolsspanspan-idddkdevconremovetoolsspanparameters"></a><span id="ddk_devcon_remove_tools"></span><span id="DDK_DEVCON_REMOVE_TOOLS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

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

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (/r) コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon /r remove "PCI\VEN_8086&DEV_7110" 
devcon /r remove =printer
devcon /r remove =printer *deskj*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[35 の使用例:デバイス インスタンス ID のパターンによってデバイスを削除します。](devcon-examples.md#ddk_example_35_remove_devices_by_device_instance_id_pattern_tools)

[36 の使用例:特定のネットワーク デバイスを削除します。](devcon-examples.md#ddk_example_36_remove_a_particular_network_device_tools)









