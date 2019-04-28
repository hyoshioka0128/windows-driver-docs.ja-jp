---
title: SendCTPassThru 関数
description: SendCTPassThru WMI メソッドは、一般的なトランスポート (CT) パススルー コマンドを指定されたポートに送信します。
ms.assetid: 7f512980-5aff-4359-b52e-7fcef9627e1f
keywords:
- 記憶装置の SendCTPassThru 関数
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
ms.openlocfilehash: 3f1d2e83cfd027776e940032543daddec2bba636
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378531"
---
# <a name="sendctpassthru-function"></a>SendCTPassThru 関数


**SendCTPassThru** WMI メソッドは、指定されたポートに一般的なトランスポート (CT) パススルー コマンドを送信します。

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

*HBAStatus*   
に返された場合、操作の状態を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565413)構造体。

*PortWWN*   
ターゲットにアクセスする HBA の世界中の名前。 この情報は、ミニポート ドライバーに配信される、 **PortWWN**のメンバー、 [ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)構造体。

*RequestBufferCount*   
一般的なトランスポート コマンドの結果を保持するバッファーのバイト サイズ。 ミニポート ドライバーには、この情報が返されます、 **RequestBufferCount**のメンバー、 [ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)構造体。

*RequestBuffer*   
一般的なトランスポート コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **RequestBuffer**のメンバー、 [ **SendCTPassThru\_IN** ](https://msdn.microsoft.com/library/windows/hardware/ff565412)構造体。

*TotalResponseBufferCount*   
結果の一般的なトランスポート コマンドのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **TotalResponseBufferCount**のメンバー、 [ **SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565413)構造体。

*ActualResponseBufferCount*   
実際に取得されたデータのバイト単位のサイズ。 ミニポート ドライバーには、この情報が返されます、 **ActualResponseBufferCount**のメンバー、 [ **SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565413)構造体。

*ResponseBuffer*   
一般的なトランスポート コマンドの結果。 ミニポート ドライバーには、この情報が返されます、 **ResponseBuffer**のメンバー、 [ **SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565413)構造体。

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

[**SendCTPassThru\_IN**](https://msdn.microsoft.com/library/windows/hardware/ff565412)

[**SendCTPassThru\_アウト**](https://msdn.microsoft.com/library/windows/hardware/ff565413)

 

 






