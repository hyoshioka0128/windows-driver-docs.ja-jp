---
title: IPrinterScriptUsbJobContextReturnCodes Failure メソッド
description: メソッドの呼び出しが失敗した USBMon に通知するには、'1' の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: EEFDB8CA-5B6F-46E5-B181-074354E8B0EE
keywords:
- 印刷デバイスの障害メソッド
- Failure メソッド、印刷デバイス IPrinterScriptUsbJobContextReturnCodes インターフェイス
- IPrinterScriptUsbJobContextReturnCodes インターフェイス、印刷デバイス エラー メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.Failure
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d5eeb76d2e3152c564f23eeec6a370c244d5f00
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349232"
---
# <a name="iprinterscriptusbjobcontextreturncodesfailure-method"></a>IPrinterScriptUsbJobContextReturnCodes::Failure メソッド

メソッドの呼び出しが失敗した USBMon に通知するには、'1' の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT Failure(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
失敗したメソッドの呼び出しを示す値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**エラー**は読み取り専用のメソッドです。 USBMon では、このエラーの値を受信すると、ジョブ コンテキスト オブジェクトをクリーンアップし、印刷スプーラーをエラー コードを返します。

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
