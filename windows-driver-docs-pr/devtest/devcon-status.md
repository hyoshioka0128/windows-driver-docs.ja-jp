---
title: DevCon Status
description: コンピューター上のデバイスのドライバーの状態 (実行中、停止、または無効) が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。
ms.assetid: 97da6df4-ad93-440a-9136-13f2b79cbe9c
keywords:
- DevCon ステータスドライバー開発ツール
topic_type:
- apiref
api_name:
- DevCon Status
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17b8eebf064e9c63c60823701a026b97ca59534c
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038031"
---
# <a name="devcon-status"></a>DevCon Status

コンピューター上のデバイスのドライバーの状態 (実行中、停止、または無効) が表示されます。 ローカルコンピューターとリモートコンピューターで有効です。

```
    devcon [/m:\\computer] status {* | ID [ID ...] | =class [ID [ID ...]]}
```

## <a name="span-idddk_devcon_status_toolsspanspan-idddk_devcon_status_toolsspanparameters"></a><span id="ddk_devcon_status_tools"></span><span id="DDK_DEVCON_STATUS_TOOLS"></span>パラメータ

<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m: \\ @ no__t**<em>コンピューター</em>は、指定されたリモートコンピューターでコマンドを実行します。 円記号が必要です。

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

<span id="________class______"></span><span id="________CLASS______"></span> **=** _クラス_は、デバイスのデバイスセットアップクラスを指定します。 等号 ( **=** ) は、文字列をクラス名として識別します。

また、クラス名の後に、ハードウェア Id、互換性のある Id、デバイスインスタンス Id、または ID パターンを指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定された Id に一致するデバイスをクラスで検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>Comments

**/M**パラメーターは、操作名 (**状態**) の前に記述する必要があります。 それ以外の場合、DevCon は **/m**パラメーターを無視し、構文エラーを返さずに、ローカルコンピューター上のデバイスドライバーの状態を表示します。

デバイスがコンピューターに接続されていないときなど、DevCon がデバイスの状態を判断できない場合は、ステータス表示の状態を説明する行を省略します。

次の例は、status コマンドが成功したことを示しています。 デバイスの状態を説明するテキストは、太字で表示されます。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
    Driver is running.
1 matching device(s) found.
```

これに対して、次の例では、DevCon が検出できないデバイスの状態を表示する方法を示しています。 表示に状態の説明がありません。

```
STORAGE\VOLUME\1&30A96598&0&SIGNATURE80OFFSET7E0000LENGTH270987600
    Name: Generic volume
1 matching device(s) found.
```

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>使用例

```
devcon /m:\\Server01 status *
devcon status pci*
devcon status "PCI\VEN_115D&DEV_0003&SUBSYS_0181115D"
devcon status =printer
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[Example 17:ローカルコンピューター上のすべてのデバイスの状態を表示する @ no__t-0

[Example 18:デバイスインスタンス ID @ no__t でデバイスの状態を表示します。

[Example 19:リモートコンピューターの関連デバイスの状態を表示する @ no__t-0
