---
title: ロードとアンロード
description: ロードとアンロード
ms.assetid: e7a4e405-5361-4217-a279-2b54a10ebce2
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター、ドライバーの読み込み/アンロード
- ミニフィルター ドライバー WDK、ドライバーの読み込み
- ファイル システム ミニフィルター ドライバー WDK、ドライバーの読み込み
- ドライバー WDK ファイル システムの読み込み
- ドライバー WDK ファイル システムの読み込み
- アンロード ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ddf6fb60b1bd233fcab4bbbe482919bdec6b13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324405"
---
# <a name="loading-and-unloading"></a>ロードとアンロード


システムの実行中に、いつでもミニフィルター ドライバーを読み込むことができます。 ミニフィルター ドライバーの場合[INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)ドライバー開始サービスの種類を指定します\_ブート\_開始、サービス\_システム\_開始、またはサービス\_自動\_。[スタート]、[ミニフィルター ドライバーがレガシ フィルター ドライバーとの相互運用をサポートするために、ファイル システム フィルター ドライバーの既存のロード順序グループ定義に従って読み込まれます。 サービスの開始要求 (sc start、net の開始、またはサービス Api)、または、明示的な読み込み要求を通じて、システムが実行中にミニフィルター ドライバーを読み込むことができます (fltmc 負荷、 [ **FltLoadFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff543366)、または[ **FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504))。

ミニフィルター ドライバーの[DriverEntry](writing-a-driverentry-routine-for-a-minifilter-driver.md)ルーチンは、そのミニフィルター ドライバーはミニフィルター ドライバーのすべてのインスタンスに適用する初期化を実行できるように、ミニフィルター ドライバーが読み込まれるときに呼び出されます。 内でその**DriverEntry**ミニフィルター ドライバーのルーチンを呼び出す[ **FltRegisterFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544305)フィルター マネージャーとコールバック ルーチンを登録して[**FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)ミニフィルター ドライバーがボリュームへのアタッチと、I/O 要求をフィルター処理を開始する準備がフィルター マネージャーに通知します。

ミニフィルター ドライバーのインスタンスで定義されている、 [INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)ミニフィルター ドライバーをインストールするために使用します。 ミニフィルター ドライバーの INF ファイルで、既定のインスタンスを定義する必要があり、追加のインスタンスを定義できます。 これらの定義は、すべてのボリュームに適用されます。 各インスタンスの定義には、インスタンス名、その高度、およびインスタンスを自動的に、手動で接続できるかどうかを示すフラグまたはその両方が含まれています。 既定のインスタンスは、フィルター マネージャーが正しい順序でミニフィルター ドライバーのマウントおよびインスタンス セットアップ コールバック ルーチンを呼び出す順序ミニフィルター ドライバーに使用されます。 既定のインスタンスは、呼び出し元は、インスタンス名を指定しない場合にも明示的な添付ファイルの要求で使用されます。

フィルター マネージャーは自動的に呼び出すことによって使用可能なボリュームについてミニフィルター ドライバーに通知の[ *InstanceSetupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551096)を最初にルーチンは、ボリュームがマウントされた後に操作を作成します。 これには、発生する前に[ **FltStartFiltering** ](https://msdn.microsoft.com/library/windows/hardware/ff544569)戻り、フィルター マネージャーは、システムの起動時に既存のボリュームを列挙します。 発生実行時にボリュームがマウントされているか、添付ファイルの明示的な要求の結果 (fltmc attach、 [ **FltAttachVolume**](https://msdn.microsoft.com/library/windows/hardware/ff541772)、または[ **FilterAttach**](https://msdn.microsoft.com/library/windows/hardware/ff540442)).

ミニフィルター ドライバーのインスタンスが破棄しているミニフィルター ドライバーが読み込まれるに、インスタンスが接続されているボリュームのマウントされている、または、明示的な接続解除要求の結果 (fltmc デタッチ、 [ **FltDetachVolume**](https://msdn.microsoft.com/library/windows/hardware/ff542041)、または[ **FilterDetach**](https://msdn.microsoft.com/library/windows/hardware/ff540475))。 ミニフィルター ドライバーに登録する場合、 [ *InstanceQueryTeardownCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551095)ルーチンを停止する可能性がデタッチの明示的な要求を呼び出すことによって**FilterDetach**または**FltDetachVolume**します。 破棄は次のように処理されます。

-   ミニフィルター ドライバーに登録されている場合、 [ *InstanceTeardownStartCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551098)コールバック ルーチンでは、フィルター マネージャーを呼び出す、分解プロセスの先頭にします。 ミニフィルター ドライバーが保留中のすべての操作を完了する必要があります、このルーチンで、キャンセルまたは、ミニフィルター ドライバー、および新しい作業項目のキューの停止によって生成される I/O 要求などの他の作業を完了します。

-   通常の処理や postoperation コールバックを「ドレイン」か、取り消されるを待機しているすべての I/O 要求によって生成されたすべての I/O 要求インスタンスの破棄中に、現在実行中の preoperation または postoperation コールバック ルーチンを続行しますミニフィルター ドライバーでは、それらが完了するまでに通常の処理を続行します。

-   ミニフィルター ドライバーに登録されている場合、 [ *InstanceTeardownCompleteCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551098) 、日常的なフィルター マネージャーこのルーチンを呼び出すすべての未処理 I/O 操作が完了した後にします。 このルーチンでは、ミニフィルター ドライバーは、開かれているすべてのファイルを閉じます。

-   結局インスタンスに未解決の参照が解放されます、フィルター マネージャーが残りのコンテキストを削除し、インスタンスが完全に破棄します。

ミニフィルター ドライバーがサービス停止の要求 (sc stop、net stop、またはサービス Api)、または明示的なアンロード要求を通じてアンロードできるシステムの実行中 (fltmc unload、 [ **FltUnloadFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff544602)、または[ **FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516))。

ミニフィルター ドライバーの[ *FilterUnloadCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff551085)ルーチンがミニフィルター ドライバーが読み込まれると呼び出されます。 このルーチンは、オープンなコミュニケーションのサーバー ポートの呼び出しを閉じます[ **FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)、し、必要なクリーンアップを実行します。 このルーチンの登録は、省略可能です。 ただし、ミニフィルター ドライバーが登録していない場合、 *FilterUnloadCallback* 、日常的なミニフィルター ドライバーをアンロードできません。 このルーチンの詳細については、次を参照してください。 [FilterUnloadCallback ルーチンを記述](writing-a-filterunloadcallback-routine.md)します。

### <a name="span-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanspan-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanspan-idfiltermanagerroutinesforloadingandunloadingminifilterdriversspanfilter-manager-routines-for-loading-and-unloading-minifilter-drivers"></a><span id="Filter_Manager_Routines_for_Loading_and_Unloading_Minifilter_Drivers"></span><span id="filter_manager_routines_for_loading_and_unloading_minifilter_drivers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_LOADING_AND_UNLOADING_MINIFILTER_DRIVERS"></span>読み込みとアンロード ミニフィルター ドライバーのフィルター マネージャー ルーチン

フィルター マネージャーは、次の明示的な読み込みルーチンをサポートし、アンロード要求で、ユーザー モードまたはカーネル モードから発行することができますを提供します。

[**FilterLoad**](https://msdn.microsoft.com/library/windows/hardware/ff541504)

[**FilterUnload**](https://msdn.microsoft.com/library/windows/hardware/ff541516)

[**FltLoadFilter**](https://msdn.microsoft.com/library/windows/hardware/ff543366)

[**FltUnloadFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544602)

次のルーチンは、登録およびコールバック ルーチンのセットアップと破棄のインスタンスを登録解除に使用されます。

[**FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305)

[**FltStartFiltering**](https://msdn.microsoft.com/library/windows/hardware/ff544569)

[**FltUnregisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544606)

### <a name="span-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanspan-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanspan-idminifilterdrivercallbackroutinesforinstancesetupteardownandunloadspanminifilter-driver-callback-routines-for-instance-setup-teardown-and-unload"></a><span id="Minifilter_Driver_Callback_Routines_for_Instance_Setup__Teardown__and_Unload"></span><span id="minifilter_driver_callback_routines_for_instance_setup__teardown__and_unload"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_INSTANCE_SETUP__TEARDOWN__AND_UNLOAD"></span>ミニフィルター ドライバー コールバック ルーチンのインスタンスのセットアップ、破棄、およびアンロード

次のミニフィルター ドライバー コールバック ルーチンが格納されている、 [ **FLT\_登録**](https://msdn.microsoft.com/library/windows/hardware/ff544811)構造体へのパラメーターとして渡される[ **FltRegisterFilter**](https://msdn.microsoft.com/library/windows/hardware/ff544305):

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551096" data-raw-source="[&lt;em&gt;InstanceSetupCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551096)"><em>InstanceSetupCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551096" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_SETUP_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551096)"><strong>PFLT_INSTANCE_SETUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551095" data-raw-source="[&lt;em&gt;InstanceQueryTeardownCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551095)"><em>InstanceQueryTeardownCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551095" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551095)"><strong>PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;em&gt;InstanceTeardownStartCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><em>InstanceTeardownStartCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;em&gt;InstanceTeardownCompleteCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><em>InstanceTeardownCompleteCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551098" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551098)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551085" data-raw-source="[&lt;em&gt;FilterUnloadCallback&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551085)"><em>FilterUnloadCallback</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551085" data-raw-source="[&lt;strong&gt;PFLT_FILTER_UNLOAD_CALLBACK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551085)"><strong>PFLT_FILTER_UNLOAD_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




