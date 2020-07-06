---
title: PFREE_FUNCTION 関数ポインター
description: PFREE_FUNCTION 型指定されたルーチンは、ファイルシステムのレガシフィルタードライバーによって、フィルターの FreeCallback コールバックルーチンとして登録できます。
ms.assetid: 291b57d9-3bef-4acb-a571-86b67a03cd08
keywords:
- PFREE_FUNCTION 関数ポインターのインストール可能なファイルシステムドライバー
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
ms.openlocfilehash: 94195908ac31592708a3fe61e6fa82b53f1c0dab
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968063"
---
# <a name="pfree_function-function-pointer"></a>PFREE_FUNCTION 関数ポインター

**PFREE_FUNCTION**型指定されたルーチンは、ファイルシステムのレガシフィルタードライバーによって、フィルターの*FreeCallback*コールバックルーチンとして登録できます。 ファイルシステムは、ファイルシステムが[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)を使用してファイルコンテキストオブジェクトを削除するか、 [**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)を使用してストリームコンテキストオブジェクトを削除すると、 *FreeCallback*を呼び出します。

**FREE_FUNCTION**型を使用して、コールバックルーチンを宣言する必要があります。 詳細については、「解説」の例を参照してください。

## <a name="syntax"></a>構文

```ManagedCPlusPlus
typedef VOID ( *FreeCallback)(
  _In_ PVOID Buffer
);
```

## <a name="parameters"></a>パラメーター

*バッファー* \[から\]  
解放する[**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)または[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)構造体へのポインター。

## <a name="return-value"></a>戻り値
------------

なし

## <a name="remarks"></a>解説

ファイルシステムがファイルのファイルコンテキストオブジェクトを破棄すると、 [**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)を呼び出す必要があります。 このルーチンは、ファイルに関連付けられているすべてのファイルごとのコンテキスト構造の*FreeCallback*ルーチンを呼び出します。 このコールバックルーチンは、 [**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)オブジェクトと関連付けられているコンテキスト情報に使用されるメモリを解放する必要があります。 これは、 [**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)が呼び出されたときのストリームコンテキストごとのケースでもあり、 *FreeCallback*は[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)オブジェクトに使用されるメモリを解放します。

*FreeCallback*の呼び出し中に、ファイルコンテキストオブジェクトごと、またはストリームコンテキストオブジェクトごとにアクセスを同期する方法については、 [**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)と[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)を参照してください。

> [!NOTE]
> *FreeCallback*ルーチンは、ファイルシステムに再帰的に呼び出したり、ファイルシステムリソースを取得したりすることはできません。

*Myfreefunction*という名前の*FreeCallback* callback 関数を定義するには、まず、 [Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier) (sdv) およびその他の検証ツールが必要とする関数宣言を次のように指定する必要があります。

```cpp
FREE_FUNCTION MyFreeFunction;
```

次のようにコールバック関数を実装します。

```cpp
VOID
 MyFreeFunction (
 __in PVOID Buffer
    )
  {...}
```

## <a name="requirements"></a>要件

**ターゲットプラットフォーム**: デスクトップ

**バージョン**: windows Vista 以降で使用できます。

**ヘッダー**: Wdm (wdm .h または Ntddk を含む)

**IRQL**: <= APC_LEVEL


## <a name="see-also"></a>関連項目

[**FsRtlTeardownPerFileContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547290)

[**FsRtlTeardownPerStreamContexts**](https://msdn.microsoft.com/library/windows/hardware/ff547295)

[**FSRTL_PER_FILE_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547352)

[**FSRTL_PER_STREAM_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff547357)

[レガシ ファイル システム フィルター ドライバー内のファイル別コンテキストの追跡](https://docs.microsoft.com/windows-hardware/drivers/ifs/tracking-per-file-context-in-a-legacy-file-system-filter-driver)

[レガシ ファイル システム フィルター ドライバー内のストリーム別コンテキストの追跡](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-streams--stream-contexts--and-per-stream-contexts
)
