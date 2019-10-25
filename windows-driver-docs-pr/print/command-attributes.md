---
title: コマンド属性
description: コマンド属性
ms.assetid: 8ce2c668-a130-428e-bf5f-0eab2dcd3fdb
keywords:
- プリンター属性 WDK Unidrv、コマンド
- コマンド WDK Unidrv
- プリンターコマンド WDK Unidrv、属性
- 発信者 id
- Cmd
- NoPageEject
- '[オーダー]'
- Params
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75e435cb80ca84e31c31866c9ffa308a09ea095f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842872"
---
# <a name="command-attributes"></a>コマンド属性





プリンターコマンドを指定するときは、属性を使用して、次の情報で Unidrv を提供します。

-   操作がプリンターハードウェアに実装されている場合に、ハードウェアが操作を実行するエスケープシーケンス。

-   操作が[レンダリングプラグイン](rendering-plug-ins.md)で実装されている場合に、 [**Iprintoemuni:: commandcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)メソッドに必要なコールバック識別子とパラメーター。

-   コマンドの送信順序。他のコマンドと比較して相対的に使用します。

次の表に、コマンドの属性をアルファベット順に示し、それらのパラメーターについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>の</strong></p></td>
<td><p>正の数値。レンダリングプラグインの<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)"><strong>Iprintoemuni:: CommandCallback</strong></a>メソッドに<em>Dcmdcbid</em>引数として渡されます。</p></td>
<td><p>動的に<a href="dynamically-generated-printer-commands.md" data-raw-source="[dynamically generated printer commands](dynamically-generated-printer-commands.md)">生成されたプリンターコマンド</a>に必要です。 <strong></em>Cmd</strong>が指定されている場合は無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>Cmd</strong></p></td>
<td><p><a href="command-string-format.md" data-raw-source="[command string format](command-string-format.md)">コマンド文字列形式</a>を使用して指定されたプリンターコマンドエスケープシーケンスを含むテキスト文字列。</p></td>
<td><p></em>の要求<strong>id</strong>が指定されていない場合は必須です。</p></td>
</tr>
<tr class="odd">
<td><p><em>NoPageEject を <strong>しますか?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>。コマンドを実行すると、プリンターによって現在の物理ページが取り出されるかどうかを示します。</p>
<p><strong></em>の順序</strong>で DOC_SETUP セクションが指定されていて、二重印刷が有効になっている場合にのみ使用されます。 ドキュメントページのページが途中で排出されないようにするために、Unidrv は、可能であれば、この属性が<strong>TRUE</strong>に設定されたコマンドのみを発行します。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は<strong>FALSE</strong>であり、コマンドによってページの取り出しが発生する可能性があります。</p>
<p>コマンドで副作用が発生する場合は、 <strong>true</strong>にはできません。これは、コマンドが<em>NoPageEject?</strong> <strong>TRUE</strong>に設定されている <strong>コマンドによって制御されるプリンター設定を変更する場合です。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>の順序</strong></p></td>
<td><p>「<a href="command-execution-order.md" data-raw-source="[Command Execution Order](command-execution-order.md)">コマンドの実行順序</a>」で説明されているように、セクション名と順序番号。</p></td>
<td><p>コマンドの説明に記載されていない限り、構成コマンドおよびカスタマイズされたオプションコマンドでのみ有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>Params</strong></p></td>
<td><p><em>PdwParams</em>引数として渡される EXTRAPARAM 構造体のレンダリングプラグインの IPrintOemUni:: commandcallback メソッドに渡される<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">標準変数</a>の<a href="lists.md" data-raw-source="[List](lists.md)">リスト</a>。</p></td>
<td><p><strong></em></strong>の場合にのみ有効です。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




