---
title: コマンド属性
description: コマンド属性
ms.assetid: 8ce2c668-a130-428e-bf5f-0eab2dcd3fdb
keywords:
- プリンターは、WDK Unidrv、コマンドを属性します。
- WDK Unidrv コマンド
- プリンターが WDK Unidrv、属性をコマンドします。
- CallbackID
- Cmd
- NoPageEject
- '[オーダー]'
- params
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bff0efceae5936f6a41ba19ffd2c233be0795fcc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382618"
---
# <a name="command-attributes"></a>コマンド属性





プリンター コマンドを指定するときに属性を使用して Unidrv を次の情報を提供します。

-   プリンターのハードウェアで、操作が実装されている場合、操作を実行するためのハードウェアを原因となるエスケープ シーケンスです。

-   コールバック識別子として必要なパラメーター、 [ **IPrintOemUni::CommandCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff554216)メソッドで、操作が実装されている場合、[プラグインでレンダリング](rendering-plug-ins.md)します。

-   コマンドを送信する、他のコマンドに対して相対的順序。

次の表では、アルファベット順にコマンドの属性の一覧し、そのパラメーターについて説明します。

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
<td><p><strong><em>CallbackID</strong></p></td>
<td><p>正の数値があり、レンダリング プラグインでは、に渡される<a href="https://msdn.microsoft.com/library/windows/hardware/ff554216" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554216)"> <strong>IPrintOemUni::CommandCallback</strong> </a>メソッドとしてその<em>dCmdCbID</em>引数。</p></td>
<td><p>必要な<a href="dynamically-generated-printer-commands.md" data-raw-source="[dynamically generated printer commands](dynamically-generated-printer-commands.md)">プリンター コマンドを動的に生成される</a>します。 有効でない場合 <strong></em>Cmd</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>cmd</strong></p></td>
<td><p>使用して指定された、プリンター コマンドのエスケープ シーケンスを含むテキスト文字列、<a href="command-string-format.md" data-raw-source="[command string format](command-string-format.md)">コマンド文字列の形式</a>します。</p></td>
<td><p>しない限り、必要な <strong></em>CallbackID</strong>を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>NoPageEject?</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示す、プリンターを現在の物理ページを取り出すと、コマンドを実行するかどうか。</p>
<p>使用されている場合にのみ<strong></em>順序</strong>DOC_SETUP セクションを指定します、両面印刷が有効になっている場合。 二重のドキュメントのページ間での早期ページ取り出しを避けるためには、Unidrv のみを発行コマンドでは、この属性を設定する<strong>TRUE</strong>、可能な場合。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>、意味のコマンドは、ページの取り出しが発生する可能性があります。</p>
<p>必要があります<strong>TRUE</strong>コマンドは、副作用を引き起こす場合 (外でのコマンドによって制御されているプリンターの設定を変更する場合に、 <strong> <em>NoPageEject?</strong>に設定<strong>TRUE</strong>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>順序</strong></p></td>
<td><p>」の説明に従って、名前と注文番号をセクション<a href="command-execution-order.md" data-raw-source="[Command Execution Order](command-execution-order.md)">コマンドの実行順序</a>します。</p></td>
<td><p>構成コマンドとカスタマイズされたオプションのコマンドでのみ有効ですコマンドの説明に記載されている場合を除き、します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>params</strong></p></td>
<td><p><a href="lists.md" data-raw-source="[List](lists.md)">リスト</a>の<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">標準変数</a>として渡される EXTRAPARAM 構造で、レンダリング プラグインの IPrintOemUni::CommandCallback メソッドに渡されるその<em>pdwParams</em>引数。</p></td>
<td><p>有効な場合にのみ <strong></em>CallbackID</strong>も指定します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




