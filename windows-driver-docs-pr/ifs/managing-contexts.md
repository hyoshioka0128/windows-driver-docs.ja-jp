---
title: コンテキストの管理
description: コンテキストの管理
ms.assetid: 1ad33c6c-a5dd-4b65-bfcc-a40453d3a6b5
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、コンテキスト
- ファイル システム ミニフィルター ドライバー WDK、コンテキスト
- ミニフィルター ドライバー WDK、コンテキスト
- コンテキスト WDK ファイル システム ミニフィルター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d068cb31d80a16df8c9049b6b632b3ad0752ff2e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375977"
---
# <a name="managing-contexts"></a>コンテキストの管理


フィルター manager は、I/O 操作間で状態を保持するオブジェクトとコンテキストを関連付けるミニフィルター ドライバーを使用できます。 コンテキストを保持できるオブジェクトには、ボリューム、インスタンス、ストリーム、およびストリームのハンドルが含まれます。

サード パーティ製のファイル システムを使用する必要があります、 [ **FSRTL\_詳細\_FCB\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造 (の代わりに、 [ **FSRTL\_一般的な\_FCB\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_common_fcb_header)構造) で正しく動作するストリームおよびストリーム コンテキストを処理します。

コンテキストは、非ページ プールから割り当てる必要があるボリュームのコンテキスト以外のページまたは非ページ プールから割り当てられていることができます。

コンテキストは、すべての未解決の参照が解放されたときに自動的に解放されます。 ミニフィルター ドライバーには、コンテキストのクリーンアップ コールバック ルーチンが定義されている場合、フィルター マネージャーは、コンテキストを解放する前に、ルーチンを呼び出します。

ミニフィルター ドライバーが読み込まれると、インスタンスがデタッチされると、関連付けられたオブジェクトが削除されたときにコンテキストを削除するフィルター マネージャーによって行われます。

ミニフィルター ドライバーでは、ボリュームごとに 1 つだけインスタンスをサポートする場合は、パフォーマンス向上のためのボリュームのコンテキストではなく、インスタンス コンテキストを使用します。 ストリーム内でミニフィルター ドライバー インスタンス コンテキストまたはストリームのハンドル コンテキストへのポインターを格納することによってもパフォーマンスを向上できます。

ページング ファイル、または、次の操作中に、コンテキストはサポートされていません。

-   Preoperation 作成要求の処理

-   Postoperation の処理が要求を閉じる

-   IRP の処理\_MJ\_ネットワーク\_クエリ\_オープン要求

コンテキストを使用するミニフィルター ドライバーの例については、CTX サンプルを参照してください。

### <a name="span-idfiltermanagerroutinesforcontextmanagementspanspan-idfiltermanagerroutinesforcontextmanagementspanspan-idfiltermanagerroutinesforcontextmanagementspanfilter-manager-routines-for-context-management"></a><span id="Filter_Manager_Routines_for_Context_Management"></span><span id="filter_manager_routines_for_context_management"></span><span id="FILTER_MANAGER_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>コンテキスト管理用フィルター マネージャー ルーチン

フィルター マネージャーでは、作成、登録、およびコンテキストの設定の次のサポート ルーチンを提供します。

[**FltAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecontext)

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltSetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinstancecontext)

[**FltSetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetstreamcontext)

[**FltSetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetstreamhandlecontext)

[**FltSetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetvolumecontext)

次のルーチンは、コンテキストのサポートを照会するために用意されています。

[**FltSupportsStreamContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)

[**FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)

取得して、コンテキストを参照するのには、次のルーチンが用意されています。

[**FltGetContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetcontexts)

[**FltGetInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetinstancecontext)

[**FltGetStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamcontext)

[**FltGetStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetstreamhandlecontext)

[**FltGetVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltgetvolumecontext)

[**FltReferenceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreferencecontext)

解放し、コンテキストを削除するのには、次のルーチンが用意されています。

[**FltDeleteContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletecontext)

[**FltDeleteInstanceContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeleteinstancecontext)

[**FltDeleteStreamContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamcontext)

[**FltDeleteStreamHandleContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletestreamhandlecontext)

[**FltDeleteVolumeContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeletevolumecontext)

[**FltReleaseContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontext)

[**FltReleaseContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreleasecontexts)

### <a name="span-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanspan-idminifilterdrivercallbackroutinesforcontextmanagementspanminifilter-driver-callback-routines-for-context-management"></a><span id="Minifilter_Driver_Callback_Routines_for_Context_Management"></span><span id="minifilter_driver_callback_routines_for_context_management"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_CONTEXT_MANAGEMENT"></span>コンテキスト管理に対してミニフィルター ドライバー コールバック ルーチン

次のコールバック ルーチンが格納されている、 [ **FLT\_登録**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_registration)構造体へのパラメーターとして渡される[ **FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltregisterfilter)ミニフィルター ドライバーのコンテキストを管理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">コールバック ルーチンの名前</th>
<th align="left">コールバック ルーチンの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ContextAllocateCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_allocate_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_ALLOCATE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_allocate_callback)"><strong>PFLT_CONTEXT_ALLOCATE_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><em>ContextCleanupCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_CLEANUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)"><strong>PFLT_CONTEXT_CLEANUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>ContextFreeCallback</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_free_callback" data-raw-source="[&lt;strong&gt;PFLT_CONTEXT_FREE_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_context_free_callback)"><strong>PFLT_CONTEXT_FREE_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




