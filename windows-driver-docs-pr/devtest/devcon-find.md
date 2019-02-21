---
title: DevCon 検索
description: 現在のコンピューターに接続されているすべてのデバイスを検索します。 デバイス インスタンス ID とデバイスの説明が表示されます。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: ecd72b34-4117-4360-95d2-e87702f025a1
keywords:
- DevCon 検索ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Find
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fadc15cd43584f7e471560a4abc7f2194b055e1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527399"
---
# <a name="devcon-find"></a>DevCon 検索


現在のコンピューターに接続されているすべてのデバイスを検索します。 デバイス インスタンス ID とデバイスの説明が表示されます。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] find {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconfindtoolsspanspan-idddkdevconfindtoolsspanparameters"></a><span id="ddk_devcon_find_tools"></span><span id="DDK_DEVCON_FIND_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



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
<td align="left"><p><strong>&#39;</strong></p>
<p>(一重引用符)</p></td>
<td align="left"><p>リテラル文字列と一致する (正確に表示される)。 示すアスタリスクは、ID 名の一部であるし、たとえば、ワイルドカード文字ではないは、単一引用符を含む文字列の前に <strong>&#39;* PNP0600</strong>ここで、* PNP0600 ハードウェア ID (アスタリスクを含む) です。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>クラス</em>デバイスのデバイス セットアップ クラスを指定します。 等号 (=) (**=**) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**検索**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター構文エラーを返さずに、ローカル コンピューターを検索します。

使用することができます、 **DevCon 検索**ハードウェア ID または ID のパターンを代わりに接続していないコンピューターにデバイスの完全なデバイス インスタンス ID を指定することでデバイスを検索する操作。 制限をオーバーライドする完全なデバイス インスタンス ID を指定する、 **DevCon 検索**に制限される操作には、デバイスが接続されています。

**DevCon 検索**と同じ操作を 1 つのクラスの引数です、 [ **DevCon ListClass** ](devcon-listclass.md)操作。

現在、コンピューターに接続されていないものも含め、すべてのデバイスを検索するには使用、 [ **DevCon FindAll** ](devcon-findall.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon find *
devcon find =media *pnp*
devcon /m:\\Server01 find *mou* 
devcon find @*hub*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[20 の使用例:ハードウェア ID のパターンでデバイスを検索します。](devcon-examples.md#ddk_example_20_find_devices_by_hardware_id_pattern_tools)

[21 の使用例:デバイス インスタンス ID またはクラスによってデバイスを検索します。](devcon-examples.md#ddk_example_21_find_devices_by_device_instance_id_or_class_tools)









