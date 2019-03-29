---
title: C30031
description: C30031 メモリ割り当て関数を呼び出すことを警告し、実行可能なメモリを示すパラメーターを渡します。
ms.assetid: 5DBC7AC3-30CA-4BD4-BBCB-2275033FF505
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30031
ms.openlocfilehash: 5c0d38c2ba2d317f2c1f44d8dc51707cee8b5ec8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579621"
---
# <a name="c30031"></a>C30031


C30031 を警告します。メモリ割り当て関数を呼び出すと、実行可能なメモリを示すパラメーターを渡す

コード分析の使用を検出しました[プール\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)と**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** 前に呼び出されますが、関数のエントリ (たとえば、 **DriverEntry()** または**DllInitialize()**)。 あるエントリの関数を間接的に呼び出すことは**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)**、エラーを抑制する場合 (を参照してください[を抑制するプラグマ Prefast警告メッセージ](https://msdn.microsoft.com/library/gg155764.aspx))。

禁止\_MEM\_割り当て\_かもしれません\_セーフ

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


ソース ファイルで次のコードでは、この警告が生成されます。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

コード ファイル

```
void MakeSafeInitialization()
{
    ExInitializeDriverRuntime(DrvRtPoolNxOptIn);
}

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

 

 





