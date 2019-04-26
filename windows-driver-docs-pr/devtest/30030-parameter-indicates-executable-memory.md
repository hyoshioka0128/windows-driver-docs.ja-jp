---
title: C30030
description: C30030 メモリ割り当て関数を呼び出すことを警告し、実行可能なメモリを示すパラメーターを渡します。
ms.assetid: D1C8B316-DC04-4B18-A0EB-40833D50B843
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30030
ms.openlocfilehash: b5542a3de5f333824c20d9f2588b5668b3861d66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347064"
---
# <a name="c30030"></a>C30030


C30030 を警告します。メモリ割り当て関数を呼び出すと、実行可能なメモリを示すパラメーターを渡す

禁止\_MEM\_割り当て\_UNSAFE

一部の Api では、メモリが実行可能かどうかを構成するパラメーターがあります。 このエラーは、パラメーターを使用する実行可能 NonPagedPool で結果が割り当てられていることを示します。 使用可能なオプションのいずれかを使用して、非実行可能ファイルのメモリを要求する必要があります。

## <a name="span-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanspan-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanspan-idfordefectsinvolvingtheparametertypesmmpagepriorityandpooltypespanfor-defects-involving-the-parameter-types-mmpagepriority-and-pooltype"></a><span id="For_defects_involving_the_parameter_types_MM_PAGE_PRIORITY_and_POOL_TYPE"></span><span id="for_defects_involving_the_parameter_types_mm_page_priority_and_pool_type"></span><span id="FOR_DEFECTS_INVOLVING_THE_PARAMETER_TYPES_MM_PAGE_PRIORITY_AND_POOL_TYPE"></span>パラメーターの型に関連する障害の検出**MM\_ページ\_優先度**と**プール\_型**


次のいずれかのオプションを使用します。

-   プリプロセッサの定義を指定[プール\_NX\_OPTIN\_自動](https://msdn.microsoft.com/library/windows/hardware/hh920390)ソース/プロジェクトの設定にします。
-   プリプロセッサの定義を指定[プール\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)ソース/プロジェクトの設定と呼び出しで**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)** ドライバーの初期化関数から (**DriverEntry**または**DllInitialize**)。

**注**を使用するかどうかを選択した[プール\_NX\_OPTIN\_自動](https://msdn.microsoft.com/library/windows/hardware/hh920390)または[プール\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)大きく左右作成する方法の多くのバイナリを対象とするプラットフォームで。 両方のオプションと、これらの 2 種類に変更されますが (コンパイラ、または実行時に)、NX 対応します。 詳細についてはトピックのリンクを参照してください。



**注**次の条件のいずれかが true の場合は、false 正警告を表示可能性があります。
-   ドライバーの初期化関数を呼び出す別の関数を呼び出す**ExInitializeDriverRuntime (*DrvRtPoolNxOptIn*)**
-   作成して、**ドライバー\_ライブラリ**し、指定した[プール\_NX\_OPTIN](https://msdn.microsoft.com/library/windows/hardware/hh920402)初期化関数はありません。



-   非実行可能ファイルの種類に割り当ての種類を変更します。

**例 (プール\_NX\_OPTIN\_自動)。**

ソース ファイルで次の設定は警告を許可する、実行可能ファイルのパラメーターを指定する必要があります、API 呼び出しで。

```
C_DEFINES=$(C_DEFINES)
```

ソース ファイルで次の設定は、警告を回避できます。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1
```

**例 (プール\_NX\_OPTIN)。**

ソース ファイルで次のコードでは、警告が生成されます。

```
C_DEFINES=$(C_DEFINES)
```

ソース ファイルで次のコードは、警告を回避できます。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

**DriverEntry()**、すべてのメモリ割り当てが行われる前に。

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

**例 (割り当ての種類の変更):**

**MM\_ページ\_優先度**型を追加することでこれを修正することができます、 **MdlMappingNoExecute**フラグを優先順位の種類。 これは、Windows 8 以降でのみサポートします。

次のコードでは、警告が生成されます。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

次のコードは、警告を回避できます。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority | MdlMappingNoExecute);
```

**例 (プール\_型)**

**プール\_型**型の型の非実行可能ファイルのバージョンを要求の種類を変更することでこれを修正できます。 これは、Windows 8 以降でのみサポートします。

次のコードでは、警告が生成されます。

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

次のコードは、警告を回避できます。

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

**その他の特殊なケース:**

変更があった、 [ **ExInitializeNPagedLookasideList** ](https://msdn.microsoft.com/library/windows/hardware/ff545301)日常的なことになったを使用する非実行可能ファイルの非ページ プール メモリを指定します。 たとえば、次のコードでは、この警告が生成されます。

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                0,
                size,
                tag,
                depth);
```

次のコードは、この警告を回避できます。

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                POOL_NX_ALLOCATION,
                size,
                tag,
                depth);
```

## <a name="span-idfordefectsinvolvingpageprotectionsspanspan-idfordefectsinvolvingpageprotectionsspanspan-idfordefectsinvolvingpageprotectionsspanfor-defects-involving-page-protections"></a><span id="For_defects_involving_page_protections_"></span><span id="for_defects_involving_page_protections_"></span><span id="FOR_DEFECTS_INVOLVING_PAGE_PROTECTIONS_"></span>ページの保護に関連する障害を検出します。


一部の Api では、ページの保護を指定できます。 [ **ZwMapViewOfSection** ](https://msdn.microsoft.com/library/windows/hardware/ff566481)はこれらの 1 つです。 このような場合は、保護の種類の非実行可能ファイルのバージョンを使用します。

［変更］:

-   ページ\_以下の手段、またはページのいずれかに EXECUTE\_NOACCESS
-   ページ\_EXECUTE\_ページへの読み取り\_読み取り専用
-   ページ\_EXECUTE\_ページへの READWRITE\_READWRITE
-   ページ\_EXECUTE\_ページに WRITECOPY\_WRITECOPY

次のコードでは、警告が生成されます。

```
Status = ZwMapViewOfSection(   handle,
                NtCurrentProcess(),
                Address,
                0,
                0,
                &SectionOffset,
                Size,
                ViewUnmap,
                MEM_LARGE_PAGES,
                PAGE_EXECUTE_READWRITE
                ); 
```

次のコードは、この警告を回避できます。

```
Status = ZwMapViewOfSection(   handle,
                NtCurrentProcess(),
                Address,
                0,
                0,
                &SectionOffset,
                Size,
                ViewUnmap,
                MEM_LARGE_PAGES,
                PAGE_READWRITE
                ); 
```

## <a name="span-idfordefectsinvolvingcachetypesspanspan-idfordefectsinvolvingcachetypesspanspan-idfordefectsinvolvingcachetypesspanfor-defects-involving-cache-types"></a><span id="For_defects_involving_cache_types_"></span><span id="for_defects_involving_cache_types_"></span><span id="FOR_DEFECTS_INVOLVING_CACHE_TYPES_"></span>キャッシュの種類に関連する障害を検出します。


一部の Api は、キャッシュの種類に依存する実行可能ファイルのアクセス許可を持つメモリを割り当てます。 このような 2 つの Api は[ **MmAllocateContiguousMemorySpecifyCache** ](https://msdn.microsoft.com/library/windows/hardware/ff554464)と[ **MmAllocateContiguousMemorySpecifyCacheNode**](https://msdn.microsoft.com/library/windows/hardware/ff554469)します。 キャッシュの種類をする必要があります**MmCached**使用 (を参照してください[**メモリ\_CACHING\_型**](https://msdn.microsoft.com/library/windows/hardware/ff554430))、実行可能なメモリが割り当てられます。 これを解決する別のキャッシュの種類を選択またはキャッシュされたメモリが必要な場合は、API を使用して[ **MmAllocateContiguousNodeMemory**](https://msdn.microsoft.com/library/windows/hardware/jj602795)します。

［変更］:

-   **MmCached**に**MmNonCached**または**MmWriteCombined**キャッシュ メモリが必要ない場合
-   API を[ **MmAllocateContiguousNodeMemory** ](https://msdn.microsoft.com/library/windows/hardware/jj602795)キャッシュ メモリが必要な場合

次のコードでは、警告が生成されます。

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              ); 
```

次のコードは、キャッシュされたメモリが必要ない場合、この警告を回避できます。

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmNonCached,
                                              ); 
```

次のコードでは、警告が生成されます。

```
MmAllocateContiguousMemorySpecifyCacheNode(   numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              MM_ANY_NODE_OK
                                              ); 
```

次のコードは、キャッシュされたメモリが必要な場合、この警告を回避できます。

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE,
                                      MM_ANY_NODE_OK
                                      ); 
```

次のコードは、キャッシュされたメモリが必要でない場合、代替 API を使用します。

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE | PAGE_NOCACHE,
                                      MM_ANY_NODE_OK
                                      ); 
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**プール\_型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)










