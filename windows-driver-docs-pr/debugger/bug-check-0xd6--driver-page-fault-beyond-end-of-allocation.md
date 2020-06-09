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
ms.openlocfilehash: 8bfbafc51b94911362b94d67ff81956ffe6d5b89
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534551"
---
# <a name="bug-check-0xd6-driver_page_fault_beyond_end_of_allocation"></a>バグチェック 0xD6: \_ \_ \_ \_ \_ 割り当ての終了を超えた \_ ドライバーページフォールト


\_ \_ \_ \_ 割り当てバグチェックの終了後のドライバーページフォールトには、 \_ \_ 0x000000D6 の値が含まれています。 これは、ドライバーがプール割り当ての最後を超えてメモリにアクセスしたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_page_fault_beyond_end_of_allocation-parameters"></a>\_ \_ \_ \_ \_ 割り当てパラメーターの末尾を超えたドライバーページのエラー \_


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

 
! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE \_ 文字列) *KiBugCheckDriver*に格納されます。

<a name="cause"></a>原因
-----

ドライバーによって*n*バイトのメモリが割り当てられ、その後、 *n*バイトを超えて参照されました。 ドライバーの検証ツールの**特別なプール**オプションによって、この違反が検出されました。

特別なプールの詳細については、『 Windows Driver Kit 』の「Driver Verifier」セクションを参照してください。

<a name="remarks"></a>注釈
-------

これは、 **try-except**ハンドラーによって保護することはできません。プローブによってのみ保護できます。

 

 




