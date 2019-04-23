---
title: バグ チェック 0xC5 DRIVER_CORRUPTED_EXPOOL
description: DRIVER_CORRUPTED_EXPOOL のバグ チェックでは、0x000000C5 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL で無効なメモリへのアクセスを試行したことを示します。
ms.assetid: e375e7d3-9cb1-474f-ade2-1bc65dd79864
keywords:
- バグ チェック 0xC5 DRIVER_CORRUPTED_EXPOOL
- DRIVER_CORRUPTED_EXPOOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CORRUPTED_EXPOOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d10e36b99287a788b2e97c383201919b40a120cd
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902636"
---
# <a name="bug-check-0xc5-drivercorruptedexpool"></a>バグ チェック 0xC5:ドライバー\_破損した\_EXPOOL


ドライバー\_破損した\_EXPOOL バグ チェックが 0x000000C5 の値を持ちます。 これは、システムがプロセスが高すぎる IRQL で無効なメモリへのアクセスを試行したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="drivercorruptedexpool-parameters"></a>ドライバー\_破損した\_EXPOOL パラメーター


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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時に</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

ページング可能なメモリ (または、完全に無効なメモリ) にアクセスしようとする、カーネルの IRQL が高すぎる場合にします。 この問題の究極的な原因は、ほぼ間違いなく、システム プールが破損しているドライバーです。

ほとんどの場合、このバグ チェックの結果、ドライバーが小規模の割り当てが破損している場合 (ページよりも小さい\_サイズ)。 大規模な割り当てが発生する[**バグ チェック 0xD0** ](bug-check-0xd0--driver-corrupted-mmpool.md) (ドライバー\_破損した\_MMPOOL)。

<a name="resolution"></a>解決方法
----------

最近、新しいソフトウェアをインストールした場合が正しくインストールされてかどうかを確認します。 製造元の web サイトで更新されたドライバーを確認します。

このエラーをデバッグするには、Driver Verifier の特別なプールのオプションを使用します。 エラーが発生したドライバーを明らかにこれが失敗した場合は、グローバル フラグ ユーティリティを使用して、特別なプールでプール タグを有効にします。

特別なプールについては、Windows ドライバー キットの Driver Verifier のセクションを参照してください。

 

 




