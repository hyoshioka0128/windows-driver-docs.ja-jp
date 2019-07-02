---
title: DevCon Stack
description: 指定のデバイスと、GUID、各デバイスのデバイス セットアップ クラスの名前の予期されるドライバー スタックが表示されます。
ms.assetid: c06436d2-da66-4eb2-89ed-a1832967cdbb
keywords:
- DevCon Stack ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon Stack
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9060671e608f96d637092a051d05686664b1cb97
ms.sourcegitcommit: 289b5f97aff1b9ea1fefc9a8731e0fc16533073b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492503"
---
# <a name="devcon-stack"></a>DevCon Stack


指定のデバイスと、GUID、各デバイスのデバイス セットアップ クラスの名前の予期されるドライバー スタックが表示されます。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] stack {* | ID [ID ...] | =class [ID [ID...]]} 
```

## <a name="span-idddkdevconstacktoolsspanspan-idddkdevconstacktoolsspanparameters"></a><span id="ddk_devcon_stack_tools"></span><span id="DDK_DEVCON_STACK_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\** <em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista および Windows 7 を実行するコンピューター、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。 WDK 8 WDK 8.1 を実行するコンピューターでリモート アクセスでは使用できません。



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



<span id="________class______"></span><span id="________CLASS______"></span> **=** <em>クラス</em>デバイスのデバイス セットアップ クラスを指定します。 等号 (=) ( **=** ) クラスの名前として文字列を識別します。 ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**スタック**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター構文エラーを返さずに、ローカル コンピューター上のデバイス ドライバーのスタックを表示します。

**DevCon スタック**操作には、デバイスの必要なドライバー スタックが表示されます。 通常、実際のドライバー スタックには、予想されるスタックが一致するがのバリエーションが可能です。

デバイスの問題を調査するには、デバイスを使用して、実際のドライバー スタック操作から必要なドライバー スタック比較によって表示される、 [ **DevCon DriverFiles** ](devcon-driverfiles.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon /m:\\Server01 stack * > Server01Stack.txt
devcon stack ISAPNP\ReadDataPort
devcon /m:\\Server01 stack pci* 
devcon stack =multifunction
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[14 の使用例:記憶装置のドライバー スタックを表示します。](devcon-examples.md#ddk_example_14_display_the_driver_stack_for_storage_devices_tools)

[15 の使用例:デバイスのセットアップ クラスを見つける](devcon-examples.md#ddk_example_15_find_the_setup_class_of_a_device_tools)

[16 の使用例:リモート コンピューターに関連するデバイスの履歴を表示します。](devcon-examples.md#ddk_example_16_display_the_stack_for_related_devices_on_a_remote_compu)









