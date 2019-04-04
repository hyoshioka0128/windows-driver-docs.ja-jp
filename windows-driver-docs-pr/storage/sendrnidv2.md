---
title: SendRNIDV2 関数
description: SendRNIDV2 WMI メソッドは、バージョン 2 の RNID コマンドを指定されたポートに送信します。
ms.assetid: ac9304b3-498b-4349-befd-529a4978bb52
keywords:
- 記憶装置の SendRNIDV2 関数
topic_type:
- apiref
api_name:
- SendRNIDV2
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8a68d1f9410c5e0e6aab3f2517ec9c2868027491
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570091"
---
# <a name="sendrnidv2-function"></a>SendRNIDV2 関数


**SendRNIDV2** WMI メソッドは、指定されたポートにバージョン 2 RNID コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendRNIDV2(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint32                                   DestFCID,
   [in] uint32                                   NodeIdDataFormat,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、[HBA\_状態](hba-status.md)を参照してください。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendRNIDV2\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565476)構造体。

*PortWWN*   
バージョン 2 RNID コマンドを送信するローカル ポートに世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SendRNIDV2\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565472)構造体。

*DestWWN*   
接続先ポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **DestWWN**のメンバー、 [ **SendRNIDV2\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565472)構造体。

*DestFCID*   
接続先ポートのアドレス識別子。 この情報は、ミニポート ドライバーに配信される、 **DestFCID**のメンバー、 [ **SendRNIDV2\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565472)構造体。

*NodeIdDataFormat*   
ノードの id データの形式。 このメンバーの値については、T11 委員会を参照してください。*ファイバー チャネル HBA API*仕様。 この情報は、ミニポート ドライバーに配信される、 **NodeIdDataFormat**のメンバー、 [ **SendRNIDV2\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565472)構造体。

*TotalRspBufferSize*   
バージョン 2 の RNID コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalRspBufferSize**のメンバー、 [ **SendRNIDV2\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565476)構造体。

*ActualRspBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualRspBufferSize**のメンバー、 [ **SendRNIDV2\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565476)構造体。

*RspBuffer*   
バージョン 2 の RNID コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **RspBuffer**のメンバー、 [ **SendRNIDV2\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565476)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>コメント
-------

この WMI メソッドが属する、 [MSFC\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)します。

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

[**SendRNIDV2\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565472)

[**SendRNIDV2\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565476)

 

 






