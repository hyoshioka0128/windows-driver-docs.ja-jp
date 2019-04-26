---
title: DevCon Disable
description: コンピューター上のデバイスを無効にします。
ms.assetid: 544b219c-30dd-41d1-ac47-9760c772b07e
keywords:
- DevCon 無効にするドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Disable
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 528cb08b5a393d9814d2955dd18b8b5ce8210bf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341686"
---
# <a name="devcon-disable"></a>DevCon Disable


コンピューター上のデバイスを無効にします。 ローカル コンピューターでのみ有効です。

*を無効にする*デバイスにより、コンピューターに物理的に接続されたデバイスに残りますが、そのドライバーは、メモリからアンロードされのリソースが解放されるように、デバイスを使用することはできません。

```
    devcon [/r] disable {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevcondisabletoolsspanspan-idddkdevcondisabletoolsspanparameters"></a><span id="ddk_devcon_disable_tools"></span><span id="DDK_DEVCON_DISABLE_TOOLS"></span>パラメーター


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

DevCon には、デバイスが既に無効になっている場合でも、デバイスが無効にします。 前に、と、デバイスを無効にした後にを使用して、 [ **DevCon 状態**](devcon-status.md)操作をデバイスの状態を確認します。

デバイスを無効にする、ID のパターンを使用する前に、影響を受けるデバイスを決定します。 表示コマンドで使用してパターンをなどを行うに**devcon 状態 USB\\*** または * * devcon hwids USB\\* * *。

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (/r) コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon disable * (not recommended)
devcon /r disable *DVD-ROM*
devcon /r disable =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[30 の使用例:ID、パターンによってデバイスを無効にします。](devcon-examples.md#ddk_example_30_disable_devices_by_an_id_pattern_tools)

[31 の使用例:デバイス インスタンス ID でデバイスを無効にします。](devcon-examples.md#ddk_example_31_disable_devices_by_device_instance_id_tools)









