---
title: SendRPS 関数
description: SendRPS WMI メソッドは、指定されたポートまたはドメインコントローラーに読み取りポート状態ブロック (RPS) 要求を送信します。
ms.assetid: e8179a42-4095-4c59-81c5-7db7a2985939
keywords:
- SendRPS 関数のストレージデバイス
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
ms.openlocfilehash: 3a62e8d584632efff2d27e972fa4fc0a65f85234
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838030"
---
# <a name="sendrps-function"></a>SendRPS 関数


**Sendrps** WMI メソッドは、指定されたポートまたはドメインコントローラーに読み取りポート状態ブロック (RPS) 要求を送信します。

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

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendrps\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_out)構造の**hbastatus**メンバーにこの情報を返します。

*PortWWN*   
RPS コマンドの送信に使用するローカルポートの世界規模の名前。 この情報は、構造[**内の Sendrps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)の**PortWWN**メンバーのミニポートドライバーに配信されます。

*Agentwwn*   
*ObjectWWN*によって示されるポートの状態を照会するポートの世界規模の名前。 この情報は、構造[**内の Sendrps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)の**agentwwn**メンバーのミニポートドライバーに配信されます。

*ObjectWWN*   
ポートの状態を返すポートの世界中の名前。 この情報は、構造[**内の Sendrps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)の**ObjectWWN**メンバーのミニポートドライバーに配信されます。

*Agentdomain*   
*ObjectWWN*によって示されるポートの状態を照会するドメインコントローラーのドメイン番号。 この情報は、構造[**内の Sendrps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)の**agentdomain**メンバーのミニポートドライバーに配信されます。

*Objectportnumber*番号   
ポートの状態を返すポートの世界中の名前。 この情報は、構造[**内の Sendrps\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)の**objectportnumber**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
RPS コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrps\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrps\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_out)構造体の**Actualrspbuffersize**メンバーでこの情報を返します。

*Rspbuffer*   
RPS コマンドの結果。 ミニポートドライバーは、 [**Sendrps\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_out)構造体の**rspbuffer**メンバーでこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

この WMI メソッドは、 [Msfc\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)に属しています。

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
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>Library</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[HBA\_の状態](hba-status.md)

[**SendRPS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_in)

[**SendRPS\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrps_out)

 

 






