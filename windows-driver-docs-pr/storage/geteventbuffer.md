---
title: GetEventBuffer 関数
description: GetEventBuffer WMI メソッドは、HBA のイベント キュー内の次のイベントを取得します。
ms.assetid: 9eee93e0-2661-4777-8c02-a87c4e1d744c
keywords:
- 記憶装置の GetEventBuffer 関数
topic_type:
- apiref
api_name:
- GetEventBuffer
api_location:
- Hbaapi.lib
- Hbaapi.dll
api_type:
- LibDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f0c7256bdac73282af3c5a2c0a96004b8baf2141
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378552"
---
# <a name="geteventbuffer-function"></a>GetEventBuffer 関数


**GetEventBuffer** WMI メソッドは、HBA のイベント キュー内の次のイベントを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetEventBuffer(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS         HBAStatus,
   [out] uint32                                    EventCount,
   [out, WmiSizeIs("EventCount")] MSFC_EventBuffer Events[]
);
```

<a name="parameters"></a>パラメーター
----------

*HBAStatus*   
に返された場合、操作の状態を示す WMI 修飾子の値を格納します。 使用できる値とその説明の一覧は、次を参照してください。 [HBA\_状態](hba-status.md)します。 ミニポート ドライバーには、この情報が返されます、 **HBAStatus**のメンバー、 [ **GetEventBuffer\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体。

*EventCount*   
返された場合の情報が取得されたイベントの数を示します。 ミニポート ドライバーには、この情報が返されます、**イベント カウント**のメンバー、 [ **GetEventBuffer\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体。

*イベント\[\]*    
型の構造体の配列[ **MSFC\_EventBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer) HBA のイベント キューでは、[次へ] のイベントに関する情報が含まれています。 ミニポート ドライバーには、この情報が返されます、**イベント**のメンバー、 [ **GetEventBuffer\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>注釈
-------

**GetEventBuffer**メソッドは、その情報を取得した後、キューからイベントを削除します。

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


[**GetEventBuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

 

 






