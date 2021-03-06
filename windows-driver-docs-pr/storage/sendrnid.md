---
title: SendRNID 関数
description: SendRNID WMI メソッドは、指定されたポートに要求ノードの id データ (RNID) コマンドを送信します。
ms.assetid: 70c9655c-aaa8-45bb-ae5b-7428d9cdd4b2
keywords:
- 記憶装置の SendRNID 関数
topic_type:
- apiref
api_name:
- SendRNID
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 99607a6cfd6c477035f0a11a224d7c03dbf2a9e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362664"
---
# <a name="sendrnid-function"></a>SendRNID 関数


**SendRNID** WMI メソッドは、指定されたポートに要求ノードの id データ (RNID) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendRNID(
   [in, HBAType("HBA_WWN")] uint8                                                          wwn[8],
   [in, HBAType("HBA_WWNTYPE"), Values{"NODE_WWN", "PORT_WWN"}, ValueMap{"0", "1"}] uint32 wwntype,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS                                                 HBAStatus,
   [out] uint32                                                                            ResponseBufferCount,
   [out, WmiSizeIs("ResponseBufferCount")] uint8                                           ResponseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*wwn*   
RNID コマンドを送信するポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **wwn**のメンバー、 [ **SendRNID\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_in)構造体。

*wwntype*   
使用しないでください。 使わないでください。

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendRNID\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体。

*ResponseBufferCount*   
RNID コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ResponseBufferCount**のメンバー、 [ **SendRNID\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体。

*ResponseBuffer*   
RNID コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **ResponseBuffer**のメンバー、 [ **SendRNID\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SendRNID\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_in)

[**SendRNID\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sendrnid_out)

 

 






