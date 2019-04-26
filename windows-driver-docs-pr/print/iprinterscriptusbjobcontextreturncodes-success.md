---
title: IPrinterScriptUsbJobContextReturnCodes 成功メソッド
description: 関数呼び出しが正常に完了した USBMon を通知するためにゼロ (0) の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 783F9BCA-468E-4505-A6F3-9592D400E62C
keywords:
- 印刷デバイスの成功メソッド
- 成功のメソッド、印刷デバイス IPrinterScriptUsbJobContextReturnCodes インターフェイス
- IPrinterScriptUsbJobContextReturnCodes インターフェイス、印刷デバイス成功メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Success
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abb415848c70a67db17c5c1163a9e3630839edf8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349226"
---
# <a name="iprinterscriptusbjobcontextreturncodessuccess-method"></a>IPrinterScriptUsbJobContextReturnCodes::Success メソッド

関数呼び出しが正常に完了した USBMon を通知するためにゼロ (0) の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Success(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
成功したメソッドの呼び出しを示す値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**成功**は読み取り専用のメソッドです。

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
