---
title: DevCon Find
description: コンピューターに現在接続されているすべてのデバイスを検索します。 デバイスインスタンス ID とデバイスの説明が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。
ms.assetid: ecd72b34-4117-4360-95d2-e87702f025a1
keywords:
- DevCon Find ドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Find
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09e57ccfd171567ba78e37baa69225c97fbb3e65
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038085"
---
# <a name="devcon-find"></a>DevCon Find

コンピューターに現在接続されているすべてのデバイスを検索します。 デバイスインスタンス ID とデバイスの説明が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] find {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_find_toolsspanspan-idddk_devcon_find_toolsspanparameters"></a><span id="ddk_devcon_find_tools"></span><span id="DDK_DEVCON_FIND_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\** <em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

**メモ**  リモートコンピューターで DevCon コマンドを実行するには、グループポリシー設定で、プラグアンドプレイサービスをリモートコンピューターで実行できるようにする必要があります。 Windows Vista および Windows 7 を実行しているコンピューターでは、グループポリシーによって、サービスへのリモートアクセスが既定で無効になります。 WDK 8.1 および WDK 8 を実行するコンピューターでは、リモートアクセスは使用できません。

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

**/M**パラメーターは、操作名 (**find**) の前に記述する必要があります。 それ以外の場合、DevCon は、 **/m**パラメーターを無視し、構文エラーを返さずにローカルコンピューターを検索します。

**DevCon find**操作を使用すると、ハードウェア ID や id パターンではなく、デバイスの完全なデバイスインスタンス ID を指定することにより、現在コンピューターに接続されていないデバイスを見つけることができます。 完全なデバイスインスタンス ID を指定すると、それを添付デバイスに制限する、 **DevCon Find**操作の制限が上書きされます。

1つのクラス引数を持つ**Devcon Find**操作は、 [**devcon listclass**](devcon-listclass.md)操作と同じです。

現在コンピューターに接続されていないデバイスを含め、すべてのデバイスを検索するには、 [**DevCon FindAll**](devcon-findall.md)操作を使用します。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon find *
devcon find =media *pnp*
devcon /m:\\Server01 find *mou*
devcon find @*hub*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 20: ハードウェア ID パターン別にデバイスを検索する](devcon-examples.md#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[例 21: デバイスインスタンス ID またはクラスを使用してデバイスを検索する](devcon-examples.md#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)
