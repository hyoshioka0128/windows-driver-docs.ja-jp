---
title: SM\_SendSRL 関数
description: SM\_SendSRL WMI メソッドは、指定されたドメイン コント ローラーに指定されたポートを通じてスキャン リモート ループ (SRL) コマンドを送信します。
ms.assetid: 44090e8d-ffb2-48a9-a574-5bf067ffa952
keywords:
- 記憶装置の SM_SendSRL 関数
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
ms.openlocfilehash: 9f338f33877252beb2508b0733bf043b7e17b39d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380592"
---
# <a name="smsendsrl-function"></a>SM\_SendSRL 関数


SM\_SendSRL WMI メソッドは、指定されたドメイン コント ローラーに指定されたポートを通じてスキャン リモート ループ (SRL) コマンドを送信します。

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
SRL コマンドを送信するローカル ポートの世界中の名 (WWN)。 この情報は、SM の HbaPortWWN メンバーのミニポート ドライバーに配信\_SendSRL\_構造体。

*WWN*   
FL の種類のポートのワールドワイド名 (WWN)\_ループは、スキャンするポート。 この情報は、SM の WWN メンバーでは、ミニポート ドライバーに配信される\_SendSRL\_構造体。

*ドメイン*   
ループがスキャンするには、ドメインのドメインの数。 この情報は、SM のドメイン メンバーでは、ミニポート ドライバーに配信される\_SendSRL\_構造体。

*InRespBufferMaxSize*   
応答バッファーの最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SendRPL の HBAStatus メンバー\_構造体。

*TotalRespBufferSize*   
RPS コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalRespBufferSize メンバー\_SendRPS\_構造体。

*OutRespBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の OutRespBufferSize メンバー\_SendRPL\_構造体。

*RespBuffer*   
RPS コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の RespBuffer メンバー\_SendRPS\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、ミリ秒に属する\_SM\_FabricAndDomainManagementMethods WMI クラスです。

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
<td align="left">Hbapiwmi.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SM\_SendSRL\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_sm_sendsrl_out)

 

 






