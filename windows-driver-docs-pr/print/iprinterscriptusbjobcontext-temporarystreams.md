---
title: IPrinterScriptUsbJobContext TemporaryStreams メソッド
description: 現在のジョブの IHV JavaScript 関数で使用できる永続的なデータ ストリームの IPrinterScriptableSequentialStream インターフェイスの配列を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: ED9AFB90-287B-4030-AC20-ECCA9841D27E
keywords:
- 印刷デバイスの TemporaryStreams メソッド
- TemporaryStreams メソッド、印刷デバイス IPrinterScriptUsbJobContext インターフェイス
- IPrinterScriptUsbJobContext インターフェイス、印刷デバイス TemporaryStreams メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContext.TemporaryStreams
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1f44c1332415f4cd5ac98d450b87dcec3cdea37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571608"
---
# <a name="iprinterscriptusbjobcontexttemporarystreams-method"></a>IPrinterScriptUsbJobContext::TemporaryStreams メソッド

配列を返します[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)は現在のジョブ、IHV JavaScript 関数で使用できる永続的なデータ ストリームのインターフェイス。

<a name="syntax"></a>構文
------

```cpp
HRESULT TemporaryStreams(
  [out, retval] IDispatch **ppArray
);
```

<a name="parameters"></a>パラメーター
----------

*ppArray* \[out, retval\]  
配列を指すポインター [IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)インターフェイス。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>コメント
-------

**TemporaryStreams**は読み取り専用のメソッドです。 一時ストリームを 2 つの最大値は IHV JavaScript 関数を使用できます。 これらのストリームは現在の印刷ジョブの実行中のみ使用できます。 IHV は、印刷デバイスに送信できる状態にはまだデータを格納するのにこれを使用できます。 それ以降の**writePrintData** JavaScript 関数の呼び出し、これらのストリームは、印刷デバイスに格納されているデータを送信するために使用できます。

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

[IPrinterScriptableSequentialStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/printerextension/nn-printerextension-iprinterscriptablesequentialstream)
