---
title: フレームワーク要求オブジェクトの作成
description: フレームワーク要求オブジェクトの作成
ms.assetid: 4bd668ec-14fb-4999-9535-a49712a26ba6
keywords:
- 要求オブジェクトを作成する、WDK KMDF
- 要求オブジェクトを WDK KMDF、読み取り操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3be2838e848994b8d4c5e9c949458c3913bf34bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377501"
---
# <a name="creating-framework-request-objects"></a>フレームワーク要求オブジェクトの作成





ほとんどのフレームワークの要求オブジェクト、フレームワークによって作成されますが、ドライバーは、要求オブジェクトを作成もできます。

### <a name="request-objects-created-by-the-framework"></a>フレームワークによって作成された要求オブジェクト

I/O マネージャーから framework ベースのドライバーが I/O 要求パケット (IRP) を受け取ると、フレームワークは IRP をインターセプトし、framework 要求オブジェクトを作成します。 フレームワークは、I/O のキューに要求オブジェクトを配置し、ドライバーが登録されている場合[要求ハンドラー](request-handlers.md)キューの適切なハンドラーを呼び出します。

次の図は、フレームワーク、読み取り操作の要求オブジェクトを作成するときに発生する手順を示しています。

![読み取り操作の要求オブジェクトを作成する手順](images/kmdf-creating-request-objects.png)

次の手順は、前の図の番号に対応しています。

1.  ユーザー モード アプリケーションでは、ファイルを読み取り、Microsoft win32 **ReadFile**関数。

2.  **ReadFile**関数呼び出し、I/O マネージャーで、カーネル モードで実行されます。

3.  I/O マネージャー割り当てます IRP の構造体を格納し、 [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)関数、構造内のコード。

4.  I/O マネージャーの呼び出し、 [ **DispatchRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ドライバーの標準のドライバー ルーチン*x*、IRP 構造体へのポインターを渡すことです。 ドライバー *x* framework ベースのドライバー、フレームワークが、ドライバーの*DispatchRead*ルーチン。

5.  フレームワークでは、IRP 構造体を表す要求オブジェクトを作成します。 フレームワークでは、ドライバーのキュー オブジェクトの 1 つに、要求オブジェクトを追加します。

6.  フレームワークは、ドライバーの[ *EvtIoRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)要求ハンドラー、キュー オブジェクトのハンドルと要求オブジェクトのハンドルを渡します。

### <a name="request-objects-created-by-a-driver"></a>ドライバーによって作成された要求オブジェクト

Framework ベースのドライバーは、要求オブジェクトを作成することもできます。 ドライバーの読み取りでは、受信した場合は、要求オブジェクトを作成または書き込み要求が、ドライバーのより大きいデータの量の可能性がありますなど[I/O ターゲット](using-i-o-targets.md)で同時に処理できます。 このような場合は、ドライバーは、いくつかの小さな要求にデータを分割し、追加の要求オブジェクトを使用して、1 つまたは複数の I/O ターゲットにこれらの小さい要求を送信します。

要求オブジェクトを作成するには、ドライバーを呼び出す必要があります[ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)など、要求を初期化するフレームワーク オブジェクト メソッドを続けて[ **WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)します。

ドライバーを呼び出すことができる場合、ドライバーが WDM ディスパッチ ルーチンで WDM Irp を受信し、し、サービスまたはフレームワークを使用して、転送、 [ **WdfRequestCreateFromIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)します。

 

 





