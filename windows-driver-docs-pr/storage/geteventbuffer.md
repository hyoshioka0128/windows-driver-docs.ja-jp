---
title: GetEventBuffer 関数
description: GetEventBuffer WMI メソッドは、HBA のイベントキュー内の次のイベントを取得します。
ms.assetid: 9eee93e0-2661-4777-8c02-a87c4e1d744c
keywords:
- GetEventBuffer 関数のストレージデバイス
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
ms.openlocfilehash: d3cb5e9f1f050baaa8c23b82ad77a2dca8637a28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837967"
---
# <a name="geteventbuffer-function"></a>GetEventBuffer 関数


**Geteventbuffer** WMI メソッドは、HBA のイベントキュー内の次のイベントを取得します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
void GetEventBuffer(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS         HBAStatus,
   [out] uint32                                    EventCount,
   [out, WmiSizeIs("EventCount")] MSFC_EventBuffer Events[]
);
```

<a name="parameters"></a>parameters
----------

*Hbastatus*   
返されるときに、操作の状態を示す WMI 修飾子値を格納します。 許可される値とその説明の一覧については、「 [HBA\_STATUS](hba-status.md)」を参照してください。 ミニポートドライバーは、 [**Geteventbuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体の**hbastatus**メンバーにこの情報を返します。

*Eventcount*   
返されるときに、情報を取得したイベントの数を示します。 ミニポートドライバーは、 [**Geteventbuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体の**eventcount**メンバーにこの情報を返します。

*イベント\[\]*    
HBA イベントキュー内の次のイベントに関する情報を含む[**Msfc\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)型の構造体の配列。 ミニポートドライバーは、 [**Geteventbuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)構造体の**Events**メンバーでこの情報を返します。

<a name="return-value"></a>戻り値
------------

WMI メソッドには適用されません。

<a name="remarks"></a>解説
-------

**Geteventbuffer**メソッドは、情報を取得した後に、キューからイベントを削除します。

この WMI メソッドは、 [Msfc\_HBAAdapterMethods WMI クラス](msfc-hbaadaptermethods-wmi-class.md)に属しています。

<a name="requirements"></a>前提条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ターゲットプラットフォーム</p></td>
<td align="left">デスクトップ</td>
</tr>
<tr class="even">
<td align="left"><p>ヘッダー</p></td>
<td align="left">Hbapiwmi (Hbapiwmi、Hbaapi. h、または Hbaapi .h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>ライブラリ</p></td>
<td align="left">Hbaapi .lib</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**GetEventBuffer\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_geteventbuffer_out)

[**MSFC\_EventBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_eventbuffer)

 

 






