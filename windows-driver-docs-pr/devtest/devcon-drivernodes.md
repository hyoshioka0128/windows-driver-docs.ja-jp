---
title: DevCon DriverNodes
description: デバイスと互換性のあるすべてのドライバーパッケージを、そのバージョンと順位と共に一覧表示します。 ローカルコンピューター上でのみ有効です。
ms.assetid: 891aa022-44f5-4920-ab57-a0573deb94de
keywords:
- DevCon DriverNodes ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon DriverNodes
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c28becefa0e6664c25df59b1226e9158505cf29
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038063"
---
# <a name="devcon-drivernodes"></a>DevCon DriverNodes

デバイスと互換性のあるすべての[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/components-of-a-driver-package)を、そのバージョンと順位と共に一覧表示します。 ローカルコンピューター上でのみ有効です。

```
    devcon drivernodes {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_drivernodes_toolsspanspan-idddk_devcon_drivernodes_toolsspanparameters"></a><span id="ddk_devcon_drivernodes_tools"></span><span id="DDK_DEVCON_DRIVERNODES_TOOLS"></span>パラメータ

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
<td align="left"><p>任意の文字または文字を検索しません。 ワイルドカード文字 (<strong> @ no__t) を使用して、<strong><em>ディスク</em></strong>などの ID パターンを作成します。</p></td>
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

<span id="________class______"></span><span id="________CLASS______"></span> **=** _クラス_は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**DevCon DriverNodes**操作は、ローカルコンピューター上でのみ実行されます。

**DevCon DriverNodes**操作は、セットアップの問題のトラブルシューティングに特に役立ちます。 たとえば、Windows の INF ファイルまたはカスタマイズされたサードパーティ製の INF ファイルがデバイスで使用されているかどうかを判断するために使用できます。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon drivernodes *
devcon drivernodes *miniport*
devcon drivernodes =usb pci* usb*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[Example 10:ドライバーパッケージをハードウェア ID パターン @ no__t で一覧表示する

[Example 11:デバイスインスタンス ID パターンを使ってドライバーパッケージを一覧表示する @ no__t-0
