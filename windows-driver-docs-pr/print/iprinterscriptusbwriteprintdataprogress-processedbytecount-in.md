---
title: Iprint Scriptusbwriteprintdataprogress ProcessedByteCount メソッド ()
description: このメソッドが呼び出されたときに IHV JavaScript 関数が処理したバイト数を設定します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 9E870B80-421B-496A-9510-D97D3A4D7892
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
ms.openlocfilehash: be5165e4be597e67da9cf20183368b4c6dae6090
ms.sourcegitcommit: c2c99017178160988aa0e9a861ac347a11cda12a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092465"
---
# <a name="iprinterscriptusbwriteprintdataprogressprocessedbytecount-method-in"></a>Iプリンター Scriptusbwriteprintdataprogress::P rocessedByteCount メソッド ()

このメソッドが呼び出されたときに IHV JavaScript 関数が処理したバイト数を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT ProcessedByteCount(
  [in]  UINT32 value
);
```

## <a name="parameters"></a>パラメーター

*値* \[から\]  
このメソッドが呼び出されたときに処理されたバイト数。

## <a name="return-values"></a>戻り値

このメソッドは、 **HRESULT**値を返します。

## <a name="requirements"></a>要件

**サポートされている最低限のクライアント:** Windows 8.1

**サポートされる最小サーバー:** Windows Server 2012 R2

**ターゲットプラットフォーム:** デスクトップ

## <a name="see-also"></a>関連項目

[**IPrinterScriptUsbWritePrintDataProgress**](iprinterscriptusbwriteprintdataprogress.md)
