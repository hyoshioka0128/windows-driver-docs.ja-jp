---
title: PFREE\_関数の関数ポインター
description: PFREE\_関数の型指定されたルーチンは、フィルターの FreeCallback コールバック ルーチンとしてファイル システムのレガシ フィルター ドライバーを登録できません。
ms.assetid: 291b57d9-3bef-4acb-a571-86b67a03cd08
keywords:
- PFREE_FUNCTION 関数ポインター インストール可能なファイル システム ドライバー
topic_type:
- apiref
api_name:
- FreeCallback
api_location:
- wdm.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1944414572ba8d944743ecbcd9c14feccd774321
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366785"
---
# <a name="pfreefunction-function-pointer"></a>PFREE\_関数の関数ポインター


A **PFREE\_関数**型指定されたルーチンは、フィルターのとしてファイル システムのレガシ フィルター ドライバーを登録できません*FreeCallback*コールバック ルーチン。 ファイル システムの呼び出し*FreeCallback*を使用して、ファイル システムがファイル コンテキスト オブジェクトを削除するときに[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)またはによってストリーム コンテキスト オブジェクトを削除します。使用して[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)します。

使用して、コールバック ルーチンを宣言する必要があります、 **FREE\_関数**型。 詳細については、「解説」セクションの例で、を参照してください。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef VOID ( *FreeCallback)(
  _In_ PVOID Buffer
);
```

<a name="parameters"></a>パラメーター
----------

*バッファー* \[で\]  
ポインター、 [ **FSRTL\_1 秒あたり\_ファイル\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547352)または[ **FSRTL\_1 秒あたり\_ストリーム\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547357)構造体を解放します。

<a name="return-value"></a>戻り値
------------

なし

<a name="remarks"></a>注釈
-------

ファイル システムを廃棄すると、ファイルのファイル コンテキスト オブジェクトごとに呼び出す必要があります[ **FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)します。 このルーチンを呼び出す、 *FreeCallback*ファイルに関連付けられているすべてのファイルごとのコンテキストの構造体のルーチンです。 このコールバック ルーチンの使用されているメモリを解放する必要があります、 [ **FSRTL\_1 秒あたり\_ファイル\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547352)オブジェクト、および関連のコンテキスト情報。 これはストリーム コンテキストごとの場合でもとき[ **FsRtlTeardownPerStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547295)が呼び出されますと*FreeCallback*に使用されるメモリを解放[ **FSRTL\_1 秒あたり\_ストリーム\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff547357)オブジェクト。

コンテキスト オブジェクトはファイルごとまたはあたりの呼び出し中にコンテキスト オブジェクトをストリームするへのアクセスを同期する方法には、「解説」の*FreeCallback*、を参照してください[ **FsRtlTeardownPerFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff547290)と[ **FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)します。

&gt; \[!注\] &gt; 、 *FreeCallback*ルーチンが再帰的に呼び出すことはできません、ファイル システムにダウンするか、ファイル システム リソースを取得します。

 

定義する、 *FreeCallback*という名前のコールバック関数*MyFreeFunction*、最初に指定する必要あります関数の宣言を[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier) (SDV) とその他の検証ツールが必要です、とおり。

```cpp
FREE_FUNCTION MyFreeFunction;
```

次のように、コールバック関数を実装します。

```cpp
VOID 
 MyFreeFunction (
 __in PVOID Buffer
    )
  {...}
```

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
<td align="left"><p>バージョン</p></td>
<td align="left"><p>開始 withWindows Vista を使用できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Wdm.h (Wdm.h または Ntddk.h を含む)</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)

[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)

[**FSRTL\_PER\_FILE\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)

[**FSRTL\_PER\_STREAM\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)

[レガシ ファイル システム フィルター ドライバーのファイルごとのコンテキストの追跡](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-file-context-in-a-legacy-file-system-filter-driver)

[レガシ ファイル システム フィルター ドライバーでの Stream あたりのコンテキストの追跡](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-stream-context-in-a-legacy-file-system-filter-driver)

 

 






