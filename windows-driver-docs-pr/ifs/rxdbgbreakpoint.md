---
title: RxDbgBreakPoint 関数
description: インストールされている場合、RxDbgBreakPoint はカーネル デバッガーを中断します。
ms.assetid: 981256a4-2faf-4f9e-acfc-7488230bb62e
keywords:
- インストール可能なファイル システム ドライバーの RxDbgBreakPoint 関数
topic_type:
- apiref
api_name:
- RxDbgBreakPoint
api_location:
- rxassert.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da46cfe74a64752ecfbc4f6c4d828cd4acca991d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570072"
---
# <a name="rxdbgbreakpoint-function"></a>RxDbgBreakPoint 関数


**RxDbgBreakPoint**がインストールされている場合は、カーネル デバッガーを中断します。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID RxDbgBreakPoint(
   ULONG LineNumber
);
```

<a name="parameters"></a>パラメーター
----------

*LineNumber*   
ソース内の行番号ファイル**RxDbgBreakPoint**が呼び出されました。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>コメント
-------

このルーチンは、カーネルを呼び出す**DbgBreakPoint**ルーチン。

このルーチンは、インストールされている場合は、カーネル デバッガーによって処理される例外を発生させます。それ以外の場合、デバッグ システムによって処理されます。 システムにデバッガーが接続されていない場合は、標準的な方法で、例外を処理することができます。

カーネル モードでは、結果としてブルー スクリーン (バグ チェック) が処理されていない中断例外になります。 ただし、カーネル デバッグを有効にするターゲット コンピューターに、カーネル モードのデバッガーを接続ことができます。 詳細については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>対象プラットフォーム</p></td>
<td align="left">Desktop</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Rxassert.h (Rxassert.h を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**RxAssert**](rxassert.md)

[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)

 

 






