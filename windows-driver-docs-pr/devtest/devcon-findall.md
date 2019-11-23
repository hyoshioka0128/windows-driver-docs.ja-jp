---
title: DevCon FindAll
description: コンピューターに接続されていても切断または移動されているデバイスを含め、コンピューター上のすべてのデバイスを検索します。
ms.assetid: 63148bb4-dc54-4b82-9e8f-d6967ad86d74
keywords:
- DevCon FindAll ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon FindAll
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f0035362447daa94d657b9a5fd107504b7d33e0
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038044"
---
# <a name="devcon-findall"></a>DevCon FindAll

コンピューターに接続されていても切断または移動されているデバイスを含め、コンピューター上のすべてのデバイスを検索します。 (これらは非存在デバイスまたは*ファントム*デバイスと呼ばれます)。また、 **DevCon FindAll**操作は、BIOS の変更の結果として異なる方法で列挙されたデバイスも検索します。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] findall {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_findall_toolsspanspan-idddk_devcon_findall_toolsspanparameters"></a><span id="ddk_devcon_findall_tools"></span><span id="DDK_DEVCON_FINDALL_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

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
<td align="left"><p>文字列を文字どおり (表示されているとおりに) 照合します。 アスタリスクが ID 名の一部で、ワイルドカード文字ではないことを示すには、文字列の前に単一引用符を付けます。たとえば、 <strong>' * PNP0600</strong>,、* PNP0600 (アスタリスクを含む) はハードウェア ID です。</p></td>
</tr>
</tbody>
</table>  

<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**/M**パラメーターは、操作名 (**findall**) の前に記述する必要があります。 それ以外の場合、DevCon は、 **/m**パラメーターを無視し、構文エラーを返さずにローカルコンピューターを検索します。

コンピューターに現在接続されているデバイスのみを検索するには、 [**DevCon find**](devcon-find.md)操作を使用します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon resources STORAGE\Volume
devcon resources =ports lpt*
devcon resources @pci*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>よう

[例 22: セットアップクラスですべてのデバイスを検索 (および検索する)](devcon-examples.md#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)
