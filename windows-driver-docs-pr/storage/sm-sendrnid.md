---
title: SM\_SendRNID 関数
description: SM\_SendRNID WMI メソッドは、要求ノード識別データ (RNID) コマンドを指定されたポートに送信します。
ms.assetid: 160e2dc7-8195-4f8a-bc59-854e5283cf6f
keywords:
- SM_SendRNID 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SendRNID
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e29155b70dce368e9306dc33cf8c69773d1723d9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845458"
---
# <a name="sm_sendrnid-function"></a>SM\_SendRNID 関数


SM\_SendRNID WMI メソッドは、要求ノード識別データ (RNID) コマンドを指定されたポートに送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendRNID(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              DestWWN[8],
   [in] uint32                                 DestFCID,
   [in] uint32                                 NodeIdDataFormat,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                ResponseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
RNID コマンドの送信に使用されるローカルポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendRNID\_の PortWWN メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendRNID\_の DestWWN メンバーのミニポートドライバーに配信されます。

*DestFCID*   
宛先ポートのアドレス識別子。 この情報は、構造内の SM\_SendRNID\_の DestFCID メンバーのミニポートドライバーに配信されます。

*NodeIdDataFormat*   
ノード識別データ形式。 このメンバーが持つことができる値の詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、構造内の SM\_SendRNID\_の NodeIdDataFormat メンバーのミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_SendRNID\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

*Total火炎 buffersize*   
RNID コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendRNID\_OUT 構造体の TotalRspBufferSize メンバーにこの情報を返します。

*Responsebuffersize*   
RNID コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendRNID\_OUT 構造体の ResponseBufferSize メンバーにこの情報を返します。

*Responsebuffer*   
RNID コマンドの結果。 ミニポートドライバーは、SM\_SendRNID\_OUT 構造体の ResponseBuffer メンバーにこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、MS\_SM\_FabricAndDomainManagementMethods WMI クラスに属しています。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SM\_SendRNID\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_in)

[**SM\_SendRNID\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrnid_out)

 

 






