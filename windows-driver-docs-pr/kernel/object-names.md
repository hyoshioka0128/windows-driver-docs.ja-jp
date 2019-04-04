---
title: オブジェクト名
description: オブジェクト名
ms.assetid: b30e7475-7f94-4993-b373-8e4a8b1bcb4c
keywords:
- オブジェクト名の WDK カーネル
- 名前付きオブジェクトの WDK カーネル
- WDK カーネルの名前のないオブジェクト
- WDK のユーザー モードのオブジェクト名
- オブジェクトは、WDK のユーザー モードを処理します。
- オブジェクト ハンドル WDK カーネル
- WDK のユーザー モードを処理します。
- ハンドルの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd7fdf24eb420f670fe5234fc8e5a17d985ff7af
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552118"
---
# <a name="object-names"></a>オブジェクト名





カーネル モードのオブジェクトは、という名前か、または名前のないです。 *オブジェクト名*Unicode 文字列で、オブジェクトを参照するユーザー モードとカーネル モードの両方のコンポーネントを使用できます。 たとえば、  **\\KernelObjects\\LowMemoryCondition**システムの空きメモリの量が少ないときに通知する標準的なイベント オブジェクトの名前を指定します。

ユーザー モードとカーネル モードの両方のコンポーネントでは、オブジェクト名を使用して、オブジェクトへのハンドルを開きます。 ハンドルを使用して、後続のすべての操作が実行されます。

オブジェクトが名前付きでない場合、ユーザー モード コンポーネントは、それを識別するハンドルを開くことができません。 カーネル モード コンポーネントは、名前のないオブジェクトへのポインターまたはハンドルのいずれかによって参照できます。

名前付きオブジェクトは、階層に編成されます。 各オブジェクトの名前は、親オブジェクトに対して相対的です。 オブジェクトの名前の各コンポーネントは、円記号で始まります。 たとえば、  **\\KernelObjects**の親である **\\KernelObjects\\LowMemoryCondition**します。

いくつかの種類のオブジェクトのみでは、子オブジェクトを持つことができます。 例を次に示します。

-   オブジェクトのディレクトリでは、子オブジェクトがあります。 オブジェクト マネージャーでは、オブジェクトのディレクトリを使用して、オブジェクトを整理します。 たとえば **\\KernelObjects**は標準的なイベント オブジェクトを保持するオブジェクトのディレクトリです。 オブジェクトのディレクトリは、ディスク上の実際のディレクトリに対応していません。 詳細については、[オブジェクト ディレクトリ](object-directories.md)を参照してください。

-   ディスク ドライブのデバイス オブジェクトでは、ディスク上のファイルに対応する子オブジェクトがあります。

-   ディレクトリを表すファイル オブジェクトには、ディレクトリ内のファイルに対応する子オブジェクトがあります。

-   WDM ドライバーのデバイス オブジェクトは、ドライバーの定義済みの方法で使用できる、独自の名前空間を持ちます。 詳細については、[デバイス Namespace のアクセスを制御する](controlling-device-namespace-access.md)を参照してください。

ファイルの基準とするオブジェクト名がある **\\\dosdevices\z**します。 ファイル c: たとえば、\\ディレクトリ\\として指定できるファイル **\\\dosdevices\z\\c:\\**<em>ディレクトリ\\ファイル</em>.

たとえば、次のように、オブジェクト名のコンポーネントを記述できます。

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
<td><p>オブジェクトのディレクトリ。</p></td>
</tr>
<tr class="even">
<td><p><strong>\DosDevices\C:</strong></p></td>
<td><p>C: ドライブを表すデバイス オブジェクト。</p></td>
</tr>
<tr class="odd">
<td><p><strong>\DosDevices\C:&lt;/strong&gt; <em>Directory</em></p></td>
<td><p>ファイルの C:\Directory という名前のディレクトリを表すオブジェクト。</p></td>
</tr>
<tr class="even">
<td><p><strong>\DosDevices\C:&lt;/strong&gt; <em>Directory</em> \ <em>File</em></p></td>
<td><p>ファイルの C:\Directory\File という名前のファイルを表すオブジェクト。</p></td>
</tr>
</tbody>
</table>

 

名前付きのオブジェクトを作成するドライバーは、特定のオブジェクトのディレクトリで行います。 詳細については、[オブジェクト ディレクトリ](object-directories.md)を参照してください。

 

 




