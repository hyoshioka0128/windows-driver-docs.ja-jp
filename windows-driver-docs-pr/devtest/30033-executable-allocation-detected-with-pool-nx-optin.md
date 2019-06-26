---
title: C30033
description: POOL_NX_OPTIN でコンパイルされたドライバーで C30033 実行可能ファイルの割り当ての警告が検出されました。
ms.assetid: A5212960-F33D-485A-9B80-23F3D95D475C
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30033
ms.openlocfilehash: 7f0732574c5ee1adff1e651883695b83f437b93d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371462"
---
# <a name="c30033"></a>C30033


C30033 を警告します。コンパイルされたドライバーの実行可能ファイルの割り当てが見つかりました[プール\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)します。 別のドライバーでの実行時に読み込まれるドライバーと判断されました。 読み込みのドライバーを呼び出すことを確認してください**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** その DriverEntry でします。

禁止\_MEM\_割り当て\_かもしれません\_UNSAFE\_ドライバー\_LOADED

別のドライバーが読み込まれ、そのため、完全な初期化関数はありませんが DLL であると判断されました。 読み込みのドライバーを確認します。

-   使用してコンパイル[プール\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)= 1
-   呼び出し**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** でその初期化関数

読み込みのドライバーを指定しますこれら正常、警告を無視できます。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


DLL のすべてのローダーでは、次のコードの意味 (次の安全な例) に従って変更をする必要があります。

ソース ファイル

```
C_DEFINES=$(C_DEFINES)
```

**DriverEntry**、すべてのメモリ割り当てが行われる前に。

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;
…
    // No call to ExInitializeDriverRuntime
    return(status)
}
```

DLL のすべてのローダーでは、次のコードでは、警告を無視できることを意味します。

ソース ファイルで次のように追加します。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

**DriverEntry**、すべてのメモリ割り当てが行われる前に。

```
NTSTATUS
DriverEntry (
    _In_ PDRIVER_OBJECT DriverObject,
    _In_ PUNICODE_STRING RegistryPath
    )
{
    NTSTATUS status;

    ExInitializeDriverRuntime( DrvRtPoolNxOptIn );
…
```

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例


これを解決する 2 番目の方法は、非実行可能メモリを明示的に参照するすべての呼び出しを行うには。

次のコードでは、この警告を生成します。

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

次のコードは、この警告を回避できます。

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

 

 





