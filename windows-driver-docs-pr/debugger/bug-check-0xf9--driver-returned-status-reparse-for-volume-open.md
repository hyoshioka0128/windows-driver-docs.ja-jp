---
title: バグチェック 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: ドライバーが末尾の名前のない IRP_MJ_CREATE 要求に STATUS_REPARSE を返したことを示す DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN バグチェック。
ms.assetid: 60eeb24a-accf-4db8-ba5b-1738a9aa4b46
keywords:
- バグチェック 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 07/21/2020
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c1f9ee94e7f764d71c4c62f3e378ca7e87e7a522
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402309"
---
# <a name="bug-check-0xf9-driver_returned_status_reparse_for_volume_open"></a>バグチェック 0xF9: ドライバー \_ が \_ \_ \_ \_ オープンボリュームの状態の再解析を返しました \_

ドライバーは \_ 、 \_ \_ \_ ボリュームオープンバグチェックのステータスの再解析に \_ \_ 0x000000f9 の値を返しました。 これは、ドライバーが \_ \_ \_ 名前の末尾がない IRP MJ CREATE 要求へのステータスの再解析を返したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_returned_status_reparse_for_volume_open-parameters"></a>\_ \_ \_ \_ \_ ボリュームオープンパラメーターの状態の再解析がドライバーによって返されました \_

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

## <a name="remarks"></a>解説

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

ステータスの \_ 再解析は \_ \_ 、ドライバーが名前空間をサポートしていることを示すため、末尾の名前を持つ IRP MJ CREATE 要求に対してのみ返される必要があります。 

ファイルシステムドライバーの使用方法の詳細については、「 [file systems driver design guide](https://docs.microsoft.com/windows-hardware/drivers/ifs/)」を参照してください。 IRP MJ CREATE 要求の詳細については、 \_ \_ 「 [IRP_MJ_CREATE (IFS)](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)」を参照してください。
