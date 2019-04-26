---
title: DevCon FindAll
description: コンピューターのコンピューターに接続された 1 回がデタッチまたは移動されたデバイスを含め、すべてのデバイスを検索します。
ms.assetid: 63148bb4-dc54-4b82-9e8f-d6967ad86d74
keywords:
- DevCon FindAll ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon FindAll
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf7de1608c61f3463f7c1381c10f35be56292597
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347673"
---
# <a name="devcon-findall"></a>DevCon FindAll


コンピューターのコンピューターに接続された 1 回がデタッチまたは移動されたデバイスを含め、すべてのデバイスを検索します。 (これらは、デバイスの存在と呼ばれますまたは*ファントム*デバイス。)。**DevCon FindAll**も操作では、BIOS の変更時、結果として異なる方法で列挙されているデバイスで検索します。 ローカルおよびリモート コンピューターで有効です。

```
    devcon [/m:\\computer] findall {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevconfindalltoolsspanspan-idddkdevconfindalltoolsspanparameters"></a><span id="ddk_devcon_findall_tools"></span><span id="DDK_DEVCON_FINDALL_TOOLS"></span>パラメーター


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **m:\\\\**<em>コンピューター</em>   
指定したリモート コンピューター上のコマンドを実行します。 円記号が必要です。

**注**DevCon コマンドをリモート コンピューターで実行する、グループ ポリシー設定がリモート コンピューターで実行するプラグ アンド プレイ サービスを許可する必要があります。 Windows Vista と Windows の以降のバージョンを実行しているコンピューターで、グループ ポリシーには、既定では、サービスへのリモート アクセスが無効にします。



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
<td align="left"><p><strong>'</strong></p>
<p>(一重引用符)</p></td>
<td align="left"><p>リテラル文字列と一致する (正確に表示される)。 示すアスタリスクは、ID 名の一部であるし、たとえば、ワイルドカード文字ではないは、単一引用符を含む文字列の前に<strong>' * PNP0600</strong>ここで、* PNP0600 ハードウェア ID (アスタリスクを含む) です。</p></td>
</tr>
</tbody>
</table>



<span id="________class______"></span><span id="________CLASS______"></span> **=**<em>クラス</em>デバイスのデバイス セットアップ クラスを指定します。 等号 (=) (**=**) クラスの名前として文字列を識別します。

ハードウェア Id、互換性 Id、デバイス インスタンス Id、または ID パターンを次のクラス名を指定することもできます。 各 ID またはパターンの間にスペースを入力します。 DevCon は、指定した Id に一致するクラス内のデバイスを検索します。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

**/M**パラメーターは、操作名を付ける必要があります (**findall**)。 それ以外の場合、DevCon は無視されます、 **/m**パラメーター構文エラーを返さずに、ローカル コンピューターを検索します。

コンピューターに現在接続されているデバイスのみを検索するには、使用、 [ **DevCon 検索**](devcon-find.md)操作。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon resources STORAGE\Volume
devcon resources =ports lpt*
devcon resources @pci*
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>例

[22 の使用例:検索 (および すべて検索) デバイス セットアップ クラス](devcon-examples.md#ddk_example_22_find_and_find_all_devices_in_a_setup_class_tools)









