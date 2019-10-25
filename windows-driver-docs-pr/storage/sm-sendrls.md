---
title: SM\_SendRLS 関数
description: SM\_SendRLS WMI メソッドは、指定されたローカルポートを介して読み取りリンクステータス (RLS) を送信します。 この RLS は、リモートポートに関連付けられているリンクエラー状態ブロックを取得するために、示されたリモートポートに送信されます。
ms.assetid: 4498edde-1249-43b8-b581-37e24f8bd2d3
keywords:
- SM_SendRLS function Storage デバイス
topic_type:
- apiref
api_name:
- SM_SendRLS
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3d779aeb2d2c17ae6f44ff87a891925c2e2c6123
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845459"
---
# <a name="sm_sendrls-function"></a>SM\_SendRLS 関数


SM\_SendRLS WMI メソッドは、指定されたローカルポートを介して読み取りリンクステータス (RLS) を送信します。 この RLS は、リモートポートに関連付けられているリンクエラー状態ブロックを取得するために、示されたリモートポートに送信されます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SM_SendRLS(
   [in, HBAType("HBA_WWN")] uint8              HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8              DestWWN[8],
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
RLS コマンドの送信に使用されるローカルポートのワールド名 (WWN)。 この情報は、SM\_SendRLS\_構造の HbaPortWWN メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートのワールド名 (WWN)。 この情報は、SM の DestWWN メンバーのミニポートドライバーに配信されます。\_SendRLS\_構造体です。

*In火炎 Buffermaxsize*   
応答バッファーの最大サイズ (バイト単位)。

*Hbastatus*   
操作の状態。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、SM\_SendRLS\_OUT 構造体の HBAStatus メンバーにこの情報を返します。

*Total火炎 buffersize*   
RLS コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、SM\_SendRLS\_OUT 構造体の Totalの値のメンバーにこの情報を返します。

* *  
実際に取得されたデータのサイズ (バイト単位)。 この情報は、ミニポートドライバーによって、SM\_SendRLS\_OUT 構造体の Outて Buffersize のメンバーに返されます。

* *  
RLS コマンドの結果。 ミニポートドライバーは、この情報を SM\_SendRLS\_OUT 構造体の出力バッファーに返します。

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

[**SM\_SendRLS\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_sendrls_out)

 

 






