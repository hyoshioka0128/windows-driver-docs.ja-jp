---
title: C30035
description: 警告 C30035 (たとえば、DriverEntry() または DllInitialize()) 初期化関数内から行う必要がある関数が呼び出されました。 PREfast は、初期化関数の呼び出しを行ったかどうかを判断できませんでした。
ms.assetid: 1A5F97EA-7DDC-4D3A-8058-B9C0C2211DA9
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30035
ms.openlocfilehash: 0ece0218f32a0e1e11dcaeae6f7055bce797890a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538320"
---
# <a name="c30035"></a>C30035


C30035 を警告します。初期化関数内から行う必要がある関数が呼び出されました (たとえば、 **DriverEntry()** または**DllInitialize()**)。 PREfast は、初期化関数の呼び出しを行ったかどうかを判断できませんでした。

禁止\_MEM\_割り当て\_かもしれません\_不適切な\_呼び出す\_サイト

コンパイルされたコード、[プール\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)マクロが、初期化の内部で発生しなかった**DriverEntry()** または**DllInitialize()**. この問題を解決するには、初期化関数の内部呼び出しを移動します。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


次のコードでは、この警告を生成します。

ソース ファイル。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    MakeSafeInitialization ();
…
}

void MakeSafeInitialization()
{
    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
}
```

次のコードは、この警告を回避できます。

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
…
}
```

 

 





