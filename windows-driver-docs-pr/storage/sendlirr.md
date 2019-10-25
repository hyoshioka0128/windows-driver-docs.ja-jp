---
title: SendLIRR 関数
description: SendLIRR WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートにリンクインシデントレコード登録 (LIRR) コマンドを送信します。
ms.assetid: ca54161d-d5fe-4775-a38c-dfaf3fd8c00b
keywords:
- SendLIRR 関数のストレージデバイス
topic_type:
- apiref
api_name:
- SendLIRR
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c17a6c0a401ab17b519842506055e81ccc570a52
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832077"
---
# <a name="sendlirr-function"></a>SendLIRR 関数


**Sendlirr** WMI メソッドは、指定されたローカルポートを介して、指定されたリモートポートにリンクインシデントレコード登録 (lirr) コマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendLIRR(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS       HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                SourceWWN[8],
   [in, HBAType("HBA_WWN")] uint8                DestWWN[8],
   [in] uint8                                    Function,
   [in] uint8                                    Type,
   [out] uint32                                  TotalRspBufferSize,
   [out] uint32                                  ActualRspBufferSize,
   [out, WmiSizeIs("ActualRspBufferSize")] uint8 RspBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendlirr\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造の**hbastatus**メンバーにこの情報を返します。

*Sourcewwn*   
LIRR コマンドの送信に使用されるローカルポートの世界規模の名前。 この情報は、構造[**内の Sendlirr\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)の**sourcewwn**メンバーのミニポートドライバーに配信されます。

*Destwwn*   
宛先ポートの世界規模の名前。 この情報は、構造[**内の Sendlirr\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)の**destwwn**メンバーのミニポートドライバーに配信されます。

*関数*   
実行する登録関数を識別するコード。 このメンバーに割り当てることができる値の説明については、T11 委員会の*ファイバーチャネルフレーミングとシグナリング*の仕様を参照してください。 この情報は、構造[**内の Sendlirr\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)の**関数**メンバーのミニポートドライバーに配信されます。

*型*   
リンク情報が要求されるデバイスの種類。 このメンバーに割り当てることができる値の説明については、T11 委員会の*ファイバーチャネルフレーミングとシグナリング*の仕様を参照してください。 この情報は、構造[**内の Sendlirr\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)の**関数**メンバーのミニポートドライバーに配信されます。

*Totalrspbuffersize*   
LIRR コマンドの結果のサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendlirr\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体の**Totalrspbuffersize**メンバーにこの情報を返します。

*Actualrspbuffersize*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendlirr\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体の**Actualrspbuffersize**メンバーにこの情報を返します。

*Rspbuffer*   
LIRR コマンドの結果。 ミニポートドライバーは、 [**Sendlirr\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)構造体の**rspbuffer**メンバーにこの情報を返します。

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

[**SendLIRR\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_in)

[**SendLIRR\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendlirr_out)

 

 






