---
title: HRESULT の値
description: 次に示すのは、関数とメソッドの一般的な戻り値の一覧と、通常の意味です。
ms.assetid: 713f3ee2-2f5b-415e-9908-90f5ae428b43
ms.date: 12/07/2017
keywords:
- HRESULT 値 Windows デバッグ
topic_type:
- apiref
api_name:
- HRESULT Values
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: b20726a1d9d65d37cc890337ceb3b12b898b741c
ms.sourcegitcommit: 329eee396e727bbd1b2a096a5c7bb0c4b78f52e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/10/2020
ms.locfileid: "81007810"
---
# <a name="hresult-values"></a>HRESULT の値


次に示すのは、関数とメソッドの一般的な戻り値の一覧と、通常の意味です。

## <span id="ddk_return_values_dbx"></span><span id="DDK_RETURN_VALUES_DBX"></span>


**成功した結果。** これらの値は、Winerror.h で定義されています。

<span id="S_OK"></span><span id="s_ok"></span>\_OK  
正常に完了しました。

<span id="S_FALSE"></span><span id="s_false"></span>S\_FALSE  
エラーなしで完了しましたが、結果は部分的にしか取得されませんでした。

バッファーが、返された情報を格納するのに十分な大きさではない場合、多くの場合、返された情報はバッファーに格納されるように切り捨てられ、S\_FALSE がメソッドから返されます。

**エラーの結果。** これらの値は、Winerror.h で定義されています。

<span id="E_FAIL"></span><span id="e_fail"></span>E\_失敗  
操作を実行できませんでした。

<span id="E_INVALIDARG"></span><span id="e_invalidarg"></span>E\_INVALIDARG  
渡された引数の1つが無効です。

<span id="E_NOINTERFACE"></span><span id="e_nointerface"></span>E\_NOINTERFACE  
検索対象のオブジェクトが見つかりませんでした。

<span id="E_OUTOFMEMORY"></span><span id="e_outofmemory"></span>E\_OUTOFMEMORY  
メモリ割り当ての試行に失敗しました。

<span id="E_UNEXPECTED"></span><span id="e_unexpected"></span>予期しない E\_  
ターゲットにアクセスできなかったか、エンジンが関数またはメソッドを処理できた状態ではありませんでした。

<span id="E_NOTIMPL"></span><span id="e_notimpl"></span>E\_NOTIMPL  
実装されていません。

<span id="HRESULT_FROM_WIN32_ERROR_ACCESS_DENIED_"></span><span id="hresult_from_win32_error_access_denied_"></span>\_WIN32 からの HRESULT\_(エラー\_アクセス\_拒否)  
デバッガーが[保護モード](https://docs.microsoft.com/windows-hardware/drivers/debugger/secure-mode)であるため、操作が拒否されました。

**NT エラーの結果。** ステータス\_制御\_C\_終了、状態\_その他の\_エントリがないなど、他のエラーコードが発生する場合があります。\_ これらの結果は、返される前に、Winerror.h で定義されている\_NT マクロから HRESULT\_に渡されます。

**Win32 エラーの結果。** エラー\_READ\_FAULT、ERROR\_WRITE\_FAULT などの他のエラーコードが発生することがあります。 これらの結果は、返される前に、Winerror.h で定義されている\_WIN32 マクロから HRESULT\_に渡されます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>ヘッダー</p></td>
<td align="left">DbgEng .h (DbgEng .h を含む)</td>
</tr>
</tbody>
</table>

 

 





