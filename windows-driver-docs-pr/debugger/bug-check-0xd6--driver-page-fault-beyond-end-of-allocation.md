---
title: バグチェック 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION バグチェックの値は0x000000D6 です。 これは、ドライバーがプール割り当ての最後を超えてメモリにアクセスしたことを示します。
ms.assetid: 939165dc-3052-4de7-88fd-25d4a7e82945
keywords:
- バグチェック 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c72e875365c5b04548a0c0baf3598a596581955
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313783"
---
# <a name="bug-check-0xd6-driver_page_fault_beyond_end_of_allocation"></a>バグチェック 0xD6: ドライバー\_ページ\_フォールト\_\_割り当ての\_終了\_を超えています


ドライバー\_ページ\_フォールト\_\_\_割り当てバグチェックの値が0x000000D6 になっています。\_ これは、ドライバーがプール割り当ての最後を超えてメモリにアクセスしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_page_fault_beyond_end_of_allocation-parameters"></a>ドライバー\_ページ\_フォールト\_\_割り当てパラメーターの\_エンド\_を超えています


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
<td align="left"><p>参照されたメモリアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0:</strong>込ん</p>
<p><strong>1:</strong>企画</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>参照されているメモリ (既知の場合) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

 
! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリに格納されます (PUNICODE\_STRING) *KiBugCheckDriver*。

<a name="cause"></a>原因
-----

ドライバーによって*n*バイトのメモリが割り当てられ、その後、 *n*バイトを超えて参照されました。 ドライバーの検証ツールの**特別なプール**オプションによって、この違反が検出されました。

特別なプールの詳細については、『 Windows Driver Kit 』の「Driver Verifier」セクションを参照してください。

<a name="remarks"></a>注釈
-------

これは、 **try-except**ハンドラーによって保護することはできません。プローブによってのみ保護できます。

 

 




