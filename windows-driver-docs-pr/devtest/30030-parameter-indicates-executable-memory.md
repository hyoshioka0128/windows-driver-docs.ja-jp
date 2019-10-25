---
title: C30030
description: 警告 C30030 は、メモリの割り当て関数を呼び出し、実行可能メモリを示すパラメーターを渡しています。
ms.assetid: D1C8B316-DC04-4B18-A0EB-40833D50B843
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C30030
ms.openlocfilehash: 7f5128021f75e46114b6209b81e1b80486e7b1a7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840308"
---
# <a name="c30030"></a>C30030


警告 C30030: メモリの割り当て関数を呼び出し、実行可能メモリを示すパラメーターを渡す

禁止\_メモリ\_割り当て\_安全ではありません

一部の Api には、メモリを実行可能にするかどうかを構成するパラメーターがあります。 このエラーは、実行可能ファイル NonPagedPool が割り当てられたパラメーターが使用されていることを示します。 実行可能でないメモリを要求するには、使用可能なオプションのいずれかを使用する必要があります。

## <a name="span-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanspan-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanspan-idfor_defects_involving_the_parameter_types_mm_page_priority_and_pool_typespanfor-defects-involving-the-parameter-types-mm_page_priority-and-pool_type"></a><span id="For_defects_involving_the_parameter_types_MM_PAGE_PRIORITY_and_POOL_TYPE"></span><span id="for_defects_involving_the_parameter_types_mm_page_priority_and_pool_type"></span><span id="FOR_DEFECTS_INVOLVING_THE_PARAMETER_TYPES_MM_PAGE_PRIORITY_AND_POOL_TYPE"></span>パラメーターの種類が**MM\_ページ**に関係する問題については\_優先順位と**プール\_の種類**


次のいずれかのオプションを使用します。

-   ソース/プロジェクトの設定で、[[自動\_]\_OPTIN\_](https://docs.microsoft.com/windows-hardware/drivers/kernel/multiple-binary-opt-in-pool-nx-optin-auto)プリプロセッサ定義プールを指定します。
-   ソース/プロジェクトの設定で[\_NX\_OPTIN](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)のプリプロセッサ定義プールを指定し、ドライバー初期化関数 (**driverentry**またはからの**Exinitializedriverruntime (*DrvRtPoolNxOptIn*)** を呼び出します。**DllInitialize**)。

**メモ** [プール\_nx\_optin\_自動](https://docs.microsoft.com/windows-hardware/drivers/kernel/multiple-binary-opt-in-pool-nx-optin-auto)または\_プールのどちらを使用するかを選択すると、 [nx\_optin](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)は、対象とするプラットフォームと作成するバイナリの数に大きく依存します。 どちらのオプションでも、これらの2つの型は (コンパイラまたは実行時に) それぞれの NX に対応するように変更されます。 詳細については、トピックのリンクを参照してください。



**メモ** 次のいずれかの条件に該当する場合は、偽陽性の警告が表示されることがあります。
-   ドライバー初期化関数は、 **Exinitializedriverruntime (*DrvRtPoolNxOptIn*)** を呼び出す別の関数を呼び出します。
-   **ドライバー\_ライブラリ**を作成していて、指定された[プールに NX\_OPTIN\_](https://docs.microsoft.com/windows-hardware/drivers/kernel/single-binary-opt-in-pool-nx-optin)指定されていますが、初期化関数がありません。



-   割り当ての種類を実行可能ではない型に変更します。

**例 (プール\_NX\_OPTIN\_AUTO):**

ソースファイルの次の設定では、API 呼び出しで実行可能なパラメーターを指定する必要があることを警告します。

```
C_DEFINES=$(C_DEFINES)
```

ソースファイルの次の設定は、警告を回避します。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1
```

**例 (プール\_NX\_OPTIN):**

ソースファイル内の次のコードでは、警告が生成されます。

```
C_DEFINES=$(C_DEFINES)
```

ソースファイル内の次のコードは、警告を回避します。

```
C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN=1
```

**Driverentry ()** で、メモリの割り当てが行われる前に、次のようにします。

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

**例 (割り当ての種類を変更する):**

[ **MM\_] ページ\_priority**の種類では、 **Mdlmappingnoexecute**フラグを優先度の種類に追加することで、この問題を解決できます。 これは、Windows 8 以降でのみサポートされています。

次のコードでは、警告が生成されます。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority);
```

次のコードでは、警告が回避されます。

```
pPtr = MmGetSystemAddressForMdlSafe( pMdl, NormalPagePriority | MdlMappingNoExecute);
```

**例 (プール\_の種類)**

[**プール\_種類**の種類] では、要求の種類を実行可能でないバージョンの型に変更することで、この問題を解決できます。 これは、Windows 8 以降でのみサポートされています。

次のコードでは、警告が生成されます。

```
ExAllocatePoolWithTag(NonPagedPool, numberOfBytes, 'xppn');
```

次のコードでは、警告が回避されます。

```
ExAllocatePoolWithTag(NonPagedPoolNx, numberOfBytes, 'xppn');
```

**その他の特殊なケース:**

[**ExInitializeNPagedLookasideList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializenpagedlookasidelist)ルーチンが変更され、非実行可能な非ページプールメモリを指定できるようになりました。 たとえば、次のコードでは、この警告が生成されます。

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                0,
                size,
                tag,
                depth);
```

次のコードは、この警告を回避します。

```
ExInitializeNPagedLookasideList(pLookaside,
                NULL,
                NULL,
                POOL_NX_ALLOCATION,
                size,
                tag,
                depth);
```

## <a name="span-idfor_defects_involving_page_protections_spanspan-idfor_defects_involving_page_protections_spanspan-idfor_defects_involving_page_protections_spanfor-defects-involving-page-protections"></a><span id="For_defects_involving_page_protections_"></span><span id="for_defects_involving_page_protections_"></span><span id="FOR_DEFECTS_INVOLVING_PAGE_PROTECTIONS_"></span>ページ保護に関する不具合がある場合:


一部の Api では、ページ保護を指定できます。 [**ZwMapViewOfSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmapviewofsection)はこれらのうちの1つです。 このような場合は、保護の種類の実行可能ではないバージョンを使用します。

変更

-   ページ\_、次のいずれかの代替手段またはページ\_NOACCESS に実行されます。
-   ページ\_実行\_読み取り専用\_ページ
-   ページ\_\_readwrite\_の READWRITE に実行
-   ページ\_\_WRITECOPY を実行\_WRITECOPY

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

次のコードは、この警告を回避します。

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

## <a name="span-idfor_defects_involving_cache_types_spanspan-idfor_defects_involving_cache_types_spanspan-idfor_defects_involving_cache_types_spanfor-defects-involving-cache-types"></a><span id="For_defects_involving_cache_types_"></span><span id="for_defects_involving_cache_types_"></span><span id="FOR_DEFECTS_INVOLVING_CACHE_TYPES_"></span>キャッシュの種類に関連する問題の場合:


一部の Api は、キャッシュの種類に依存する実行可能なアクセス許可を使用してメモリを割り当てます。 このような Api には、 [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)と[**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)の2つがあります。 **Mmcached**のキャッシュの種類を使用する必要があります (「[**メモリ\_キャッシュ\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_memory_caching_type)」を参照)。次に、実行可能メモリが割り当てられます。 これを修正するには、別のキャッシュの種類を選択するか、キャッシュされたメモリが必要な場合は API [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)を使用します。

変更

-   キャッシュされたメモリが不要な場合、 **Mmcached**または**Mmwritecombined**にキャッシュされた**mmcached**
-   キャッシュされたメモリが必要な場合に[**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)する API

次のコードでは、警告が生成されます。

```
MmAllocateContiguousMemorySpecifyCache(       numberOfBytes,
                                              lowestAddress,
                                              highestAddress,
                                              NULL,
                                              MmCached,
                                              ); 
```

次のコードは、キャッシュされたメモリが不要な場合にこの警告を回避します。

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

次のコードは、キャッシュされたメモリが必要な場合にこの警告を回避します。

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE,
                                      MM_ANY_NODE_OK
                                      ); 
```

キャッシュされたメモリが不要な場合、次のコードでは代替 API を使用します。

```
MmAllocateContiguousNodeMemory(       numberOfBytes,
                                      lowestAddress,
                                      highestAddress,
                                      NULL,
                                      PAGE_READWRITE | PAGE_NOCACHE,
                                      MM_ANY_NODE_OK
                                      ); 
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連項目


[**プール\_の種類**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)










