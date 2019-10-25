---
title: コンテキストの管理
description: コンテキストの管理
ms.assetid: 1ad33c6c-a5dd-4b65-bfcc-a40453d3a6b5
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、コンテキスト
- ファイルシステムミニフィルタードライバー WDK、コンテキスト
- ミニフィルタードライバー WDK、コンテキスト
- コンテキスト WDK ファイルシステムミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdeff72eaa35daca18476289f3e92735c99829ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841131"
---
# <a name="managing-contexts"></a>コンテキストの管理


フィルターマネージャーを使用すると、ミニフィルタードライバーを使用して、i/o 操作間で状態を保持するためにコンテキストをオブジェクトに関連付けることができます。 コンテキストを持つことのできるオブジェクトには、ボリューム、インスタンス、ストリーム、およびストリームハンドルがあります。

サードパーティのファイルシステムでは、 [**FSRTL\_ADVANCED\_fcb\_header**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造体 ( [**FSRTL\_COMMON\_fcb\_header**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_common_fcb_header)構造体ではなく) を使用して、ストリームおよびストリームハンドルコンテキストで適切に動作する必要があります.

コンテキストは、ページングされたプールまたは非ページプールから割り当てることができます。ただし、ボリュームコンテキストは、非ページプールから割り当てる必要があります。

すべての未処理の参照が解放されると、コンテキストは自動的に解放されます。 ミニフィルタードライバーによってコンテキストクリーンアップコールバックルーチンが定義されている場合、コンテキストが解放される前に、フィルターマネージャーがルーチンを呼び出します。

フィルターマネージャーは、関連付けられたオブジェクトが削除されたとき、インスタンスがデタッチされたとき、およびミニフィルタードライバーがアンロードされたときに、コンテキストの削除を行います。

ミニフィルタードライバーが1つのボリュームにつき1つのインスタンスのみをサポートしている場合は、パフォーマンスを向上させるために、ボリュームコンテキストではなくインスタンスコンテキストを使用します。 また、ストリームまたはストリームハンドルコンテキスト内にミニフィルタードライバーインスタンスコンテキストへのポインターを格納することで、パフォーマンスを向上させることもできます。

コンテキストは、ページングファイルまたは次の操作中にはサポートされません。

-   作成要求の事前操作処理

-   クローズ要求の postoperation 処理

-   IRP\_MJ\_ネットワーク\_クエリ\_オープン要求の処理

コンテキストを使用するミニフィルタードライバーの例については、CTX サンプルを参照してください。

### <a name="span-idfilter_manager_routines_for_context_managementspanspan-idfilter_manager_routines_for_context_managementspanspan-idfilter_manager_routines_for_context_managementspanfilter-manager-routines-for-context-management"></a><span id="Filter_Manager_Routines_for_Context_Management"></span><span id="filter_manager_routines_for_context_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>コンテキスト管理のフィルターマネージャールーチン

フィルターマネージャーには、コンテキストを作成、登録、および設定するための次のサポートルーチンが用意されています。

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltSetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinstancecontext)

[**FltSetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamcontext)

[**FltSetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)

[**FltSetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetvolumecontext)

コンテキストサポートをクエリするために、次のルーチンが用意されています。

[**FltSupportsStreamContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)

[**FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

コンテキストを取得および参照するために、次のルーチンが用意されています。

[**FltGetContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetcontexts)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreferencecontext)

コンテキストの解放と削除には、次のルーチンが用意されています。

[**FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletecontext)

[**FltDeleteInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeleteinstancecontext)

[**FltDeleteStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamcontext)

[**FltDeleteStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)

[**FltDeleteVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeletevolumecontext)

[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontext)

[**FltReleaseContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreleasecontexts)

### <a name="span-idminifilter_driver_callback_routines_for_context_managementspanspan-idminifilter_driver_callback_routines_for_context_managementspanspan-idminifilter_driver_callback_routines_for_context_managementspanminifilter-driver-callback-routines-for-context-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Context_Management"></span><span id="minifilter_driver_callback_routines_for_context_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>コンテキスト管理用のミニフィルタードライバーコールバックルーチン

次のコールバックルーチンは、コンテキストを管理するミニフィルタードライバーの[**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡される[**FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体に格納されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバックルーチン名</th>
<th align="left">コールバックルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ContextAllocateCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_ALLOCATE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_allocate_callback)"><strong>PFLT_CONTEXT_ALLOCATE_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_CLEANUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)"><strong>PFLT_CONTEXT_CLEANUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ContextFreeCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_FREE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_free_callback)"><strong>PFLT_CONTEXT_FREE_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




