---
title: SM\_SendCTPassThru 関数
description: SM\_SendCTPassThru WMI メソッドは、指定されたポートに common transport (CT) パススルーコマンドを送信します。
ms.assetid: 437f0c79-78f6-406e-8774-79de4425bfe8
keywords:
- SM_SendCTPassThru 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SendCTPassThru
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2d33f65e26d17829f2e018bc8fbcecbe757898e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845463"
---
# <a name="sm_sendctpassthru-function"></a>SM\_SendCTPassThru 関数


SM\_SendCTPassThru WMI メソッドは、指定されたポートに common transport (CT) パススルーコマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendCTPassThru(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in] uint32                                 InRespBufferMaxSize,
   [in] uint32                                 RequestBufferSize,
   [in, WmiSizeIs("RequestBufferSize")] uint8  RequestBuffer,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalResponseBufferSize,
   [out] uint32                                ActualResponseBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
ターゲットへのアクセスに使用される HBA のワールド名 (WWN)。 この情報は、PortWWN の SendCTPassThru\_のメンバーであるミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ。

*Requestbuffersize*   
Common transport コマンドの結果を保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、構造内の SM\_SendCTPassThru\_の RequestBufferSize メンバーにこの情報を返します。

*Requestbuffer*   
Common transport コマンドの結果。 この情報は、ミニポートドライバーによって、SM\_SendCTPassThru\_構造内の RequestBuffer メンバーに返されます。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_SendCTPassThru\_OUT 構造の HBAStatus メンバーにこの情報を返します。

*Totalresponsebuffersize*   
結果の共通トランスポートコマンドのサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendCTPassThru\_OUT 構造体の TotalResponseBufferSize メンバーにこの情報を返します。

*Actualresponsebuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendCTPassThru\_OUT 構造体の ActualResponseBufferSize メンバーでこの情報を返します。

*Responsebuffer*   
Common transport コマンドの結果。 ミニポートドライバーは、SM\_SendCTPassThru\_OUT 構造体の ResponseBuffer メンバーにこの情報を返します。

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

[**SM\_SendCTPassThru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_in)

[**SM\_SendCTPassThru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendctpassthru_out)

 

 






