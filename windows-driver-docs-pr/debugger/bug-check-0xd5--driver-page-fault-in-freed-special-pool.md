---
title: バグチェック 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL のバグチェックの値は0x000000D5 です。 これは、ドライバーが以前に解放されたメモリを参照したことを示します。
ms.assetid: b86e55d2-122f-40ac-adb3-092511d3274e
keywords:
- バグチェック 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0f882b4e91ac32d838428b8a81a0fe7d5ada730
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313785"
---
# <a name="bug-check-0xd5-driver_page_fault_in_freed_special_pool"></a>バグ チェック 0xD5:DRIVER @ NO__T-0PAGE @ NO__T-1FAULT @ NO__T IN @ NO__T-3FREED @ NO__T-4SPECIAL @ NO__T-5POOL


DRIVER @ no__t-0PAGE @ no__t-1FAULT @ no__t IN @ no__t-3FREED @ no__t-4SPECIAL @ no__t-5POOL bug check の値は0x000000D5 です。 これは、ドライバーが以前に解放されたメモリを参照したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_page_fault_in_freed_special_pool-parameters"></a>DRIVER @ no__t-0PAGE @ no__t-1FAULT @ no__t IN @ no__t-3FREED @ no__t-4SPECIAL @ no__t-5POOL Parameters


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
<td align="left"><p><strong>0</strong>読み取り</p>
<p><strong>1:</strong>書き込み</p></td>
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
エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE @ no__t-0STRING) **KiBugCheckDriver**に格納されます。

<a name="cause"></a>原因
-----

ドライバーの検証ツールの**特別なプール**オプションによって、以前に解放されたメモリにアクセスするドライバーが検出されました。

特別なプールの詳細については、『 Windows Driver Kit 』の「Driver Verifier」セクションを参照してください。

<a name="remarks"></a>コメント
-------

これは、 **try-except**ハンドラーによって保護することはできません。プローブによってのみ保護できます。

 

 




