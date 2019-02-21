---
title: IPrinterScriptUsbJobContextReturnCodes DeviceBusy メソッド
description: デバイスの通信チャネルはこの時点でデータを受け付けていませんこと USBMon に通知するには、'3' の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: D1205445-2587-4C9D-B383-587F06A3E899
keywords:
- 印刷デバイスの DeviceBusy メソッド
- DeviceBusy メソッド、印刷デバイス IPrinterScriptUsbJobContextReturnCodes インターフェイス
- IPrinterScriptUsbJobContextReturnCodes インターフェイス、印刷デバイス DeviceBusy メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.DeviceBusy
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437e48ed6f6a274b92751d32f40d2cb58580835c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535434"
---
# <a name="iprinterscriptusbjobcontextreturncodesdevicebusy-method"></a>IPrinterScriptUsbJobContextReturnCodes::DeviceBusy メソッド

デバイスの通信チャネルはこの時点でデータを受け付けていませんこと USBMon に通知するには、'3' の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT DeviceBusy(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
通信チャネルはこの時点でデータを受け付けていませんことを示す値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**DeviceBusy**は読み取り専用のメソッドです。 '3' の戻り値は、障害を示していませんし、USBMon は、印刷スプーラーを通知する必要があります、デバイスがビジー状態であります。 USBMon は、後でもう一度、関数を呼び出すことができます。 WritePrintDataProgress オブジェクトでは、印刷データ ストリーム (printData) から処理されるバイト数が返されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>サポートされている最小のクライアント</p></td>
<td><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td><p>サポートされている最小のサーバー</p></td>
<td><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p>対象プラットフォーム</p></td>
<td>Desktop</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IPrinterScriptUsbJobContextReturnCodes**](iprinterscriptusbjobcontextreturncodes.md)
