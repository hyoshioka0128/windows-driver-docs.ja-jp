---
title: SendRLS 関数
description: SendRLS WMI メソッドでは、読み取りリンクのエラー ステータス ブロック (RLS) を指定したローカル ポートを介してリモート ポートに関連付けられた、リンク エラーの状態のブロックを取得する対象のリモート ポートに送信します。
ms.assetid: 57dcc810-023f-4dbf-a9c2-3062765729c7
keywords:
- 記憶装置の SendRLS 関数
topic_type:
- apiref
api_name:
- SendRLS
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 02121f426a757a068598e603dbf99101acaeb99d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527264"
---
# <a name="sendrls-function"></a>SendRLS 関数


**SendRLS** WMI メソッドは、リモートのポートに関連付けられた、リンク エラーの状態のブロックを取得する対象のリモート ポートに示されたローカル ポートを介して読み取りリンクのエラー ステータス ブロック (RLS) を送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendRLS(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565452)構造体。

*PortWWN*   
RLS コマンドを送信するローカル ポートに世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SendRLS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565446)構造体。

*DestWWN*   
接続先ポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DestWWN**のメンバー、 [ **SendRLS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565446)構造体。

*TotalRspBufferSize*   
RLS コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalRspBufferSize**のメンバー、 [ **SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565452)構造体。

*ActualRspBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualRspBufferSize**のメンバー、 [ **SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565452)構造体。

*RspBuffer*   
RLS コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **RspBuffer**のメンバー、 [ **SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565452)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

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
<td align="left">Hbapiwmi.h (Hbapiwmi.h、Hbaapi.h、Hbaapi.h など)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi.lib</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[HBA\_状態](hba-status.md)

[**SendRLS\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565446)

[**SendRLS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565452)

 

 






