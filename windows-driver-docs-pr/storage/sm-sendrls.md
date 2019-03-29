---
title: SM\_SendRLS 関数
description: SM\_SendRLS WMI メソッドは、指定したローカル ポートを介して読み取りリンクのステータス (RLS) を送信します。 この RLS は、リモートのポートに関連付けられているリンク エラー状態のブロックを取得する対象のリモート ポートに送信されます。
ms.assetid: 4498edde-1249-43b8-b581-37e24f8bd2d3
keywords:
- 記憶装置の SM_SendRLS 関数
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
ms.openlocfilehash: 86a2da5a4c0210f281cfaf56968757cab19960db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579824"
---
# <a name="smsendrls-function"></a>SM\_SendRLS 関数


SM\_SendRLS WMI メソッドは、指定したローカル ポートを介して読み取りリンクのステータス (RLS) を送信します。 この RLS は、リモートのポートに関連付けられているリンク エラー状態のブロックを取得する対象のリモート ポートに送信されます。

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
RLS コマンドを送信するローカル ポートの世界中の名 (WWN)。 この情報は、SM の HbaPortWWN メンバーのミニポート ドライバーに配信\_SendRLS\_構造体。

*DestWWN*   
接続先ポートの世界中の名 (WWN)。 この情報は、SM の DestWWN メンバーのミニポート ドライバーに配信\_SendRLS\_構造体。

*InRespBufferMaxSize*   
応答バッファーのバイト単位で最大サイズ。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_SendRLS\_構造体。

*TotalRespBufferSize*   
RLS コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalRespBufferSize メンバー\_SendRLS\_構造体。

*OutRespBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の OutRespBufferSize メンバー\_SendRLS\_構造体。

*RespBuffer*   
RLS コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の RespBuffer メンバー\_SendRLS\_構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドは、ミリ秒に属する\_SM\_FabricAndDomainManagementMethods WMI クラスです。

<a name="requirements"></a>必要条件
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

[**SM\_SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566305)

 

 






