---
title: ファンクション ドライバーでのデバイスの開始
description: ファンクション ドライバーでのデバイスの開始
ms.assetid: 148a3128-9cb1-4a2c-a62e-45199476d968
keywords:
- 機能ドライバー WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a19fd96e6894f27a58cb789bbe89bd7cf7721e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382996"
---
# <a name="starting-a-device-in-a-function-driver"></a>ファンクション ドライバーでのデバイスの開始





関数のドライバーの設定、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine) 、日常的なパス、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)デバイス スタックを要求し、下のすべてのドライバーが IRP に完了するまで、その開始操作を延期します。 参照してください[を延期する PnP IRP の処理まで低いドライバー完了](postponing-pnp-irp-processing-until-lower-drivers-finish.md)のカーネル イベントの使用に関する詳細情報と*IoCompletion* IRP の処理を延期するルーチン。

ときにその[ *DispatchPnP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、下のすべてのドライバーが IRP が完了した後にコントロールを再度獲得、関数ドライバー、デバイスを起動するためのタスクを実行します。 関数のドライバーでは、次のようにプロシージャを使用したデバイスを開始します。

1.  下位のドライバーが IRP が失敗した場合 ([**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)がエラーを返しました)、IRP の処理を続行しないでください。 戻って、必要なクリーンアップを行う、 *DispatchPnP*ルーチン (この一覧の最後のステップに移動) します。

2.  下位のドライバーが IRP を正常に処理する場合は、デバイスを起動します。

    デバイスを起動する正確な手順には、デバイスからデバイスが異なります。 マップ I/O 領域、ハードウェア レジスタの初期化、D0 の電源状態で、デバイスの設定、および割り込みを接続するこのような手順が含まれます[ **IoConnectInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)します。 ドライバーが後にデバイスを再起動する場合、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求と、ドライバーはデバイスの状態を復元する必要があります。

    すべてのドライバーがアクセスする前に、デバイスの電源を必要があります。 参照してください[、デバイスの電源を入れて](powering-up-a-device.md)詳細についてはします。

    ウェイク アップには、デバイスを有効にする場合、その電源ポリシー所有者 (関数ドライバーでは、通常は) 送信待機/ウェイク IRP と完了前に、デバイスに電源がオンにした後、 **IRP\_MN\_開始\_デバイス**要求。 詳細については、次を参照してください。[送信待機/ウェイク IRP](sending-a-wait-wake-irp.md)します。

3.  IRP を保持するキューでは、Irp を起動します。

    ドライバーの定義済みの保留を解除\_新規\_要求フラグし、IRP を保持するキューで、Irp を起動します。 ドライバーは、最初に、クエリ停止後にデバイスを再起動すると、デバイスを開始するときに、この操作を行います。 または、IRP を停止する必要があります。 参照してください[を保持している受信 Irp ときに、デバイスが一時停止](holding-incoming-irps-when-a-device-is-paused.md)詳細についてはします。

4.  \[省略可能な\]呼び出すことによって、デバイス用のインターフェイスを有効にする[ **IoSetDeviceInterfaceState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)します。

    有効にするインターフェイス、存在する場合、ドライバーが以前に登録されているその[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)日常的な (または、INF または共同インストーラーなどの別のコンポーネントで)。

    Windows 2000 および以降のバージョンの Windows では、PnP マネージャー通知は送信されませんデバイス インターフェイス到着するまでの**IRP\_MN\_開始\_デバイス**IRP が完了したことを示すすべてデバイスのドライバーは、その開始操作が完了しました。 PnP マネージャーでは、デバイスのすべてのドライバーが IRP スタートを完了する前に配信される作成要求も失敗します。

5.  IRP を完了します。

    関数のドライバーの*IoCompletion*ルーチンには、状態が返されました\_詳細\_処理\_」の説明に従って、必要な[を延期する PnP IRP の処理まで低いドライバー完了。](postponing-pnp-irp-processing-until-lower-drivers-finish.md)ため、関数のドライバーの*DispatchPnP*ルーチンを呼び出す必要があります[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) I/O 完了処理を再開します。

    Function ドライバーの開始操作が成功した場合、ドライバーは設定**Irp の&gt;IoStatus.Status**ステータス\_成功すると、呼び出し**IoCompleteRequest**より優先度がIO のブースト\_いいえ\_増分値、および状態を返します。\_成功からその*DispatchPnP*ルーチン。

    ドライバーが IRP の呼び出しではエラー状態を設定する関数のドライバーには、その開始操作中にエラーが発生すると場合、 **IoCompleteRequest** IO と\_いいえ\_インクリメントし、そのからエラーを返します*DispatchPnP*ルーチン。

    下位のドライバーが IRP が失敗した場合 (**保留**がエラーを返しました)、ドライバーの関数呼び出し**IoCompleteRequest** IO と\_いいえ\_インクリメントし、を返します**保留**エラーからその*DispatchPnP*ルーチン。 関数のドライバーを設定しない**Irp -&gt;IoStatus.Status**ここで IRP の失敗した下位のドライバーによって、状態は既に設定されているためです。

関数のドライバーが受信すると、 **IRP\_MN\_開始\_デバイス**に構造を調べる必要があります、要求**IrpSp-&gt;Parameters.StartDevice.AllocatedResources**と**IrpSp -&gt;Parameters.StartDevice.AllocatedResourcesTranslated**、それぞれ、生と翻訳済みのリソースについて説明します。ある PnP マネージャーがデバイスに割り当てられます。 ドライバーは、デバッグのため、デバイスの拡張機能の各リソースの一覧のコピーを保存する必要があります。

リソースの一覧はペアになっている[ **CM\_リソース\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list) 、生のリストの各要素が変換されたリストの同じ要素に対応する構造体。 たとえば場合、 **AllocatedResources.List**\[0\]未処理の I/O ポート範囲をについて説明し、 **AllocatedResourcesTranslated.List**\[0\]変換後の同じ範囲をについて説明します。 変換された各リソースには、物理アドレスとリソースの種類が含まれています。

ドライバーでの翻訳済みのメモリ リソースが割り当てられている場合 (**CmResourceTypeMemory**) を呼び出す必要があります[ **MmMapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)を通じて仮想アドレスを物理アドレスにマップするにはそのは、デバイスの登録にアクセスできます。 プラットフォームの独立した方法で動作するドライバーの場合、返された各翻訳されたリソースを確認して、必要に応じてマップします。

関数のドライバーへの応答では、次を行う必要があります、 **IRP\_MN\_開始\_デバイス**デバイスのすべてのリソースにアクセスできるようにします。

1.  コピー **IrpSp -&gt;Parameters.StartDevice.AllocatedResources**デバイス拡張機能にします。

2.  コピー **IrpSp -&gt;Parameters.StartDevice.AllocatedResourcesTranslated**デバイス拡張機能にします。

3.  ループ内の各記述子要素を検査**AllocatedResourcesTranslated**します。 記述子リソースの種類が場合**CmResourceTypeMemory**、呼び出す**MmMapIoSpace**、物理アドレスと翻訳されたリソースの長さを渡します。

ドライバーが受信すると、 **IRP\_MN\_停止\_デバイス**、 **IRP\_MN\_削除\_デバイス**、または**IRP\_MN\_突然\_削除**呼び出すことによってマッピングをリリースする必要がありますが、要求[ **MmUnmapIoSpace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmunmapiospace)で、ようなループします。 ドライバーは呼び出す必要がありますも**MmUnmapIoSpace**にする必要がありますが失敗した場合、 **IRP\_MN\_開始\_デバイス**要求。

参照してください[Bus 相対アドレスを仮想のアドレスにマッピング](mapping-bus-relative-addresses-to-virtual-addresses.md)詳細についてはします。

 

 




