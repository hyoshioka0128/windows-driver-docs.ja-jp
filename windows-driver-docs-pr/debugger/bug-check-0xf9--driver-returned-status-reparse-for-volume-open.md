---
title: Bug Check 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: ドライバーがない末尾名な irp_mj_create 用要求 status_reparse を不確実を返すことを示す DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN バグ チェックします。
ms.assetid: 60eeb24a-accf-4db8-ba5b-1738a9aa4b46
keywords:
- Bug Check 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3b6063b1e6bfdc2596eab0648631761f08cbf14b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367302"
---
# <a name="bug-check-0xf9-driverreturnedstatusreparseforvolumeopen"></a>バグ チェック 0xF9:ドライバー\_から返された\_状態\_再解析\_の\_ボリューム\_開く


ドライバー\_から返された\_状態\_再解析\_の\_ボリューム\_バグを開くチェックが 0x000000F9 の値を持ちます。 これは、ドライバーが状態を返すことを示します\_IRP を再解析\_MJ\_ない末尾の名前を持つ要求の作成。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="driverreturnedstatusreparseforvolumeopen-parameters"></a>ドライバー\_から返された\_状態\_再解析\_の\_ボリューム\_パラメーターを開く


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
<td align="left"><p>開かれたデバイス オブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>Irp_mj_create 用要求の発行先のデバイス オブジェクト</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>(再解析され) するファイルの新しい名前を含む Unicode 文字列のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>Irp_mj_create 用要求用のドライバーによって返される情報</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

ステータス\_IRP ののみ、再解析を返す必要がある\_MJ\_作成要求の末尾に、ドライバーを示す、名、名前空間はサポートしています。

 

 




