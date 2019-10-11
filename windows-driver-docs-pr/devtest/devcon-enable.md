---
title: DevCon Enable
description: コンピューター上のデバイスを有効にします。 ローカルコンピューター上でのみ有効です。デバイスを有効にするには、デバイスドライバーがメモリに読み込まれ、デバイスが使用できる状態になっていることを意味します。
ms.assetid: 2fb2cb9b-ba37-4946-b78b-0cd2aaaadcb4
keywords:
- DevCon ドライバー開発ツールを有効にする
topic_type:
- apiref
api_name:
- DevCon Enable
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5fd66207df6fbdb11d38a2f9f9606fcc68f3886a
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038089"
---
# <a name="devcon-enable"></a>DevCon Enable

コンピューター上のデバイスを有効にします。 ローカルコンピューター上でのみ有効です。

デバイスを*有効*にするには、デバイスドライバーがメモリに読み込まれ、デバイスが使用できる状態になっていることを意味します。

```
    devcon [/r] enable {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_enable_toolsspanspan-idddk_devcon_enable_toolsspanparameters"></a><span id="ddk_devcon_enable_tools"></span><span id="DDK_DEVCON_ENABLE_TOOLS"></span>パラメータ

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

<span id="________class______"></span><span id="________CLASS______"></span> *= クラス*デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

DevCon は、既に有効になっている場合でもデバイスを有効にします。 デバイスを有効にする前と後に、[ [**DevCon status**](devcon-status.md) ] 操作を使用してデバイスの状態を確認します。

この変更を有効にするには、システムを再起動する必要がある場合があります。 システムを DevCon で再起動するには、条件付き再起動パラメーター (/r) をコマンドに追加します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon enable * (not recommended)
devcon /r enable *DVD-ROM*
devcon /r enable =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[Example 28:特定のデバイスを有効にする @ no__t-0

[Example 29:クラス @ no__t でデバイスを有効にする-0
