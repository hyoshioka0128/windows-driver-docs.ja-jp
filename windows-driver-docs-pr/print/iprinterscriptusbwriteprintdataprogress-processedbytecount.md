---
title: Iprint Scriptusbwriteprintdataprogress ProcessedByteCount メソッド (out)
description: このメソッドが呼び出されたときに IHV JavaScript 関数が処理したバイト数を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 667DDBEA-14DA-4037-98A1-A2E7DB8B97F5
keywords:
- ProcessedByteCount メソッドの印刷デバイス
- ProcessedByteCount メソッドの印刷デバイス、Iprint Scriptusbwriteprintdataprogress インターフェイス
- Iプリンター Scriptusbwriteprintdataprogress インターフェイスの印刷デバイス、ProcessedByteCount メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbWritePrintDataProgress.ProcessedByteCount
api_type:
- COM
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 73ebb2f33889462eb5537c741e235923c4fe792e
ms.sourcegitcommit: c2c99017178160988aa0e9a861ac347a11cda12a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092467"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method-out"></a>Iプリンター Scriptusbwriteprintdataprogress::P rocessedByteCount メソッド (out)

このメソッドが呼び出されたときに IHV JavaScript 関数が処理したバイト数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT ProcessedByteCount(
  [out, retval] UINT32 *value
);
```

## <a name="parameters"></a>パラメーター

*値* \[out、retval\]  
このメソッドが呼び出されたときに処理されたバイト数。

## <a name="return-value"></a>戻り値

このメソッドは、 **HRESULT**値を返します。

## <a name="requirements"></a>必要条件

**サポートされている最低限のクライアント:** Windows 8.1

**サポートされる最小サーバー:** Windows Server 2012 R2

**ターゲットプラットフォーム:** デスクトップ

## <a name="see-also"></a>関連項目

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
