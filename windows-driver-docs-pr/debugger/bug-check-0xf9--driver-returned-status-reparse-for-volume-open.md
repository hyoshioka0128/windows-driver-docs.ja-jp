---
title: バグチェック 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN bug check は、ドライバーが末尾の名前のない IRP_MJ_CREATE 要求に STATUS_REPARSE を返したことを示します。
ms.assetid: 60eeb24a-accf-4db8-ba5b-1738a9aa4b46
keywords:
- バグチェック 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3013fc6e6e65b69b86dce54c974690f38ef8bb6
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038097"
---
# <a name="bug-check-0xf9-driver_returned_status_reparse_for_volume_open"></a>バグ チェック 0xF9:DRIVER @ NO__T から返された @ NO__T-1STATUS @ NO__T-2REPARSE 解析 @ NO__T-3FOR NO__T-4VOLUME @ NO__T-5OPEN


ドライバー @ no__t から返された @ no__t-1STATUS @ no__t-2REPARSE 解析 @ no__t-3FOR no__t を @ no__t のバグチェックの値を0x000000F9 です。 これは、ドライバーが、末尾に名前のない IRP @ no__t-1MJ @ no__t-2CREATE 要求に対して状態 @ no__t-0REPARSE 返したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_returned_status_reparse_for_volume_open-parameters"></a>DRIVER @ no__t から返された @ no__t-1STATUS @ no__t-2REPARSE 解析 @ no__t-3FOR no__t の @ no__t-4VOLUME @-5OPEN Parameters


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
<td align="left"><p>開かれたデバイスオブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRP_MJ_CREATE 要求が発行されたデバイスオブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>(再解析する) ファイルの新しい名前を含む Unicode 文字列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>IRP_MJ_CREATE 要求のドライバーによって返される情報</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
STATUS @ no__t-0REPARSE は、ドライバーが名前空間をサポートしていることを示すため、末尾の名前を持つ IRP @ no__t-1MJ @ no__t-2CREATE 要求に対してのみ返される必要があります。

 

 




