---
title: バグチェック 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: ドライバーが末尾の名前のない IRP_MJ_CREATE 要求に STATUS_REPARSE を返したことを示す DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN バグチェック。
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
# <a name="bug-check-0xf9-driver_returned_status_reparse_for_volume_open"></a>バグチェック 0xF9:\_ボリューム\_開くための再解析\_の状態\_\_返されたドライバー\_


ドライバー\_、\_ボリューム\_開いているバグチェックの状態\_再解析\_\_返されます。 これは、ドライバーが IRP\_MJ\_CREATE 要求に対して、末尾に名前のない状態\_再解析を返したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_returned_status_reparse_for_volume_open-parameters"></a>\_ボリューム\_開いているパラメーターの状態\_再解析\_\_\_ドライバーが返されました


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

 

<a name="remarks"></a>注釈
-------

! [デバッグ拡張機能の[**分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
ドライバーが名前空間をサポートしていることを示すため、IRP\_\_MJ の場合にのみ、ステータス\_再解析が返され、末尾に名前の付いた要求が作成されます。

 

 




