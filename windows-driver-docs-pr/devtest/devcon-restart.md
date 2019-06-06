---
title: DevCon Restart
description: 停止し、指定したデバイスを再起動します。 ローカル コンピューターでのみ有効です。
ms.assetid: 3d16435d-e80d-408c-8e61-fad4a5aa7b9b
keywords:
- DevCon 再起動ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Restart
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42d2599dd3437b17f6d09acdbf7e6c14b3f6f305
ms.sourcegitcommit: e542212bb5e7aba06b9e005e9b63c438404d5643
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719957"
---
# <a name="devcon-restart"></a>DevCon Restart


停止し、指定したデバイスを再起動します。 ローカル コンピューターでのみ有効です。

```
    devcon [/r] restart {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconrestarttoolsspanspan-idddkdevconrestarttoolsspanparameters"></a><span id="ddk_devcon_restart_tools"></span><span id="DDK_DEVCON_RESTART_TOOLS"></span>パラメーター


<span id="________r______"></span><span id="________R______"></span> **/r**   
条件付き再起動します。 再起動が必要な変更を有効にする場合にのみ操作を完了した後、システムを再起動します。

<span id="______________"></span> **\\** *   
コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span> *ID*   
ハードウェア ID、互換性 ID、またはデバイスのデバイス インスタンス ID のすべてまたは一部を指定します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字を含む Id ( **&** ) 引用符で囲む必要があります。

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



<span id="________class______"></span><span id="________CLASS______"></span> **=** _クラス_   
デバイスのデバイス セットアップ クラスを指定します。 等号 (=) ( **=** ) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

システムは、この変更を有効にするを再起動する必要があります。 DevCon システムを再起動するのには、再起動の条件付きパラメーターを追加します (/r) コマンド。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon restart *
devcon restart pci*
devcon restart "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon restart =printer
devcon restart =printer *desk*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[38 の使用例:デバイスを再起動します。](devcon-examples.md#ddk_example_38_restart_a_device_tools)









