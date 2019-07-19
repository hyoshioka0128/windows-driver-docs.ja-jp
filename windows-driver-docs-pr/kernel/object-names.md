---
title: オブジェクト名
description: オブジェクト名
ms.assetid: b30e7475-7f94-4993-b373-8e4a8b1bcb4c
keywords:
- オブジェクト名 WDK カーネル
- 名前付きオブジェクト WDK カーネル
- 名前のないオブジェクト WDK カーネル
- オブジェクト名 WDK ユーザーモード
- オブジェクトが WDK ユーザーモードを処理する
- オブジェクトは WDK カーネルを処理します
- WDK ユーザーモードを処理する
- WDK カーネルを処理します
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: adbe7e202a2ae1808e6164572312658392fbd5ba
ms.sourcegitcommit: b9a65cb309bea3d35048968bdc708e0067276e68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68313210"
---
# <a name="object-names"></a>オブジェクト名





カーネルモードオブジェクトには名前が付けられているか、名前が付いていません。 *オブジェクト名*は、ユーザーモードとカーネルモードの両方のコンポーネントがオブジェクトを参照するために使用できる Unicode 文字列です。 たとえば、  **\\KernelObjects\\lowmemorycondition**は、システム内の空きメモリ容量が不足したときに通知する標準イベントオブジェクトの名前です。

ユーザーモードとカーネルモードの両方のコンポーネントは、オブジェクト名を使用してオブジェクトへのハンドルを開きます。 後続のすべての操作は、ハンドルを使用して実行されます。

オブジェクトに名前が付いていない場合、ユーザーモードコンポーネントはそのオブジェクトへのハンドルを開くことができません。 カーネルモードのコンポーネントは、ポインターまたはハンドルのいずれかによって名前のないオブジェクトを参照できます。

名前付きオブジェクトは、階層に編成されます。 各オブジェクトは、親オブジェクトに対して相対的な名前が付けられます。 オブジェクトの名前の各コンポーネントは、円記号で始まります。 たとえば、  **\\KernelObjects**は **\\KernelObjects\\lowmemorycondition**の親オブジェクトです。

子オブジェクトを持つことができるのは、一部の種類のオブジェクトだけです。 次に例をいくつか示します。

-   オブジェクトディレクトリには子オブジェクトがあります。 オブジェクトマネージャーは、オブジェクトディレクトリを使用してオブジェクトを整理します。 たとえば、KernelObjects は、標準のイベントオブジェクトを保持するオブジェクトディレクトリです。  **\\** オブジェクトディレクトリは、ディスク上の実際のディレクトリには対応していません。 詳細については、「[オブジェクトディレクトリ](object-directories.md)」を参照してください。

-   ディスクドライブのデバイスオブジェクトには、ディスク上のファイルに対応する子オブジェクトがあります。

-   ディレクトリを表すファイルオブジェクトには、ディレクトリ内のファイルに対応する子オブジェクトがあります。

-   WDM ドライバーのデバイスオブジェクトには、ドライバー定義の方法で使用できる独自の名前空間があります。 詳細については、「[デバイスの名前空間へのアクセスの制御](controlling-device-namespace-access.md)」を参照してください。

ファイルには、  **\\dosdevices**を基準としたオブジェクト名があります。 たとえば\\、ファイル c: ディレクトリ\\ファイルは、  **\\dosdevices\\c:\\** <em>directory\\ファイル</em>として指定できます。

たとえば、オブジェクト名のコンポーネントは、次のように記述できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>オブジェクト名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>\DosDevices</strong></p></td>
<td><p>オブジェクトディレクトリ。</p></td>
</tr>
<tr class="even">
<td><p><strong>\DosDevices\C:</strong></p></td>
<td><p>C: ドライブを表すデバイスオブジェクト。</p></td>
</tr>
<tr class="odd">
<td><p>\ <strong>Dosdevic/C: \</strong><em>ディレクトリ</em></p></td>
<td><p>C:\ directoryという名前のディレクトリを表すファイルオブジェクト。</p></td>
</tr>
<tr class="even">
 <td><p>\ <strong>Dosdevic/C: \</strong><em>ディレクトリ</em>\<em>ファイル</em></p></td>
<td><p>C:\Directory\File. という名前のファイルを表すファイルオブジェクト</p></td>
</tr>
</tbody>
</table>

 

名前付きオブジェクトを作成するドライバーは、特定のオブジェクトディレクトリで実行されます。 詳細については、「[オブジェクトディレクトリ](object-directories.md)」を参照してください。

 

 




