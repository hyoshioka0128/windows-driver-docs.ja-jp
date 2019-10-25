---
title: SendRPL 関数
description: SendRPL WMI メソッドは、指定されたポートを使用して、指定された宛先ポートに読み取りポートリスト (RPL) コマンドを送信します。
ms.assetid: 3cf3dfe2-6ff9-431f-b6bf-66ef8dd77df3
keywords:
- SendRPL 関数のストレージデバイス
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
ms.openlocfilehash: 58460bbed809a64ea313cde127218e10f197bff8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832012"
---
# <a name="sendrpl-function"></a>SendRPL 関数


**Sendrpl** WMI メソッドは、指定されたポートを使用して、指定された宛先ポートに読み取りポートリスト (RPL) コマンドを送信します。

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

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendrpl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)構造の**hbastatus**メンバーにこの情報を返します。

*PortWWN*   
読み取りポート一覧 (RPL) コマンドが送信されるローカルポートの世界規模の名前。 この情報は、構造[**内の Sendrpl\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)の**PortWWN**メンバーのミニポートドライバーに配信されます。

*Agentwwn*   
FC\_ポートの種類のポートの一覧を照会するポートの世界規模の名前。 FC\_ポートの定義については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、構造[**内の Sendrpl\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)の**agentwwn**メンバーのミニポートドライバーに配信されます。

*エージェント\_ドメイン*   
FC\_ポートの種類のポートの一覧を照会するドメインコントローラーのドメイン番号。 FC\_ポートの定義については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、構造[**内の Sendrpl\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)の**エージェント\_ドメイン**メンバーのミニポートドライバーに配信されます。

*Portindex*   
返される FC\_ポートの種類のポートの一覧にある、最初のポートのポートインデックス。 この情報は、構造[**内の Sendrpl\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)の**portindex**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
読み取りポートリスト (RPL) コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrpl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrpl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)構造体の**Actualrspbuffersize**メンバーにこの情報を返します。

*Rspbuffer*   
読み取りポートリスト (RPL) コマンドの結果。 ミニポートドライバーは、 [**Sendrpl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)構造体の**rspbuffer**メンバーでこの情報を返します。

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

[**の SendRPL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_in)

[**SendRPL\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrpl_out)

 

 






