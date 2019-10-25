---
title: ロードとアンロード
description: ロードとアンロード
ms.assetid: e7a4e405-5361-4217-a279-2b54a10ebce2
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、読み込み/アンロードドライバー
- ミニフィルタードライバー WDK、ドライバーの読み込み
- ファイルシステムミニフィルタードライバー WDK、ドライバーの読み込み
- WDK ファイルシステムの読み込み中のドライバー
- ドライバー WDK ファイルシステムを読み込んでいます
- ドライバーのアンロード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 880d54a6d60d73d846e06c5a0b9306024de81aa1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841136"
---
# <a name="loading-and-unloading"></a>ロードとアンロード


ミニフィルタードライバーは、システムの実行中にいつでも読み込むことができます。 ミニフィルタードライバーの[INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)で、起動\_開始、サービス\_システム\_開始、またはサービス\_自動\_開始のドライバーの開始\_の種類が指定されている場合は、既存の負荷に応じてミニフィルタードライバーが読み込まれます。レガシフィルタードライバーとの相互運用性をサポートするために、ファイルシステムフィルタードライバーの順序グループの定義。 システムの実行中は、サービス開始要求 (sc start、net start、または service Api) を介して、または明示的な読み込み要求 (fltmc load、 [**Fltloadfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)、または[**filterload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)) を介してミニフィルタードライバーを読み込むことができます。

ミニフィルタードライバーの[Driverentry](writing-a-driverentry-routine-for-a-minifilter-driver.md)ルーチンはミニフィルタードライバーが読み込まれるときに呼び出されます。そのため、ミニフィルタードライバーは、ミニフィルタードライバーのすべてのインスタンスに適用される初期化を実行できます。 その**Driverentry**ルーチンでは、ミニフィルタドライバーは[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出して、フィルターマネージャーと[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)にコールバックルーチンを登録します。これにより、フィルタマネージャーに対して、ミニフィルタードライバーを開始する準備ができたことが通知されます。ボリュームにアタッチし、i/o 要求をフィルター処理しています。

ミニフィルタードライバーインスタンスは、ミニフィルタードライバーのインストールに使用される[INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)で定義されています。 ミニフィルタードライバーの INF ファイルでは、既定のインスタンスを定義する必要があります。また、追加のインスタンスを定義することもできます。 これらの定義は、すべてのボリュームに適用されます。 各インスタンス定義には、インスタンス名、その高度、インスタンスを自動的に接続できるかどうかを示すフラグ、手動で、またはその両方を含めることができます。 既定のインスタンスは、フィルタマネージャーがミニフィルタードライバーのマウントおよびインスタンスセットアップコールバックルーチンを正しい順序で呼び出すように、ミニフィルタードライバーの順序を設定するために使用されます。 既定のインスタンスは、呼び出し元がインスタンス名を指定していない場合に、明示的な添付ファイル要求でも使用されます。

フィルターマネージャーは、ボリュームがマウントされた後の最初の作成操作で[*Instancesetupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)ルーチンを呼び出すことによって、使用可能なボリュームについてミニフィルタードライバーに自動的に通知します。 これは、フィルターマネージャーがシステムの起動時に既存のボリュームを列挙するときに、 [**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)が戻る前に発生することがあります。 また、実行時に、ボリュームがマウントされたとき、または明示的な添付ファイルの要求 (fltmc attach、 [**Fltattachvolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltattachvolume)、または[**filterattach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)) の結果として発生することもあります。

ミニフィルタードライバーインスタンスは、ミニフィルタードライバーがアンロードされたとき、インスタンスがアタッチされているボリュームがマウント解除されたとき、または明示的なデタッチ要求 (fltmc detach、 [**FltDetachVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdetachvolume)、または[**filterdetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)) の結果として破棄されます。 ミニフィルタードライバーによって[*InstanceQueryTeardownCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)ルーチンが登録されると、 **Filterdetach**または**FltDetachVolume**を呼び出すことによって明示的なデタッチ要求が失敗する可能性があります。 破棄は次のように進行します。

-   ミニフィルタードライバーによって[*InstanceTeardownStartCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)コールバックルーチンが登録されている場合、フィルターマネージャーは破棄プロセスの開始時にそれを呼び出します。 このルーチンでは、ミニフィルタードライバーがすべての保留中の操作を完了するか、ミニフィルタードライバーによって生成された i/o 要求などの他の処理を完了し、新しい作業項目のキューを停止します。

-   インスタンスの破棄中、現在実行中の preoperation または postoperation コールバックルーチンは通常の処理を続行し、postoperation コールバックを待機しているすべての i/o 要求は "ドレイン" またはキャンセルされ、ミニフィルタードライバーは、完了するまで通常の処理を続行します。

-   ミニフィルタードライバーによって[*InstanceTeardownCompleteCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)ルーチンが登録されている場合、未処理の i/o 操作がすべて完了した後に、フィルターマネージャーがこのルーチンを呼び出します。 このルーチンでは、ミニフィルタードライバーによって、開いているファイルがすべて閉じられます。

-   インスタンスへの未処理の参照がすべて解放されると、フィルターマネージャーは残りのコンテキストを削除し、インスタンスは完全に破棄されます。

システムの実行中は、サービス停止要求 (sc stop、net stop、または service Api) を介して、または明示的なアンロード要求 (fltmc unload、 [**Fltunloadfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)、または[**filterunload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)) を介してミニフィルタードライバーをアンロードできます。

ミニフィルタードライバーの[*FilterUnloadCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、ミニフィルタードライバーがアンロードされるときに呼び出されます。 このルーチンは、開いている通信サーバーのポートを閉じ、 [**Fltunregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出して、必要なクリーンアップを実行します。 このルーチンの登録は任意です。 ただし、ミニフィルタードライバーで*FilterUnloadCallback*ルーチンが登録されていない場合は、ミニフィルタードライバーをアンロードできません。 このルーチンの詳細については、「 [FilterUnloadCallback ルーチンの記述](writing-a-filterunloadcallback-routine.md)」を参照してください。

### <a name="span-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanspan-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanspan-idfilter_manager_routines_for_loading_and_unloading_minifilter_driversspanfilter-manager-routines-for-loading-and-unloading-minifilter-drivers"></a><span id="Filter_Manager_Routines_for_Loading_and_Unloading_Minifilter_Drivers"></span><span id="filter_manager_routines_for_loading_and_unloading_minifilter_drivers"></span><span id="FILTER_MANAGER_ROUTINES_FOR_LOADING_AND_UNLOADING_MINIFILTER_DRIVERS"></span>ミニフィルタードライバーを読み込んでアンロードするためのフィルターマネージャールーチン

フィルターマネージャーには、明示的な読み込み要求とアンロード要求に対する次のサポートルーチンが用意されています。これらのルーチンは、ユーザーモードまたはカーネルモードから発行できます。

[**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

[**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

[**FltLoadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)

[**FltUnloadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)

インスタンスのセットアップと破棄のためにコールバックルーチンを登録および登録解除するには、次のルーチンを使用します。

[**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

[**FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)

[**FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)

### <a name="span-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanspan-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanspan-idminifilter_driver_callback_routines_for_instance_setup__teardown__and_unloadspanminifilter-driver-callback-routines-for-instance-setup-teardown-and-unload"></a><span id="Minifilter_Driver_Callback_Routines_for_Instance_Setup__Teardown__and_Unload"></span><span id="minifilter_driver_callback_routines_for_instance_setup__teardown__and_unload"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_INSTANCE_SETUP__TEARDOWN__AND_UNLOAD"></span>インスタンスのセットアップ、破棄、アンロードを行うためのミニフィルタードライバーのコールバックルーチン

次のミニフィルタードライバーコールバックルーチンは、 [**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡される[**FLT\_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体に格納されます。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback" data-raw-source="[&lt;em&gt;InstanceSetupCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)"><em>InstanceSetupCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_SETUP_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)"><strong>PFLT_INSTANCE_SETUP_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback" data-raw-source="[&lt;em&gt;InstanceQueryTeardownCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)"><em>InstanceQueryTeardownCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)"><strong>PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;em&gt;InstanceTeardownStartCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><em>InstanceTeardownStartCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;em&gt;InstanceTeardownCompleteCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><em>InstanceTeardownCompleteCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback" data-raw-source="[&lt;strong&gt;PFLT_INSTANCE_TEARDOWN_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)"><strong>PFLT_INSTANCE_TEARDOWN_CALLBACK</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback" data-raw-source="[&lt;em&gt;FilterUnloadCallback&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)"><em>FilterUnloadCallback</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback" data-raw-source="[&lt;strong&gt;PFLT_FILTER_UNLOAD_CALLBACK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)"><strong>PFLT_FILTER_UNLOAD_CALLBACK</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




