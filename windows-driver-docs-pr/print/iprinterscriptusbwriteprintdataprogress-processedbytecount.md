---
title: IPrinterScriptUsbWritePrintDataProgress ProcessedByteCount メソッド
description: IHV JavaScript 関数は、このメソッドが呼び出された時点で処理されたバイト数を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 667DDBEA-14DA-4037-98A1-A2E7DB8B97F5
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
ms.openlocfilehash: b3a276a90a21561270cd5a3511376aff08f865ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548897"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method"></a>IPrinterScriptUsbWritePrintDataProgress::ProcessedByteCount メソッド

IHV JavaScript 関数は、このメソッドが呼び出された時点で処理されたバイト数を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcessedByteCount(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
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
