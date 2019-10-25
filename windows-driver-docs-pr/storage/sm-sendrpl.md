---
title: SM\_SendRPL 関数
description: SM\_SendRPL WMI メソッドは、指定されたポートを介して、指定された宛先ポートに読み取りポートリスト (RPL) コマンドを送信します。
ms.assetid: 9297d5eb-f8c4-48f3-8536-a94c66917e66
keywords:
- SM_SendRPL function Storage デバイス
topic_type:
- apiref
api_name:
- SM_SendRPL
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f7d6e399de3f03604080108621875c00a73ad541
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845455"
---
# <a name="sm_sendrpl-function"></a>SM\_SendRPL 関数


SM\_SendRPL WMI メソッドは、指定されたポートを介して、指定された宛先ポートに読み取りポートリスト (RPL) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendRPL(
   [in, HBAType("HBA_WWN")] uint8              PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              AgentWWN[8],
   [in] uint32                                 AgentDomain,
   [in] uint32                                 PortIndex,
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
読み取りポート一覧 (RPL) コマンドの送信に使用されるローカルポートのワールド名 (WWN)。 この情報は、構造内の SM\_SendRPL\_の PortWWN メンバーのミニポートドライバーに配信されます。

*Agentwwn*   
FC\_ポートの種類のポートの一覧を照会するポートのワールドワイド名 (WWN)。 FC\_ポートの定義については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、構造内の SM\_SendRPL\_の AgentWWN メンバーのミニポートドライバーに配信されます。

*Agentdomain*   
FC\_ポートの種類のポートの一覧を照会するドメインコントローラーのドメイン番号。 FC\_ポートの定義については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、\_構造内の SM\_SendRPL のエージェント\_ドメインメンバーのミニポートドライバーに配信されます。

*Portindex*   
返される FC\_ポートの種類のポートの一覧にある、最初のポートのポートインデックス。 この情報は、構造内の SM\_SendRPL\_の portIndex メンバーのミニポートドライバーに配信されます。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SendRPL\_OUT 構造の HBAStatus メンバーにこの情報を返します。

*Total火炎 buffersize*   
読み取りポート一覧 (RPL) コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendRPL\_OUT 構造体の Total火炎 Buffersize メンバーにこの情報を返します。

* *  
実際に取得されたデータのサイズ (バイト単位)。 この情報は、ミニポートドライバーによって、SM\_SendRPL\_OUT 構造の外部のメンバーに返されます。

* *  
読み取りポートリスト (RPL) コマンドの結果。 ミニポートドライバーは、SendRPL\_OUT 構造体の値を取得します。

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

[**SM\_SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_in)

[**SM\_SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrpl_out)

 

 






