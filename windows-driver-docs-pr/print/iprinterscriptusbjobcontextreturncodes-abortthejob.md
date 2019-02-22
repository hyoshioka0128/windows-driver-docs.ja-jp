---
title: IPrinterScriptUsbJobContextReturnCodes AbortTheJob メソッド
description: 印刷ジョブを中止する必要がある USBMon に通知するには、'4' の値を返します。
MSHAttr:
- PreferredSiteName:MSDN
- PreferredLib:/library/windows/hardware
ms.assetid: 6E56330E-BDD9-4EDC-A006-CA1D8A58DE32
keywords:
- 印刷デバイスの AbortTheJob メソッド
- AbortTheJob メソッド、印刷デバイス IPrinterScriptUsbJobContextReturnCodes インターフェイス
- IPrinterScriptUsbJobContextReturnCodes インターフェイス、印刷デバイス AbortTheJob メソッド
topic_type:
- apiref
api_name:
- IPrinterScriptUsbJobContextReturnCodes.AbortTheJob
api_type:
- COM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 873a13cc76aad4a0e4723eb47d5ab3d9e515bb32
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557657"
---
# <a name="iprinterscriptusbjobcontextreturncodesabortthejob-method"></a>IPrinterScriptUsbJobContextReturnCodes::AbortTheJob メソッド

印刷ジョブを中止する必要がある USBMon に通知するには、'4' の値を返します。

<a name="syntax"></a>構文
------

```cpp
HRESULT AbortTheJob(
  [out, retval] UINT32 *value
);
```

<a name="parameters"></a>パラメーター
----------

*値* \[out, retval\]  
印刷ジョブを中止する必要があるかを示す値。

<a name="return-value"></a>戻り値
------------

このメソッドが戻る、 **HRESULT**値。

<a name="remarks"></a>注釈
-------

**AbortTheJob**は読み取り専用のメソッドです。 このリターン コード、IHV JavaScript 関数からは、いずれか、デバイスは、ジョブの処理を続行できませんでしたか、ユーザー、デバイスの前面パネルでジョブが取り消されました USBMon を通知します。 USBMon では、印刷ジョブを中止するメッセージを受信したときに、印刷スプーラーを返す前に、ジョブを中止する情報を渡します。

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
