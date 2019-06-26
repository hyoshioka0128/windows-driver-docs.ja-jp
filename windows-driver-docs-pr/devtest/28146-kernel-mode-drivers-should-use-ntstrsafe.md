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
ms.openlocfilehash: e04b61871faa1a6735deb763297791311611e869
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364126"
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

 

カーネル モード ドライバーには、Ntstrsafe.h ではなく、Strsafe.h が含まれています。 Ntstrsafe.h と Strsafe.h については、次を参照してください。[安全な文字列関数を使用して](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-safe-string-functions)します。

 

 





