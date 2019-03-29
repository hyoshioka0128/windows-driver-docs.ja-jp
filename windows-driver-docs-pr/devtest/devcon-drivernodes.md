---
title: DevCon DriverNodes
description: 順位付け、バージョンと共に、デバイスと互換性があるすべてのドライバー パッケージを一覧表示します。 ローカル コンピューターでのみ有効です。
ms.assetid: 891aa022-44f5-4920-ab57-a0573deb94de
keywords:
- DevCon DriverNodes ドライバーの開発ツール
topic_type:
- apiref
api_name:
- DevCon DriverNodes
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53e8c9e4ee674b9d2965e3348d159d2b5710842c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350081"
---
# <a name="devcon-drivernodes"></a>DevCon DriverNodes


すべてを一覧表示[ドライバー パッケージ](https://msdn.microsoft.com/library/windows/hardware/ff539954)と共に順位付け、バージョン、デバイスと互換性のあります。 ローカル コンピューターでのみ有効です。

```
    devcon drivernodes {* | ID [ID ...] | =class [ID [ID ...]]} 
```

## <a name="span-idddkdevcondrivernodestoolsspanspan-idddkdevcondrivernodestoolsspanparameters"></a><span id="ddk_devcon_drivernodes_tools"></span><span id="DDK_DEVCON_DRIVERNODES_TOOLS"></span>パラメーター


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

**DevCon DriverNodes**操作はローカル コンピューター上でのみ実行されます。

**DevCon DriverNodes**操作はセットアップの問題のトラブルシューティングに特に便利です。 たとえば、Windows INF ファイル、またはカスタマイズされたサード パーティ製 INF ファイルをデバイスで使用されたかどうかを特定するのには使用できます。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>サンプルの使用法

```
devcon drivernodes *
devcon drivernodes *miniport*
devcon drivernodes =usb pci* usb*
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

[例 10:ハードウェア ID のパターンでドライバー パッケージの一覧](devcon-examples.md#ddk_example_10_list_driver_packages_by_hardware_id_pattern_tools)

[例 11:デバイス インスタンス ID のパターンでドライバー パッケージの一覧](devcon-examples.md#ddk_example_11_list_driver_packages_by_device_instance_id_pattern_tool)









