---
title: SM\_SendRPS 関数
description: SM\_SendRPS WMI メソッドは、指定されたポートまたはドメインコントローラーに読み取りポート状態ブロック (RPS) 要求を送信します。
ms.assetid: a64983ef-c665-43db-ad29-0a6f14421ab8
keywords:
- SM_SendRPS 関数記憶装置
topic_type:
- apiref
api_name:
- SM_SendRPS
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6f44a495c4438cd39bd2c3f0570f96be10d82553
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845454"
---
# <a name="sm_sendrps-function"></a>SM\_SendRPS 関数


SM\_SendRPS WMI メソッドは、指定されたポートまたはドメインコントローラーに読み取りポート状態ブロック (RPS) 要求を送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendRPS(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              AgentWWN[8],
   [in, HBAType("HBA_WWN")] uint8              ObjectWWN[8],
   [in] uint32                                 AgentDomain,
   [in] uint32                                 ObjectPortNumber,
   [in] uint32                                 InRespBufferMaxSize,
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS     HBAStatus,
   [out] uint32                                TotalRespBufferSize,
   [out] uint32                                OutRespBufferSize,
   [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*PortWWN*   
RPS コマンドの送信に使用されるローカルポートのワールド名 (WWN)。 この情報は、\_SendRPS\_構造で、SM の PortWWN メンバーのミニポートドライバーに配信されます。

*Agentwwn*   
ObjectWWN によって示されるポートの状態を照会するポートの世界規模の名前 (WWN)。 この情報は、構造内の SM\_SendRPS\_の AgentWWN メンバーのミニポートドライバーに配信されます。

*ObjectWWN*   
ポートの状態を返すポートのワールドワイド名 (WWN)。 この情報は、\_SendRPS\_構造で、SM の ObjectWWN メンバーのミニポートドライバーに配信されます。

*Agentdomain*   
ObjectWWN によって示されるポートの状態を照会するドメインコントローラーのドメイン番号。 この情報は、\_SendRPS\_構造の AgentDomain メンバーのミニポートドライバーに配信されます。

*Objectportnumber*番号   
ポートの状態を返すポートのワールドワイド名 (WWN)。 この情報は、構造内の SM\_SendRPS\_の ObjectPortNumber メンバーのミニポートドライバーに配信されます。

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

[**SM\_SendRPS\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrps_out)

 

 






