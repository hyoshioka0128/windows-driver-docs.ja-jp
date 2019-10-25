---
title: SendCTPassThru 関数
description: SendCTPassThru WMI メソッドは、指定されたポートに common transport (CT) パススルーコマンドを送信します。
ms.assetid: 7f512980-5aff-4359-b52e-7fcef9627e1f
keywords:
- SendCTPassThru 関数のストレージデバイス
topic_type:
- apiref
api_name:
- SendCTPassThru
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 356b83d984a78276415c2940c4cb9a527aa950d6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823797"
---
# <a name="sendctpassthru-function"></a>SendCTPassThru 関数


**Sendctpassthru** WMI メソッドは、指定されたポートに common TRANSPORT (CT) パススルーコマンドを送信します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void SendCTPassThru(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus,
   [in, HBAType("HBA_WWN")] uint8                      PortWWN[8],
   [in] uint32                                         RequestBufferCount,
   [in, WmiSizeIs("RequestBufferCount")] uint8         RequestBuffer[],
   [out] uint32                                        TotalResponseBufferCount,
   [out] uint32                                        ActualResponseBufferCount,
   [out, WmiSizeIs("ActualResponseBufferCount")] uint8 ResponseBuffer[]
);
```

<a name="parameters"></a>パラメーター
----------

*Hbastatus*   
戻ると、操作の状態が格納されます。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Sendctpassthru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)構造の**hbastatus**メンバーでこの情報を返します。

*PortWWN*   
ターゲットへのアクセスに使用される HBA のワールド名。 この情報は、 **PortWWN**の[**sendctpassthru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)のメンバーであるミニポートドライバーに配信されます。

*RequestBufferCount*   
Common transport コマンドの結果を保持するバッファーのサイズ (バイト単位)。 ミニポートドライバーは、 **RequestBufferCount**構造体の[**sendctpassthru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)のメンバーであるこの情報を返します。

*Requestbuffer*   
Common transport コマンドの結果。 ミニポートドライバーは、構造[**内の Sendctpassthru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)の**requestbuffer**メンバーでこの情報を返します。

*TotalResponseBufferCount*   
結果の共通トランスポートコマンドのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendctpassthru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)構造体の**TotalResponseBufferCount**メンバーにこの情報を返します。

*ActualResponseBufferCount*   
実際に取得されたデータのサイズ (バイト単位)。 ミニポートドライバーは、 [**Sendctpassthru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)構造体の**ActualResponseBufferCount**メンバーにこの情報を返します。

*Responsebuffer*   
Common transport コマンドの結果。 ミニポートドライバーは、 [**Sendctpassthru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)構造体の**responsebuffer**メンバーでこの情報を返します。

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

[**の SendCTPassThru\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_in)

[**SendCTPassThru\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sendctpassthru_out)

 

 






