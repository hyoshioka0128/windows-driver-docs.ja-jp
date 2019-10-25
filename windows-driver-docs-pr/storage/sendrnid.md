---
title: SendRNID 関数
description: SendRNID WMI メソッドは、要求ノード識別データ (RNID) コマンドを指定されたポートに送信します。
ms.assetid: 70c9655c-aaa8-45bb-ae5b-7428d9cdd4b2
keywords:
- SendRNID 関数ストレージデバイス
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
ms.openlocfilehash: 66c40c17c69aec66691cbbcd068c0cc02f28089b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832037"
---
# <a name="sendrnid-function"></a>SendRNID 関数


**Sendrnid** WMI メソッドは、要求ノード識別データ (rnid) コマンドを指定されたポートに送信します。

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
RNID コマンドが送信されるポートの世界規模の名前。 この情報は、構造[**内の Sendrnid\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_in)の**wwn**メンバーのミニポートドライバーに配信されます。

*wwntype*   
使用しないでください。 使わないでください。

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendrnid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体の**hbastatus**メンバーにこの情報を返します。

*ResponseBufferCount*   
RNID コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrnid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体の**ResponseBufferCount**メンバーにこの情報を返します。

*Responsebuffer*   
RNID コマンドの結果。 ミニポートドライバーは、 [**Sendrnid\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)構造体の**responsebuffer**メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**の SendRNID\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_in)

[**SendRNID\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnid_out)

 

 






