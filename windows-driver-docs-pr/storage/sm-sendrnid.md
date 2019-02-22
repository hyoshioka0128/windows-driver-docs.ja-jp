---
title: SM\_SendRNID 関数
description: SM\_SendRNID WMI メソッドは、指定されたポートに要求ノードの id データ (RNID) コマンドを送信します。
ms.assetid: 160e2dc7-8195-4f8a-bc59-854e5283cf6f
keywords:
- 記憶装置の SM_SendRNID 関数
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
ms.openlocfilehash: 11c6959fcfc6155ebb85dda55c1e8003917ca34d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557464"
---
# <a name="smsendrnid-function"></a>SM\_SendRNID 関数


SM\_SendRNID WMI メソッドは、指定されたポートに要求ノードの id データ (RNID) コマンドを送信します。

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
RNID コマンドを送信するローカル ポートの世界中の名 (WWN)。 この情報は、SM の PortWWN メンバーのミニポート ドライバーに配信\_SendRNID\_構造体。

*DestWWN*   
接続先ポートの世界中の名 (WWN)。 この情報は、SM の DestWWN メンバーのミニポート ドライバーに配信\_SendRNID\_構造体。

*DestFCID*   
接続先ポートのアドレス識別子。 この情報は、SM の DestFCID メンバーのミニポート ドライバーに配信\_SendRNID\_構造体。

*NodeIdDataFormat*   
ノードの id データの形式。 このメンバーの値については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。 この情報は、SM の NodeIdDataFormat メンバーのミニポート ドライバーに配信\_SendRNID\_構造体。

*InRespBufferMaxSize*   
応答バッファーの最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_SendRNID\_構造体。

*TotalRespBufferSize*   
RNID コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalRspBufferSize メンバー\_SendRNID\_構造体。

*ResponseBufferSize*   
RNID コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の ResponseBufferSize メンバー\_SendRNID\_構造体。

*ResponseBuffer*   
RNID コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の ResponseBuffer メンバー\_SendRNID\_構造体。

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

[**SM\_SendRNID\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566308)

[**SM\_SendRNID\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566310)

 

 






