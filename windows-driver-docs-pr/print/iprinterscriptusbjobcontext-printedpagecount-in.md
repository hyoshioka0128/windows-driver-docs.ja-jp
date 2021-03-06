---
title: IPrinterScriptUsbJobContext PrintedPageCount メソッド
description: 現在のジョブで印刷デバイスによって印刷されたページ数を設定します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 3C1DAE22-F1DF-48AE-A6F6-CCB8A97EB424
keywords:
- 印刷デバイスの PrintedPageCount メソッド
- PrintedPageCount メソッド、印刷デバイス IPrinterScriptUsbJobContext インターフェイス
- IPrinterScriptUsbJobContext インターフェイス、印刷デバイス PrintedPageCount メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.PrintedPageCount
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d57fc1464cc39e4137bcd5665df41b903476ec6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349241"
---
# <a name="iprinterscriptusbjobcontextprintedpagecount-method"></a>IPrinterScriptUsbJobContext::PrintedPageCount メソッド

現在のジョブで印刷デバイスによって印刷されたページ数を設定します。

<a name="syntax"></a>構文
------

```cpp
HRESULT PrintedPageCount(
  [in] UINT32 value
);
```

<a name="parameters"></a>パラメーター
----------

*value* \[in\]  
現在のジョブで印刷デバイスによって印刷されたページ数。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**PrintedPageCount**は読み取り/書き込みの方法です。 IHV JavaScript **writeData**関数が印刷されたページ数最新に保つため、ジョブの進行状況が正しくを設定する USBMon を許可します。

IHV JavaScript コードを呼び出すことはない場合**PrintedPageCount**印刷されたページ数を設定することが前提とページ数が正確にことはできません、USBMon、スプーラーの進行状況の推定を続行できるようになります。

USBMon と USB ベースの双方向については、印刷デバイスとの通信を参照してください[USB Bidi エクステンダー](https://docs.microsoft.com/windows-hardware/drivers/print/usb-bidi-extender)します。

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

[**IPrinterScriptUsbJobContext**](iprinterscriptusbjobcontext.md)

[USB Bidi エクステンダー](https://docs.microsoft.com/windows-hardware/drivers/print/usb-bidi-extender)
