---
title: RxAssert ルーチン
description: RxAssert がインストールされている場合、RDBSS のチェックされたビルドに対してアサート文字列をカーネルデバッガーに送信します。 RDBSS のリテールビルドの場合、このルーチンの呼び出しによってバグチェックが行われます。
ms.assetid: 3ef01569-74ef-4f35-acaf-9c01f2b9d9a7
keywords:
- RxAssert ルーチンのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- RxAssert
api_location:
- rxassert.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7ef93d1ad010614582d93016a5bc2be761f5012
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840976"
---
# <a name="rxassert-routine"></a>RxAssert ルーチン


**RxAssert**がインストールされている場合、RDBSS のチェックされたビルドに対してアサート文字列をカーネルデバッガーに送信します。 RDBSS のリテールビルドの場合、このルーチンの呼び出しによってバグチェックが行われます。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
VOID RxAssert(
  _In_     PVOID FailedAssertion,
  _In_     PVOID FileName,
  _In_     ULONG LineNumber,
  _In_opt_ PCHAR Message
);
```

<a name="parameters"></a>パラメーター
----------

\] の失敗した*アサーション*\[  
失敗したアサーション。

*ファイル名*\[\]  
**RxAssert**または**rtlassert**が呼び出されたソースファイルの名前。

\] の*LineNumber* \[  
**RxAssert**または**rtlassert**が呼び出されたソースファイル内の行番号。

での*メッセージ*\[、オプションの\]  
省略可能なメッセージ。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

*Rxassert*インクルードファイルを使用すると、この rxassert ルーチンも呼び出されるように Windows カーネルの RtlAssert 呼び出しが再定義されます。

リテールビルドでは、 **RxAssert**は、BugCheckParamater1 として行番号を使用して、値0xa55a0000 を渡す**Keバグ checkex**を呼び出します。

<a name="requirements"></a>要件
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
<td align="left">Rxassert (Rxassert を含む)</td>
</tr>
<tr class="odd">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**アサート**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))

[RtlAssert](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**RxDbgBreakPoint**](rxdbgbreakpoint.md)

 

 






