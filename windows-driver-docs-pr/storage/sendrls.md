---
title: SendRLS 関数
description: SendRLS WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートに読み取りリンクエラー状態ブロック (RLS) を送信し、リモートポートに関連付けられているリンクエラー状態ブロックを取得します。
ms.assetid: 57dcc810-023f-4dbf-a9c2-3062765729c7
keywords:
- SendRLS 関数記憶装置
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
ms.openlocfilehash: dfe0a38e146c2efd343e634e44c8d75ff629d3ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832043"
---
# <a name="sendrls-function"></a>SendRLS 関数


**Sendrls** WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートに読み取りリンクエラー状態ブロック (RLS) を送信し、リモートポートに関連付けられているリンクエラー状態ブロックを取得します。

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

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendrls\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)構造の**hbastatus**メンバーでこの情報を返します。

*PortWWN*   
RLS コマンドの送信に使用されるローカルポートの世界規模の名前。 この情報は、構造[**内の Sendrls\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)の**PortWWN**メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートの世界規模の名前。 この情報は、構造[**内の Sendrls\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)の**destwwn**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
RLS コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrls\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendrls\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)構造体の**Actualrspbuffersize**メンバーでこの情報を返します。

*Rspbuffer*   
RLS コマンドの結果。 ミニポートドライバーは、 [**Sendrls\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)構造体の**rspbuffer**メンバーでこの情報を返します。

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

[**の SendRLS\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_in)

[**SendRLS\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendrls_out)

 

 






