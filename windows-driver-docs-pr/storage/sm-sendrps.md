---
title: SM\_SendRPS 関数
description: SM\_SendRPS WMI メソッドは、指定したポートまたはドメイン コント ローラーに読み取りポート状態ブロック (RPS) 要求を送信します。
ms.assetid: a64983ef-c665-43db-ad29-0a6f14421ab8
keywords:
- 記憶装置の SM_SendRPS 関数
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
ms.openlocfilehash: 6e662a22b27114ee6faf4629340c20cc3611baf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378902"
---
# <a name="smsendrps-function"></a>SM\_SendRPS 関数


SM\_SendRPS WMI メソッドは、指定したポートまたはドメイン コント ローラーに読み取りポート状態ブロック (RPS) 要求を送信します。

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
RPS コマンドを送信するローカル ポートの世界中の名 (WWN)。 この情報は、SM の PortWWN メンバーのミニポート ドライバーに配信\_SendRPS\_構造体。

*AgentWWN*   
ObjectWWN で示されるポートの状態を照会するのには、ポートの世界中の名 (WWN)。 この情報は、SM の AgentWWN メンバーのミニポート ドライバーに配信\_SendRPS\_構造体。

*ObjectWWN*   
世界中の状態が返されるポートのポート名 (WWN) この情報は、SM の ObjectWWN メンバーのミニポート ドライバーに配信\_SendRPS\_構造体。

*AgentDomain*   
ObjectWWN で示されるポートの状態のクエリを実行するドメイン コント ローラーのドメインの数。 この情報は、SM の AgentDomain メンバーのミニポート ドライバーに配信\_SendRPS\_構造体。

*ObjectPortNumber*   
世界中の状態が返されるポートのポート名 (WWN) この情報は、SM の ObjectPortNumber メンバーのミニポート ドライバーに配信\_SendRPS\_構造体。

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

[**SM\_SendRPS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566320)

 

 






