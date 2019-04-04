---
title: SM\_SendCTPassThru 関数
description: SM\_SendCTPassThru WMI メソッドは、指定されたポートに一般的なトランスポート (CT) パススルー コマンドを送信します。
ms.assetid: 437f0c79-78f6-406e-8774-79de4425bfe8
keywords:
- 記憶装置の SM_SendCTPassThru 関数
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
ms.openlocfilehash: 25b0276fee830c90e681222fa078712aea7fdbfe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559376"
---
# <a name="smsendctpassthru-function"></a>SM\_SendCTPassThru 関数


SM\_SendCTPassThru WMI メソッドは、指定されたポートに一般的なトランスポート (CT) パススルー コマンドを送信します。

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
ターゲットにアクセスする HBA の世界中の名 (WWN)。 この情報は、SendCTPassThru の PortWWN メンバーのミニポート ドライバーに配信\_構造体。

*InRespBufferMaxSize*   
応答バッファーの最大サイズ。

*RequestBufferSize*   
一般的なトランスポート コマンドの結果を保持するバッファーのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の RequestBufferSize メンバー\_SendCTPassThru\_構造体。

*RequestBuffer*   
一般的なトランスポート コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の RequestBuffer メンバー\_SendCTPassThru\_構造体。

*HBAStatus*   
操作の状態。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーでは、この情報を返します、SM の HBAStatus メンバー\_SendCTPassThru\_構造体。

*TotalResponseBufferSize*   
結果の一般的なトランスポート コマンドのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の TotalResponseBufferSize メンバー\_SendCTPassThru\_構造体。

*ActualResponseBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーでは、この情報を返します、SM の ActualResponseBufferSize メンバー\_SendCTPassThru\_構造体。

*ResponseBuffer*   
一般的なトランスポート コマンドの結果。 ミニポート ドライバーでは、この情報を返します、SM の ResponseBuffer メンバー\_SendCTPassThru\_構造体。

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

[**SM\_SendCTPassThru\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff566293)

[**SM\_SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff566294)

 

 






