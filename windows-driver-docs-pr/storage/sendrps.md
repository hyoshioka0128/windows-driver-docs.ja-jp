---
title: SendRPS 関数
description: SendRPS WMI メソッドでは、読み取りのポートの状態のブロック (RPS) 要求を指定したポートまたはドメイン コント ローラーに送信します。
ms.assetid: e8179a42-4095-4c59-81c5-7db7a2985939
keywords:
- 記憶装置の SendRPS 関数
topic_type:
- apiref
api_name:
- SendRPS
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c52a673094b3821c1e80fe6b3b4f60cf44203916
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329985"
---
# <a name="sendrps-function"></a>SendRPS 関数


**SendRPS** WMI メソッドは、指定したポートまたはドメイン コント ローラーに読み取りポート状態ブロック (RPS) 要求を送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendRPS(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                AgentWWN[8],
   [in, HBAType("HBA_WWN")] uint8                ObjectWWN[8],
   [in] uint32                                   AgentDomain,
   [in] uint32                                   ObjectPortNumber,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendRPS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565516)構造体。

*PortWWN*   
RPS コマンドを送信するローカル ポートに世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)構造体。

*AgentWWN*   
ポートのポートの状態を照会するのには、世界中の名前で示されます*ObjectWWN*します。 この情報は、ミニポート ドライバーに配信される、 **AgentWWN**のメンバー、 [ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)構造体。

*ObjectWWN*   
状態が返されるポートのポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **ObjectWWN**のメンバー、 [ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)構造体。

*AgentDomain*   
ポートの状態のクエリを実行するドメイン コント ローラーのドメインの数が示される*ObjectWWN*します。 この情報は、ミニポート ドライバーに配信される、 **AgentDomain**のメンバー、 [ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)構造体。

*ObjectPortNumber*   
状態が返されるポートのポートの世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **ObjectPortNumber**のメンバー、 [ **SendRPS\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565512)構造体。

*TotalRspBufferSize*   
RPS コマンドの結果のバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalRspBufferSize**のメンバー、 [ **SendRPS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565516)構造体。

*ActualRspBufferSize*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualRspBufferSize**のメンバー、 [ **SendRPS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565516)構造体。

*RspBuffer*   
RPS コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **RspBuffer**のメンバー、 [ **SendRPS\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565516)構造体。

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

[**SendRPS\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565512)

[**SendRPS\_OUT**](https://msdn.microsoft.com/library/windows/hardware/ff565516)

 

 






