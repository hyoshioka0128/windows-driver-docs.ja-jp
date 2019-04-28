---
title: SM\_SendRPL 関数
description: SM\_SendRPL WMI メソッドは、指定された宛先ポートに指定されたポートを通じて読み取りポート一覧 (RPL) コマンドを送信します。
ms.assetid: 9297d5eb-f8c4-48f3-8536-a94c66917e66
keywords:
- 記憶装置の SM_SendRPL 関数
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
ms.openlocfilehash: a19413d55e92d1316ad0a72e12a60cbd5f8809b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378920"
---
# <a name="smsendrpl-function"></a>SM\_SendRPL 関数


SM\_SendRPL WMI メソッドは、指定された宛先ポートに指定されたポートを通じて読み取りポート一覧 (RPL) コマンドを送信します。

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
読み取りのポートを使用するには、(RPL) コマンドを一覧表示するローカル ポートのワールドワイド名 (WWN) が送信されます。 この情報は、SM の PortWWN メンバーのミニポート ドライバーに配信\_SendRPL\_構造体。

*AgentWWN*   
ポート種類 FC のポートの一覧を照会するのには、世界中の名 (WWN)\_ポート。 FC の定義については\_ポートを参照してください、T11 委員会の*ファイバー チャネル HBA API*仕様。 この情報は、SM の AgentWWN メンバーのミニポート ドライバーに配信\_SendRPL\_構造体。

*AgentDomain*   
FC の種類のポートの一覧を照会するのには、ドメイン コント ローラーのドメイン数\_ポート。 FC の定義については\_ポートを参照してください、T11 委員会の*ファイバー チャネル HBA API*仕様。 この情報は、エージェントで、ミニポート ドライバーに配信\_SM のドメイン メンバー\_SendRPL\_構造体。

*PortIndex*   
FC の種類のポートの一覧で最初のポートのポート インデックス\_返されるポート。 この情報は、SM の portIndex メンバーのミニポート ドライバーに配信\_SendRPL\_構造体。

*InRespBufferMaxSize*   
応答バッファーの最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SendRPL の HBAStatus メンバー\_構造体。

*TotalRespBufferSize*   
読み取りのポートの一覧 (RPL) コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalRespBufferSize メンバー\_SendRPL\_構造体。

*OutRespBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の OutRespBufferSize メンバー\_SendRPL\_構造体。

*RespBuffer*   
読み取りの結果は、list (RPL) コマンドを移植します。 ミニポート ドライバーでは、この情報を返します、SendRPL の RespBuffer メンバー\_構造体。

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

[**SM\_SendRPL\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566314)

[**SM\_SendRPL\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566315)

 

 






