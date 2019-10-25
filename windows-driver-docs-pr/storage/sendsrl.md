---
title: SendSRL 関数
description: SendSRL WMI メソッドは、指定されたポートを使用して、指定されたドメインコントローラーに scan remote loop (SRL) コマンドを送信します。
ms.assetid: b191fc8c-2765-4e39-aab7-e950ae1d46b0
keywords:
- SendSRL 関数のストレージデバイス
topic_type:
- apiref
api_name:
- SendSRL
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 377f9278c06c7b09a71b680b7571c3b10fd9b97c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842436"
---
# <a name="sendsrl-function"></a>SendSRL 関数


**Sendsrl** WMI メソッドは、指定されたポートを使用して、指定されたドメインコントローラーに scan remote LOOP (SRL) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendSRL(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                PortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                WWN[8],
   [in] uint32                                   Domain,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendsrl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)構造体の**hbastatus**メンバーにこの情報を返します。

*PortWWN*   
SRL コマンドの送信に使用するローカルポートの世界規模の名前。 この情報は、構造内の SendSRL\_の**PortWWN**メンバーのミニポートドライバーに配信されます。

*WWN*   
スキャンされるループの種類が FL\_ポートの世界規模の名前。 この情報は、構造内の SendSRL\_の**WWN**メンバーのミニポートドライバーに配信されます。

*ドメイン*   
ループがスキャンされるドメインのドメイン番号。 この情報は、構造内の SendSRL\_の**ドメイン**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
SRL コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendsrl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendsrl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)構造体の**Actualrspbuffersize**メンバーにこの情報を返します。

*Rspbuffer*   
SRL コマンドの結果。 ミニポートドライバーは、 [**Sendsrl\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)構造体の**rspbuffer**メンバーにこの情報を返します。

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

[ **Sendsrl\_OUT**の sendsrl\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendsrl_out)

 

 






