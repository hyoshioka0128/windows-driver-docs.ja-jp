---
title: SendRPL 関数
description: SendRPL WMI メソッドでは、読み取りのポートの一覧 (RPL) コマンドを指定されたポートを通じて指定された宛先ポートに送信します。
ms.assetid: 3cf3dfe2-6ff9-431f-b6bf-66ef8dd77df3
keywords:
- 記憶装置の SendRPL 関数
topic_type:
- apiref
api_name:
- SendRPL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0dc71f1aef614860f95fa884aa93e21d7929eb30
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532464"
---
# <a name="sendrpl-function"></a>SendRPL 関数


**SendRPL** WMI メソッドは、指定された宛先ポートに指定されたポートを通じて読み取りポート一覧 (RPL) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendRPL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                AgentWWN[8],
   [in] uint32                                   agent_domain,
   [in] uint32                                   portIndex,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendRPL\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565503)構造体。

*PortWWN*   
世界中の名前読み取りのポートを使用するには、(RPL) コマンドを一覧表示、ローカル ポートに送信されます。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)構造体。

*AgentWWN*   
ポート種類 FC のポートの一覧を照会するのには、世界中の名前\_ポート。 FC の定義については\_ポートを参照してください、T11 委員会の*ファイバー チャネル HBA API*仕様。 この情報は、ミニポート ドライバーに配信される、 **AgentWWN**のメンバー、 [ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)構造体。

*エージェント\_ドメイン*   
FC の種類のポートの一覧を照会するのには、ドメイン コント ローラーのドメイン数\_ポート。 FC の定義については\_ポートを参照してください、T11 委員会の*ファイバー チャネル HBA API*仕様。 この情報は、ミニポート ドライバーに配信される、**エージェント\_ドメイン**のメンバー、 [ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)構造体。

*portIndex*   
FC の種類のポートの一覧で最初のポートのポート インデックス\_返されるポート。 この情報は、ミニポート ドライバーに配信される、 **portIndex**のメンバー、 [ **SendRPL\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565496)構造体。

*TotalRspBufferSize*   
読み取りのポートの一覧 (RPL) コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalRspBufferSize**のメンバー、 [ **SendRPL\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565503)構造体。

*ActualRspBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualRspBufferSize**のメンバー、 [ **SendRPL\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565503)構造体。

*RspBuffer*   
読み取りの結果は、list (RPL) コマンドを移植します。 ミニポート ドライバーには、この情報が返されます、 **RspBuffer**のメンバー、 [ **SendRPL\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565503)構造体。

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

[**SendRPL\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565496)

[**SendRPL\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565503)

 

 






