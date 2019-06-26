---
title: RxAssert ルーチン
description: インストールされている場合、カーネル デバッガーに RDBSS のチェックで、ASSERT 文字列ビルド RxAssert を送信します。 RDBSS の製品版ビルドでこのルーチンの呼び出しはチェックをバグします。
ms.assetid: 3ef01569-74ef-4f35-acaf-9c01f2b9d9a7
keywords:
- RxAssert ルーチン インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: 4acca9a3a22ba85bcfd529a8555f8eec4e0adbf0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385031"
---
# <a name="rxassert-routine"></a>RxAssert ルーチン


**RxAssert**がインストールされている場合、カーネル デバッガーに RDBSS のサブタイプでアサート文字列を送信します。 RDBSS の製品版ビルドでこのルーチンの呼び出しはチェックをバグします。

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

*FailedAssertion* \[で\]  
失敗したアサーションです。

*FileName* \[in\]  
ファイル ソースの名前を where **RxAssert**または**RtlAssert**が呼び出されました。

*LineNumber* \[で\]  
ソース内の行番号ファイル**RxAssert**または**RtlAssert**が呼び出されました。

*メッセージ*\[で、省略可能\]  
オプションのメッセージ。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

ときに、 *rxassert.h*含めるファイルを使用するもこの RxAssert ルーチンを呼び出す RtlAssert を呼び出す Windows カーネルを再定義されます。

製品版ビルドで**RxAssert**が呼び出す**KeBugCheckEx** 0xa55a0000 値を渡して BugCheckParamater1 と行番号の論理和。

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


[**アサート**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))

[RtlAssert](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**RxDbgBreakPoint**](rxdbgbreakpoint.md)

 

 






