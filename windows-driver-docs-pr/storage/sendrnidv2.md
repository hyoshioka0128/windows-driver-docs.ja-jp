---
title: SendRNIDV2 関数
description: SendRNIDV2 WMI メソッドは、指定されたポートにバージョン 2 RNID コマンドを送信します。
ms.assetid: ac9304b3-498b-4349-befd-529a4978bb52
keywords:
- SendRNIDV2 function Storage デバイス
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
ms.openlocfilehash: 03c2970e4ac9ed95c2566d8a1852facae0d9502c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832019"
---
# <a name="sendrnidv2-function"></a>SendRNIDV2 関数


**SendRNIDV2** WMI メソッドは、指定されたポートにバージョン 2 rnid コマンドを送信します。

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

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)構造体の**hbastatus**メンバーにこの情報を返します。

*PortWWN*   
バージョン2の RNID コマンドの送信に使用されるローカルポートの世界規模の名前。 この情報は、構造体の[**SendRNIDV2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)の**PortWWN**メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートの世界規模の名前。 この情報は、構造[**内の SendRNIDV2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)の**destwwn**メンバーのミニポートドライバーに配信されます。

*DestFCID*   
宛先ポートのアドレス識別子。 この情報は、構造体の[**SendRNIDV2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)の**DestFCID**メンバーのミニポートドライバーに配信されます。

*NodeIdDataFormat*   
ノード識別データ形式。 このメンバーが持つことができる値の詳細については、T11 委員会の*ファイバーチャネル HBA API*仕様を参照してください。 この情報は、構造体の[**SendRNIDV2\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)の**NodeIdDataFormat**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
バージョン 2 RNID コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)構造体の**Actualrspbuffersize**メンバーにこの情報を返します。

*Rspbuffer*   
バージョン 2 RNID コマンドの結果。 ミニポートドライバーは、 [**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)構造体の**rspbuffer**メンバーでこの情報を返します。

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

[**SendRNIDV2\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_in)

[**SendRNIDV2\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrnidv2_out)

 

 






