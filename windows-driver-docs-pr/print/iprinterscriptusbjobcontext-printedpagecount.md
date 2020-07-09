---
title: Iプリンター Scriptusbjobcontext PrintedPageCount メソッド (out)
description: 現在のジョブの印刷デバイスによって印刷されたページ数を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 5933D374-D134-4731-994A-B16027225CA3
keywords:
- PrintedPageCount メソッドの印刷デバイス
- PrintedPageCount メソッドの印刷デバイス、Iプリンター Scriptusbjobcontext インターフェイス
- Iプリンター Scriptusbjobcontext インターフェイスの印刷デバイス、PrintedPageCount メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.PrintedPageCount
api_type:
- COM
ms.date: 07/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: f9b42aa4aa8dc28af7ef6f6829170521c2643d90
ms.sourcegitcommit: c2c99017178160988aa0e9a861ac347a11cda12a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86092463"
---
# <a name="iprinterscriptusbjobcontextprintedpagecount-method-out"></a>Iプリンター Scriptusbjobcontext::P rintedPageCount メソッド (out)

現在のジョブの印刷デバイスによって印刷されたページ数を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT PrintedPageCount(
  [out, retval] UINT32 *value
);
```

## <a name="parameters"></a>パラメーター

*値* \[out、retval\]  
現在のジョブの印刷デバイスによって印刷されたページ数。

## <a name="return-value"></a>戻り値

このメソッドは、 **HRESULT**値を返します。

## <a name="remarks"></a>解説

**PrintedPageCount**は、読み取り/書き込みメソッドです。 IHV JavaScript **Writedata**関数は、印刷されたページ数を最新の状態に保ち、usbmon がジョブの正しい進行状況を設定できるようにする必要があります。

IHV JavaScript コードが**PrintedPageCount**を呼び出して、印刷されたページ数を設定しない場合は、ページ数が正確ではないと想定されます。また、usbmon では、スプーラーが進行状況の推定を続けることができます。

印刷デバイスとの USBMon と USB ベースの双方向通信の詳細については、「 [USB Bidi Extender](https://docs.microsoft.com/windows-hardware/drivers/print/usb-bidi-extender)」を参照してください。

## <a name="requirements"></a>必要条件

**サポートされている最低限のクライアント:** Windows 8.1

**サポートされる最小サーバー:** Windows Server 2012 R2

**ターゲットプラットフォーム:** デスクトップ

## <a name="see-also"></a>関連項目

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[USB 双方向エクステンダー](https://docs.microsoft.com/windows-hardware/drivers/print/usb-bidi-extender)
