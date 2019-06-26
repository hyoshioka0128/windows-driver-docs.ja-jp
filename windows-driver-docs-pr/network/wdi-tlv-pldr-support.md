---
title: WDI_TLV_PLDR_SUPPORT
description: WDI_TLV_PLDR_SUPPORT は、PLDR (プラットフォーム レベルのリセット) がサポートされているかどうかを指定する TLV です。
ms.assetid: BC1BE1A7-AA2D-4D11-A75A-EC0143343F33
ms.date: 07/18/2017
keywords:
- WDI_TLV_PLDR_SUPPORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 295ccd496becfbd8158c30071bb12c220351cf39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380740"
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

 

<a name="requirements"></a>必要条件
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


[PLDR](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-pldr-and-fldr)

 

 




