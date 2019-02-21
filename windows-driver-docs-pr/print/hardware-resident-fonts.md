---
title: ハードウェアに常駐フォント
description: ハードウェアに常駐フォント
ms.assetid: 359735c2-bfa3-4c32-82a5-1d455c4eacb1
keywords:
- プリンターのフォントの記述 WDK Unidrv、ハードウェアに常駐フォント
- ハードウェアに常駐フォント WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c43bb2017697472d74065064bb9e57fbc258063
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560119"
---
# <a name="hardware-resident-fonts"></a>ハードウェアに常駐フォント





プリンターにハードウェア常駐フォントが含まれている場合は、.ufm または .ifi ファイル内でこれらのフォントのフォント メトリックの仕様を提供する必要があります。

別の .ufm または .ifi ファイルは、各ハードウェアのフォントを説明します。 これらのファイル Unidrv に使用できる、次の操作を行います。

-   プリンターのリソース DLL で .ufm ファイルを指定、RC を使用して\_UFM リソースを入力し、RC を使用して .ifi ファイルを指定\_フォント リソースの種類。

-   プリンターの GPD ファイルで使用して、 \*ResourceDLL 属性をリソース DLL の名前を指定します。

-   プリンターの GPD ファイルで使用、 \*RC に関連付けられているリソースの識別子を指定する DeviceFonts エントリ\_UFM または RC\_リソース DLL 内のエントリのフォント。

形式、 \*DeviceFonts エントリを次に示します。

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>* DeviceFonts:LIST (</strong><em>FontResourceID</em><strong>,</strong> <em>FontResourceID</em><strong>,</strong> ...<strong>)</strong></p></td>
</tr>
</tbody>
</table>

 

場所*FontResourceID* RC は、\_.ufm ファイル、または rc 版に関連付けられている UFM リソース識別子\_.ifi ファイルに関連付けられたフォント リソース識別子。

例を次に示します。

```cpp
*% Assume that RC_FONT_xxx ids are references to 
*% value macros defined by the GPD file creator.
*DeviceFonts: LIST(=RC_FONT_COURIER10, =RC_FONT_ARIALR,
+                  =RC_FONT_ARIALI, =RC_FONT_ARIALB, 
+                  =RC_FONT_ARIALBI, =RC_FONT_TIMESNRR,
+                  =RC_FONT_TIMESNRI, =RC_FONT_TIMESNRB,
+                  =RC_FONT_TIMESNRBI)
```

いくつかを含めることができます\*DeviceFonts エントリ[Unidrv ミニドライバー](unidrv-minidrivers.md)します。 GPD パーサーでは、複数のエントリを連結し、表示されているすべてのフォントをプリンターの機能のすべての構成できるようになります。 一部のフォントは、特定の構成で使用可能なのみを含めることができますを指定する必要がある場合\*内にある DeviceFonts エントリ[条件付きステートメント](conditional-statements.md)します。

 

 




