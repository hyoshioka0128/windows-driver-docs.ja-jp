---
title: IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount メソッド
description: IHV JavaScript 関数は、このメソッドが呼び出された時に処理されたバイト数を設定します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9E870B80-421B-496A-9510-D97D3A4D7892
keywords:
- 印刷デバイスの ProcessedByteCount メソッド
- ProcessedByteCount メソッド、印刷デバイス IPrinterScriptUsbWritePrintDataProgress インターフェイス
- IPrinterScriptUsbWritePrintDataProgress インターフェイス、印刷デバイス ProcessedByteCount メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress.ProcessedByteCount
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27d84b37a5863ca6acc3f9a080d94c78795d410f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349206"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method"></a>IPrinterScriptUsbWritePrintDataProgress::ProcessedByteCount メソッド

IHV JavaScript 関数は、このメソッドが呼び出された時に処理されたバイト数を設定します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcessedByteCount(
  [in]  UINT32 value
);
```

<a name="parameters"></a>パラメーター
----------

*value* \[in\]  
このメソッドが呼び出された時点で処理されるバイト数。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

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

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
