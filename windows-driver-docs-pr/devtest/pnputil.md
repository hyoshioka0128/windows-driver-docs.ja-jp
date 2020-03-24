---
title: PnPUtil
description: PnPUtil
ms.assetid: 3678fd41-c3ee-4538-b783-6f099ac104a6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9d3487b8b43407bd3050888960d9581ca4ce4c2
ms.sourcegitcommit: 4058fcb136cfb8255ca7bec68e8597c89f7b68cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/21/2020
ms.locfileid: "80080131"
---
# <a name="pnputil"></a>PnPUtil


PnPUtil (PnPUtil) は、管理者が[ドライバーパッケージ](https://docs.microsoft.com/windows-hardware/drivers/install/driver-packages)に対してアクションを実行できるようにするコマンドラインツールです。  たとえば、次のものがあります。

-   ドライバーパッケージを[ドライバーストア](https://docs.microsoft.com/windows-hardware/drivers/install/driver-store)に追加します。

-   コンピューターにドライバーパッケージをインストールします。

-   ドライバーストアからドライバーパッケージを削除します。

-   現在ドライバーストアにあるドライバーパッケージを列挙します。 インボックスパッケージ以外のドライバーパッケージのみが一覧表示されます。 *インボックス*ドライバーパッケージは、Windows またはそのサービスパックの既定のインストールに含まれています。

サポートされているすべてのアクションの一覧については、「 [PnP コマンド構文](https://review.docs.microsoft.com/en-us/windows-hardware/drivers/devtest/pnputil-command-syntax)」を参照してください。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PnPUtil はどこでダウンロードできますか。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>PnPUtil (PnPUtil) は、windows Vista (%windir%\system32 ディレクトリ内) 以降のすべてのバージョンの Windows に含まれています。 個別の PnPUtil ダウンロードパッケージがありません。</p>
<ul>
<li><strong>コマンドプロンプト</strong>ウィンドウを開きます ([<strong>管理者として実行</strong>])。</li>
<li>「 <strong>Pnputil/?」と入力します。</strong> コマンドオプションを表示します。 詳細については、「 <a href="pnputil-command-syntax.md" data-raw-source="[&lt;strong&gt;PnPUtil Command Syntax&lt;/strong&gt;](pnputil-command-syntax.md)"><strong>PnPUtil コマンドの構文</strong></a>」を参照してください。</li>
</ul>
<div class="alert">
<strong>メモ</strong> PnPUtil は、Windows Vista 以降のバージョンの Windows でサポートされています。 Windows XP では、PnPUtil は使用できませんが、<a href="https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines" data-raw-source="[Driver Install Frameworks (DIFx)](https://docs.microsoft.com/windows-hardware/drivers/install/difx-guidelines)">ドライバーインストールフレームワーク (DIFx)</a>ツールを使用して、ドライバーパッケージのインストールを作成およびカスタマイズすることができます。
</div>
<div>
 
</div></td>
</tr>
</tbody>
</table>

 

このセクションの内容は次のとおりです。

[PnPUtil コマンドの構文](pnputil-command-syntax.md)

[PnPUtil の例](pnputil-examples.md)

 

 





