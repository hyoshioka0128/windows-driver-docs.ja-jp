---
title: バグチェック 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL バグチェックの値は0x000000D5 です。 これは、ドライバーが以前に解放されたメモリを参照したことを示します。
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
ms.openlocfilehash: d65d5fa367a6c562eaf83a3a8088d22a58a2dbd4
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534555"
---
# <a name="bug-check-0xd5-driver_page_fault_in_freed_special_pool"></a>バグチェック 0xD5: 解放された \_ \_ \_ \_ \_ 特殊な \_ プールでのドライバーページフォールト


解放された \_ 特殊なプールのバグチェックのドライバーページフォールトには、 \_ \_ \_ \_ \_ 0x000000D5 の値が含まれています。 これは、ドライバーが以前に解放されたメモリを参照したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_page_fault_in_freed_special_pool-parameters"></a>解放された \_ \_ \_ \_ \_ 特殊な \_ プールパラメーターのドライバーページエラー


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
エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE \_ 文字列) **KiBugCheckDriver**に格納されます。

<a name="cause"></a>原因
-----

ドライバーの検証ツールの**特別なプール**オプションによって、以前に解放されたメモリにアクセスするドライバーが検出されました。

特別なプールの詳細については、『 Windows Driver Kit 』の「Driver Verifier」セクションを参照してください。

<a name="remarks"></a>注釈
-------

これは、 **try-except**ハンドラーによって保護することはできません。プローブによってのみ保護できます。

 

 




