---
title: Iプリンター Scriptusbjobcontext の一時ストリームメソッド
description: 現在のジョブの IHV JavaScript 関数で使用できる永続データストリームの IPrinterScriptableSequentialStream インターフェイスの配列を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ED9AFB90-287B-4030-AC20-ECCA9841D27E
keywords:
- 一時ストリーム方式の印刷デバイス
- 一時ストリームメソッドの印刷デバイス、Iプリンター Scriptusbjobcontext インターフェイス
- Iプリンター Scriptusbjobcontext インターフェイスの印刷デバイス、一時ストリームメソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.TemporaryStreams
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c596e7c379d77b866b69c234b32da8a442999654
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844327"
---
# <a name="iprinterscriptusbjobcontexttemporarystreams-method"></a>Iプリンター Scriptusbjobcontext:: 一時ストリームメソッド

現在のジョブの IHV JavaScript 関数で使用できる永続データストリームの[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)インターフェイスの配列を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT TemporaryStreams(
  [out, retval] IDispatch **ppArray
);
```

<a name="parameters"></a>パラメーター
----------

*Pparray* \[out、retval\]  
[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)インターフェイスの配列へのポインター。

<a name="return-value"></a>戻り値
------------

このメソッドは、 **HRESULT**値を返します。

<a name="remarks"></a>注釈
-------

**一時ストリーム**は読み取り専用のメソッドです。 IHV JavaScript 関数は、最大2つの一時ストリームを使用できます。 これらのストリームは、現在の印刷ジョブの期間中のみ使用できます。 IHV はこれを使用して、まだ印刷デバイスに送信する準備ができていないデータを格納できます。 後の**Writeprintdata** JavaScript 関数呼び出しでは、これらのストリームを使用して、保存されたデータを印刷デバイスに送信できます。

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

[**Iプリンター Scriptusbjobcontext**](iprinterscriptusbjobcontext.md)

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprinterscriptablesequentialstream)
