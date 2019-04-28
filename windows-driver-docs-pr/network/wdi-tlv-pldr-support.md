---
title: WDI_TLV_PLDR_SUPPORT
description: WDI_TLV_PLDR_SUPPORT は、PLDR (プラットフォーム レベルのリセット) がサポートされているかどうかを指定する TLV です。
ms.assetid: BC1BE1A7-AA2D-4D11-A75A-EC0143343F33
ms.date: 07/18/2017
keywords:
- WDI_TLV_PLDR_SUPPORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 3339b7a4555f1a288ba0f28be901899eb130a60d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380020"
---
# <a name="wditlvpldrsupport"></a>WDI\_TLV\_PLDR\_サポート


WDI\_TLV\_PLDR\_サポートは、TLV PLDR (プラットフォーム レベルのリセット) がサポートされているかどうかを指定します。

**注**  この TLV は、Windows 10 バージョン 1511、WDI バージョン 1.0.10 で追加されました。

 

## <a name="tlv-type"></a>TLV 型


0x11A

## <a name="length"></a>長さ


UINT8 のサイズをバイト単位で。

## <a name="values"></a>値


| 型  | 説明                                                                                                                                                                                                                       |
|-------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | PLDR がサポートされているかどうかを指定します。 この値は、デバイスまたはバスでサポートされない場合のリセット機能 (通常は、ACPI または PCI メソッドのクエリを実行するには) を 0 に設定されます。 0 以外の値は、リセット機能がサポートされていることを指定します。 |

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[PLDR](https://msdn.microsoft.com/library/windows/hardware/mt269098)

 

 




