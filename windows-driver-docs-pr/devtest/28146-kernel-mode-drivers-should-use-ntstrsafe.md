---
title: C28146
description: '警告: C28146 カーネル モード ドライバー ntstrsafe.h、strsafe.h ではないを使用する必要があります。 ソース ファイルで見つかりました。'
ms.assetid: 00e3e96e-b31b-4060-8193-d69b7cca8181
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28146
ms.openlocfilehash: 4821f4657117e0ed28071d24a72b80fabf02bbfc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558262"
---
# <a name="c28146"></a>C28146


C28146 を警告します。カーネル モード ドライバーでは、strsafe.h ではない、ntstrsafe.h を使用してください。 ソース ファイルで見つかりました

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>追加情報</strong></p></td>
<td align="left"><p>ヘッダー ntstrsafe.h には、カーネル モード コードでの使用に適している strsafe.h で見つかった関数のバージョンが含まれています。</p></td>
</tr>
</tbody>
</table>

 

カーネル モード ドライバーには、Ntstrsafe.h ではなく、Strsafe.h が含まれています。 Ntstrsafe.h と Strsafe.h については、次を参照してください。[安全な文字列関数を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565508)します。

 

 





