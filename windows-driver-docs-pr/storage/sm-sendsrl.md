---
title: SM\_SendSRL 関数
description: SM\_SendSRL WMI メソッドは、指定されたポートを使用して、指定されたドメインコントローラーに scan remote loop (SRL) コマンドを送信します。
ms.assetid: 44090e8d-ffb2-48a9-a574-5bf067ffa952
keywords:
- SM_SendSRL 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SendSRL
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 48aa5f53278063beccf884512293d3352a8117bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845451"
---
# <a name="sm_sendsrl-function"></a>SM\_SendSRL 関数


SM\_SendSRL WMI メソッドは、指定されたポートを使用して、指定されたドメインコントローラーに scan remote loop (SRL) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendSRL(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              WWN[8],
   [in] uint32                                 Domain,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HbaPortWWN*   
SRL コマンドの送信に使用するローカルポートのワールド名 (WWN)。 この情報は、SM の HbaPortWWN メンバーのミニポートドライバーに配信され、構造内の SendSRL\_\_ます。

*WWN*   
スキャンされるループの種類が FL\_ポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendSRL\_の WWN メンバーのミニポートドライバーに配信されます。

*ドメイン*   
ループがスキャンされるドメインのドメイン番号。 この情報は、構造内の SM\_SendSRL\_のドメインメンバーのミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SendRPL\_OUT 構造の HBAStatus メンバーにこの情報を返します。

*Total火炎 buffersize*   
RPS コマンドの結果のサイズ (バイト単位)。 この情報は、ミニポートドライバーによって、SM\_SendRPS\_OUT 構造の Total火炎 Buffersize メンバーに返されます。

* *  
実際に取得されたデータのサイズ (バイト単位)。 この情報は、ミニポートドライバーによって、SM\_SendRPL\_OUT 構造の外部のメンバーに返されます。

* *  
RPS コマンドの結果。 ミニポートドライバーは、この情報を SM\_SendRPS\_OUT 構造体の出力バッファーに返します。

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

[**SM\_SendSRL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendsrl_out)

 

 






