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
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1484fe0082fdcf301bb6442f2084bb7031d7bfb8
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128459"
---
# <a name="loading-and-unloading"></a>ロードとアンロード

## <a name="about-loading-and-unloading"></a>読み込みとアンロードについて

ミニフィルタードライバーは、システムの実行中にいつでも読み込むことができます。 ミニフィルタードライバーの[INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)で、SERVICE_BOOT_START、SERVICE_SYSTEM_START、または SERVICE_AUTO_START のドライバーの開始の種類が指定されている場合、従来のフィルタードライバーとの相互運用性をサポートするために、ファイルシステムフィルタードライバーの既存の読み込み順序グループ定義に従ってミニフィルタードライバーが読み込まれます。 システムの実行中は、サービス開始要求 (sc start、net start、または service Api) を介して、または明示的な読み込み要求 (fltmc load、 [**Fltloadfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)、または[**filterload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)) を介してミニフィルタードライバーを読み込むことができます。

ミニフィルタードライバーの[**Driverentry**](writing-a-driverentry-routine-for-a-minifilter-driver.md)ルーチンはミニフィルタードライバーが読み込まれるときに呼び出されます。そのため、ミニフィルタードライバーは、ミニフィルタードライバーのすべてのインスタンスに適用される初期化を実行できます。 その**Driverentry**ルーチンでは、ミニフィルタドライバーは[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)を呼び出して、フィルターマネージャーと[**fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)にコールバックルーチンを登録します。これにより、フィルタマネージャーに対して、ミニフィルタードライバーを開始する準備ができたことが通知されます。ボリュームにアタッチし、i/o 要求をフィルター処理しています。

ミニフィルタードライバーインスタンスは、ミニフィルタードライバーのインストールに使用される[INF ファイル](creating-an-inf-file-for-a-minifilter-driver.md)で定義されています。 ミニフィルタードライバーの INF ファイルでは、既定のインスタンスを定義する必要があります。また、追加のインスタンスを定義することもできます。 これらの定義は、すべてのボリュームに適用されます。 各インスタンス定義には、インスタンス名、その高度、インスタンスを自動的に接続できるかどうかを示すフラグ、手動で、またはその両方を含めることができます。 既定のインスタンスは、フィルタマネージャーがミニフィルタードライバーのマウントおよびインスタンスセットアップコールバックルーチンを正しい順序で呼び出すように、ミニフィルタードライバーの順序を設定するために使用されます。 既定のインスタンスは、呼び出し元がインスタンス名を指定していない場合に、明示的な添付ファイル要求でも使用されます。

フィルターマネージャーは、ボリュームがマウントされた後の最初の作成操作で[*Instancesetupcallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback)ルーチンを呼び出すことによって、使用可能なボリュームについてミニフィルタードライバーに自動的に通知します。 これは、フィルターマネージャーがシステムの起動時に既存のボリュームを列挙するときに、 [**Fltstartfiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)が戻る前に発生することがあります。 また、実行時に、ボリュームがマウントされたとき、または明示的な添付ファイルの要求 (fltmc attach、 [**Fltattachvolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltattachvolume)、または[**filterattach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterattach)) の結果として発生することもあります。

ミニフィルタードライバーインスタンスは、ミニフィルタードライバーがアンロードされたとき、インスタンスがアタッチされているボリュームがマウント解除されたとき、または明示的なデタッチ要求 (fltmc detach、 [**FltDetachVolume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdetachvolume)、または[**filterdetach**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterdetach)) の結果として破棄されます。 ミニフィルタードライバーによって[*InstanceQueryTeardownCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback)ルーチンが登録されると、 **Filterdetach**または**FltDetachVolume**を呼び出すことによって明示的なデタッチ要求が失敗する可能性があります。 破棄は次のように進行します。

- ミニフィルタードライバーによって[*InstanceTeardownStartCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)コールバックルーチンが登録されている場合、フィルターマネージャーは破棄プロセスの開始時にそれを呼び出します。 このルーチンでは、ミニフィルタードライバーがすべての保留中の操作を完了するか、ミニフィルタードライバーによって生成された i/o 要求などの他の処理を完了し、新しい作業項目のキューを停止します。

- インスタンスの破棄中、現在実行中の preoperation または postoperation コールバックルーチンは通常の処理を続行し、postoperation コールバックを待機しているすべての i/o 要求は "ドレイン" またはキャンセルされ、ミニフィルタードライバーは、完了するまで通常の処理を続行します。

- ミニフィルタードライバーによって[*InstanceTeardownCompleteCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback)ルーチンが登録されている場合、未処理の i/o 操作がすべて完了した後に、フィルターマネージャーがこのルーチンを呼び出します。 このルーチンでは、ミニフィルタードライバーによって、開いているファイルがすべて閉じられます。

- インスタンスへの未処理の参照がすべて解放されると、フィルターマネージャーは残りのコンテキストを削除し、インスタンスは完全に破棄されます。

システムの実行中は、サービス停止要求 (sc stop、net stop、または service Api) を介して、または明示的なアンロード要求 (fltmc unload、 [**Fltunloadfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)、または[**filterunload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)) を介してミニフィルタードライバーをアンロードできます。

ミニフィルタードライバーの[*FilterUnloadCallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)ルーチンは、ミニフィルタードライバーがアンロードされるときに呼び出されます。 このルーチンは、開いている通信サーバーのポートを閉じ、 [**Fltunregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)を呼び出して、必要なクリーンアップを実行します。 このルーチンの登録は任意です。 ただし、ミニフィルタードライバーで*FilterUnloadCallback*ルーチンが登録されていない場合は、ミニフィルタードライバーをアンロードできません。 このルーチンの詳細については、「 [FilterUnloadCallback ルーチンの記述](writing-a-filterunloadcallback-routine.md)」を参照してください。

## <a name="filter-manager-routines-for-loading-and-unloading-minifilter-drivers"></a>ミニフィルタードライバーを読み込んでアンロードするためのフィルターマネージャールーチン

フィルターマネージャーには、明示的な読み込み要求とアンロード要求に対する次のサポートルーチンが用意されています。これらのルーチンは、ユーザーモードまたはカーネルモードから発行できます。

- [**FilterLoad**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterload)

- [**FilterUnload**](https://docs.microsoft.com/windows/desktop/api/fltuser/nf-fltuser-filterunload)

- [**FltLoadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltloadfilter)

- [**FltUnloadFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunloadfilter)

インスタンスのセットアップと破棄のためにコールバックルーチンを登録および登録解除するには、次のルーチンを使用します。

- [**FltRegisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)

- [**FltStartFiltering**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltstartfiltering)

- [**FltUnregisterFilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter)

## <a name="minifilter-driver-callback-routines-for-instance-setup-teardown-and-unload"></a>インスタンスのセットアップ、破棄、アンロードを行うためのミニフィルタードライバーのコールバックルーチン

次のミニフィルタードライバーコールバックルーチンは、 [**Fltregisterfilter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltregisterfilter)にパラメーターとして渡される[**FLT_REGISTRATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_registration)構造体のメンバーとして格納されます。

| コールバックルーチンメンバー名 | コールバックルーチンの種類 |
| --------------------- | --------------------- |
| **InstanceSetupCallback** | [PFLT_INSTANCE_SETUP_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_setup_callback) |
| **InstanceQueryTeardownCallback** | [PFLT_INSTANCE_QUERY_TEARDOWN_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_query_teardown_callback) |
| **InstanceTeardownStartCallback** | [PFLT_INSTANCE_TEARDOWN_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) |
| **InstanceTeardownCompleteCallback** | [PFLT_INSTANCE_TEARDOWN_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_instance_teardown_callback) |
| **FilterUnloadCallback** | [PFLT_FILTER_UNLOAD_CALLBACK](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)
