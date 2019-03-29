---
title: HRESULT の値
description: 次に関数とメソッド、およびその通常の意味に共通の戻り値の一覧を示します。
ms.assetid: 713f3ee2-2f5b-415e-9908-90f5ae428b43
ms.date: 10/30/2017
keywords:
- HRESULT 値の Windows デバッグ
topic_type:
- apiref
api_name:
- HRESULT Values
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 8210a068c972e38ba8d169a21a2a9d55e2dadcf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574802"
---
# <a name="hresult-values"></a>HRESULT の値


次に関数とメソッド、およびその通常の意味に共通の戻り値の一覧を示します。

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**成功した結果。** これらの値は、WinError.h で定義されます。

<span id="S_OK"></span><span id="s_ok"></span>S\_OK  
正常に完了します。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
エラーを発生させずに完了しましたが、のみ部分的な結果が得られました。

返される情報が S、バッファーに収まるように切り捨てられる多くの場合、バッファーに返される情報を保持するのに十分な大きさでない場合\_メソッドから FALSE が返されます。

**エラーが発生します。** これらの値は、WinError.h で定義されます。

<span id="E_FAIL"></span><span id="e_fail"></span>E\_失敗  
操作は実行されませんでした。

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E\_INVALIDARG  
渡された引数のいずれかが無効です。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
検索のオブジェクトが見つかりませんでした。

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E\_OUTOFMEMORY  
メモリ割り当ての試行が失敗しました。

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>E\_予期しません。  
ターゲットがアクセス可能で、または、エンジンは、関数やメソッドを処理ができる状態ではありませんでした。

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E\_NOTIMPL  
実装されていません。

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>HRESULT\_FROM\_WIN32 (エラー\_アクセス\_が拒否されました)  
デバッガーがあるため、操作が拒否された[保護モード](https://msdn.microsoft.com/library/windows/hardware/ff554760)します。

**NT エラーが発生します。** 状態など、他のエラー コード\_コントロール\_C\_終了と状態\_いいえ\_詳細\_エントリが発生する可能性があります。 これらの結果は、HRESULT に渡される\_FROM\_WinError.h で返される前に定義されている NT マクロ。

**Win32 エラーが発生します。** エラーなど、他のエラー コード\_読み取り\_障害ドメインとエラー\_書き込み\_場合があります、障害が発生します。 これらの結果は、HRESULT に渡される\_FROM\_WinError.h で返される前に定義されている WIN32 マクロ。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

 

 





