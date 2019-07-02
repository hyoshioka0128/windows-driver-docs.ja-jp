---
title: DevCon Resources
description: 指定されたデバイスに割り当てられたリソースを一覧表示します。 リソースは、DMA チャネル、I/O ポート、IRQ、およびメモリ アドレスなどのバスの割り当てとアドレス指定可能なパスです。 ローカルおよびリモート コンピューターで有効です。
ms.assetid: 06bf2a5a-07a1-42b4-90db-ed74ce84d075
keywords:
- DevCon リソース ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Resources
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88e88079095a472b4721dfd06ff838a61190d0d4
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492513"
---
# <a name="devcon-resources"></a>DevCon Resources


指定されたデバイスに割り当てられたリソースを一覧表示します。 リソースは、DMA チャネル、I/O ポート、IRQ、およびメモリ アドレスなどのバスの割り当てとアドレス指定可能なパスです。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] resources {* | ID [ID ...] | =class [ID [ID...]]} 
```

## <a name="span-idddkdevconresourcestoolsspanspan-idddkdevconresourcestoolsspanparameters"></a><span id="ddk_devcon_resources_tools"></span><span id="DDK_DEVCON_RESOURCES_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\** <em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista と Windows の以降のバージョンを実行しているコンピューターで、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。



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



<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>デバイスのデバイス セットアップ クラスを指定します。 等号 (=) ( **=** ) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**リソース**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター、構文エラーを返さずに、ローカル コンピューター上のデバイスにリソースが割り当てられているが表示されます。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon resources *
devcon /m:\\server01 resources =media
devcon resources acpi* *port*
devcon resources =class port* (by class and hardware ID)
devcon resources =class @port*(by class and device instance ID)
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[12 の例:デバイスのクラスのリソースを一覧表示](devcon-examples.md#ddk_example_12_list_resources_of_a_class_of_devices_tools)

[13 の使用例:デバイス ID でリモート コンピューター上のリソースを一覧表示](devcon-examples.md#ddk_example_13_list_resources_of_device_on_a_remote_computer_by_id_too)









