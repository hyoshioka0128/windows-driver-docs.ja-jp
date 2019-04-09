---
title: バグ チェック 0x8B MBR_CHECKSUM_MISMATCH
description: MBR_CHECKSUM_MISMATCH のバグ チェックでは、0x0000008B の値を持ちます。 このバグ チェックでは、MBR チェックサムの不一致が発生したことを示します。
ms.assetid: 7db57605-b6ff-49b9-8a79-3325512825b9
keywords:
- バグ チェック 0x8B MBR_CHECKSUM_MISMATCH
- MBR_CHECKSUM_MISMATCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MBR_CHECKSUM_MISMATCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5b0aa37b409a9a4212f94fe1fc117bbb73c5b991
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238451"
---
# <a name="bug-check-0x8b-mbrchecksummismatch"></a>バグ チェック 0x8B:MBR\_チェックサム\_が一致しません


MBR\_チェックサム\_の不一致のバグ チェックが 0x0000008B の値を持ちます。 このバグ チェックでは、MBR チェックサムの不一致が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="mbrchecksummismatch-parameters"></a>MBR\_チェックサム\_不一致パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>MBR からのディスク署名</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>OS ローダーを計算する MBR チェックサム</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>システムを計算する MBR チェックサム</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

MBR\_チェックサム\_Microsoft Windows オペレーティング システムを計算する MBR チェックサムがでローダーに合格するチェックサムと一致しない場合に、不一致のバグ チェックがブート プロセス中に発生します。

このエラーは、通常、ウイルスを示します。

<a name="resolution"></a>解決方法
----------

ウイルスの多くの形式があるし、すべてを検出できます。 通常、新しいウイルス通常検出できますがアップグレードされているウイルス検索プログラムによってのみ。 ウイルス検索プログラムを含む書き込み保護されているディスクを使用して起動し、感染をクリーンアップしようとしています。 必要があります。

 

 




