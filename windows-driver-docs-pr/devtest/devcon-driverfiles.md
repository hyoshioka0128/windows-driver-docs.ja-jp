---
title: DevCon DriverFiles
description: INF ファイルがインストールされていると、指定したデバイスのデバイス ドライバーのファイルの完全なパスとファイル名が表示されます。 ローカル コンピューターでのみ有効です。
ms.assetid: 8f8394e4-1ee4-4356-9f4d-ecc70deeaab1
keywords:
- DevCon DriverFiles ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon DriverFiles
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c76cac853ab620a9dfc10db8e3235c3ef79ca667
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348649"
---
# <a name="devcon-driverfiles"></a>DevCon DriverFiles


INF ファイルがインストールされていると、指定したデバイスのデバイス ドライバーのファイルの完全なパスとファイル名が表示されます。 ローカル コンピューターでのみ有効です。

```
    devcon driverfiles {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevcondriverfilestoolsspanspan-idddkdevcondriverfilestoolsspanparameters"></a><span id="ddk_devcon_driverfiles_tools"></span><span id="DDK_DEVCON_DRIVERFILES_TOOLS"></span>パラメーター


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
<td align="left"><p>任意の文字または文字と一致します。 ワイルドカード文字を使用して (<strong></em></strong>) パターンを作成する、ID、たとえば、 <strong><em>ディスク</em></strong>します。</p></td>
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

**DevCon DriverFiles**操作はローカル コンピューター上でのみ実行されます。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon driverfiles *
devcon driverfiles FDC\GENERIC_FLOPPY_DRIVE pci*
devcon driverfiles =media
devcon driverfiles =media isapnp*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 8:すべてのドライバー ファイルを一覧表示します。](devcon-examples.md#ddk_example_8_list_all_driver_files_tools)

[例 9:特定のデバイスのドライバー ファイルを一覧表示します。](devcon-examples.md#ddk_example_9_list_the_driver_files_of_a_particular_device_tools)









