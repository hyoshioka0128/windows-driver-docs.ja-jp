---
title: DevCon Resources
description: 指定したデバイスに割り当てられているリソースを一覧表示します。 リソースには、DMA チャネル、i/o ポート、IRQ、メモリアドレスなど、割り当て可能でアドレス指定が可能なバスパスがあります。 ローカルコンピューターとリモートコンピューターで有効です。
ms.assetid: 06bf2a5a-07a1-42b4-90db-ed74ce84d075
keywords:
- DevCon Resources ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Resources
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23b3e110875149291c06ae52d5f64f0acdafe815
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038041"
---
# <a name="devcon-resources"></a>DevCon Resources

指定したデバイスに割り当てられているリソースを一覧表示します。 リソースには、DMA チャネル、i/o ポート、IRQ、メモリアドレスなど、割り当て可能でアドレス指定が可能なバスパスがあります。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] resources {* | ID [ID ...] | =class [ID [ID...]]}
```

## <a name="span-idddk_devcon_resources_toolsspanspan-idddk_devcon_resources_toolsspanparameters"></a><span id="ddk_devcon_resources_tools"></span><span id="DDK_DEVCON_RESOURCES_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m: \\ @ no__t**<em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

**メモ**  リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista 以降のバージョンの Windows を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。

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
<td align="left"><p>文字列を文字どおり (表示されているとおりに) 照合します。 アスタリスクが ID 名の一部であり、ワイルドカード文字 (アスタリスクを含む) がハードウェア ID であることを示すため<strong>に、文字列</strong>の前に1つの引用符を付けて指定します。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**/M**パラメーターは操作名 (**resources**) の前に記述する必要があります。 それ以外の場合、DevCon は **/m**パラメーターを無視し、構文エラーを返さずに、ローカルコンピューター上のデバイスに割り当てられたリソースを表示します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon resources *
devcon /m:\\server01 resources =media
devcon resources acpi* *port*
devcon resources =class port* (by class and hardware ID)
devcon resources =class @port*(by class and device instance ID)
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[Example 12:デバイスのクラスのリソースを一覧表示する @ no__t-0

[Example 13:リモートコンピューター上のデバイスのリソースを一覧表示する ID @ no__t-0
