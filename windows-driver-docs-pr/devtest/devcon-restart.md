---
title: DevCon Restart
description: 指定されたデバイスを停止して再起動します。 ローカルコンピューター上でのみ有効です。
ms.assetid: 3d16435d-e80d-408c-8e61-fad4a5aa7b9b
keywords:
- DevCon 再起動ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Restart
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ffd984594d2364810fef300738dec1665cb5728c
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038083"
---
# <a name="devcon-restart"></a>DevCon Restart

指定されたデバイスを停止して再起動します。 ローカルコンピューター上でのみ有効です。

```
    devcon [/r] restart {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_restart_toolsspanspan-idddk_devcon_restart_toolsspanparameters"></a><span id="ddk_devcon_restart_tools"></span><span id="DDK_DEVCON_RESTART_TOOLS"></span>パラメータ

<span id="________r______"></span><span id="________R______"></span> **/r**条件付き再起動。 変更を有効にするために再起動が必要な場合にのみ、操作の完了後にシステムを再起動します。

<span id="______________"></span> **\*** コンピューター上のすべてのデバイスを表します。

<span id="_______ID______"></span><span id="_______id______"></span>*Id*は、デバイスのハードウェア id、互換性 ID、またはデバイスインスタンス ID のすべてまたは一部を指定します。 複数の Id を指定する場合は、各 ID の間にスペースを入力します。 アンパサンド文字 ( **&** ) を含む id は引用符で囲む必要があります。

次の特殊文字は、ID パラメーターを変更します。

<table>  
<colgroup> <col width="50%" /> <col width="50%" /> </colgroup>  
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
<td align="left"><p>文字列を文字どおり (表示されているとおりに) 照合します。 アスタリスクが ID 名の一部であり、ワイルドカード文字 (アスタリスクを含む) がハードウェア ID であることを示すため<strong>に、文字列</strong>の前に1つの引用符を付けて指定します。</p></td>
</tr>
</tbody>
</table>

<span id="________class______"></span><span id="________CLASS______"></span>  

**=** _クラス_は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

この変更を有効にするには、システムを再起動する必要がある場合があります。 システムを DevCon で再起動するには、条件付き再起動パラメーター (/r) をコマンドに追加します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon restart *
devcon restart pci*
devcon restart "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon restart =printer
devcon restart =printer *desk*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

[例 38: デバイスを再起動する](devcon-examples.md#ddk_example_38_restart_a_device_tools)
