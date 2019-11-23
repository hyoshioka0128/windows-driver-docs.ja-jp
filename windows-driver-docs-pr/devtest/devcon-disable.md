---
title: DevCon Disable
description: コンピューター上のデバイスを無効にします。
ms.assetid: 544b219c-30dd-41d1-ac47-9760c772b07e
keywords:
- DevCon ドライバー開発ツールを無効にする
topic_type:
- apiref
api_name:
- DevCon Disable
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15e0d6acb1362c95da329ce608b8a5f1bcdb8061
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038091"
---
# <a name="devcon-disable"></a>DevCon Disable

コンピューター上のデバイスを無効にします。 ローカルコンピューター上でのみ有効です。

デバイスを*無効*にすると、デバイスはコンピューターに物理的に接続されたままになりますが、そのドライバーはメモリからアンロードされ、デバイスを使用できないようにリソースが解放されます。

```
    devcon [/r] disable {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_disable_toolsspanspan-idddk_devcon_disable_toolsspanparameters"></a><span id="ddk_devcon_disable_tools"></span><span id="DDK_DEVCON_DISABLE_TOOLS"></span>パラメータ

<span id="________r______"></span><span id="________R______"></span> **/r**条件付き再起動。 変更を有効にするために再起動が必要な場合にのみ、操作の完了後にシステムを再起動します。

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

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

デバイスが既に無効になっている場合でも、DevCon はデバイスを無効にします。 デバイスを無効にする前と後に、[ [**DevCon status**](devcon-status.md) ] 操作を使用してデバイスの状態を確認します。

デバイスを無効にするために ID パターンを使用する前に、影響を受けるデバイスを決定します。 これを行うには、 **devcon STATUS USB\\** * または * * DEVCON hwids USB\\* * * のように、表示コマンドでパターンを使用します。

この変更を有効にするには、システムを再起動する必要がある場合があります。 システムを DevCon で再起動するには、条件付き再起動パラメーター (/r) をコマンドに追加します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon disable * (not recommended)
devcon /r disable *DVD-ROM*
devcon /r disable =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 30: デバイスを ID パターンで無効にする](devcon-examples.md#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[例 31: デバイスインスタンス ID でデバイスを無効にする](devcon-examples.md#ddk_example_31_disable_devices_by_device_instance_id_tools)
