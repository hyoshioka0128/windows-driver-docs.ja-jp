---
title: IPrinterScriptUsbJobContextReturnCodes 再試行メソッド
description: USBMon メソッドの呼び出しより多くの作業が完了すると、成功したことを通知するには、'2' の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 1EDF5EFA-1158-4BC7-99AB-3811E4443E62
keywords:
- 印刷デバイスのメソッドを再試行してください。
- 印刷デバイス、IPrinterScriptUsbJobContextReturnCodes インターフェイスのメソッドを再試行してください。
- IPrinterScriptUsbJobContextReturnCodes は、再試行メソッドが、印刷デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Retry
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 436e2b14d2e82fb2208e9dd6bbe81344b61535f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349216"
---
# <a name="iprinterscriptusbjobcontextreturncodesretry-method"></a>IPrinterScriptUsbJobContextReturnCodes::Retry メソッド

USBMon メソッドの呼び出しより多くの作業が完了すると、成功したことを通知するには、'2' の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Retry(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
複数の操作を完了すると、成功したメソッドの呼び出しを示す値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**再試行**は読み取り専用のメソッドです。 USBMon が printerBidiSchemaResponses オブジェクト (Bidi イベントを含む) 任意の Bidi スキーマの更新を処理する必要がありますを呼び出して、**再試行**IHV コードが、データの処理を続行できるようにするには、もう一度メソッド。 印刷データ ストリーム (printData) から処理されるバイト数が、印刷ジョブに関連付けられている writePrintDataProgress オブジェクトで返されます。

<a name="requirements"></a>必要条件
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
