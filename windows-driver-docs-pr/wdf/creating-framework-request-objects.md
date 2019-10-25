---
title: フレームワーク要求オブジェクトの作成
description: フレームワーク要求オブジェクトの作成
ms.assetid: 4bd668ec-14fb-4999-9535-a49712a26ba6
keywords:
- 要求オブジェクト WDK KMDF、作成
- 要求オブジェクト WDK KMDF、読み取り操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1049ce9eaa8c4f2027395440167ae8ee8e5684d1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844684"
---
# <a name="creating-framework-request-objects"></a>フレームワーク要求オブジェクトの作成





ほとんどのフレームワーク要求オブジェクトはフレームワークによって作成されますが、ドライバーは要求オブジェクトを作成することもできます。

### <a name="request-objects-created-by-the-framework"></a>フレームワークによって作成された要求オブジェクト

フレームワークベースのドライバーが i/o マネージャーから i/o 要求パケット (IRP) を受信すると、フレームワークは IRP をインターセプトし、フレームワークの要求オブジェクトを作成します。 フレームワークは、要求オブジェクトを i/o キューに配置し、ドライバーにキューの[要求ハンドラー](request-handlers.md)が登録されている場合は、適切なハンドラーを呼び出します。

次の図は、フレームワークが読み取り操作の要求オブジェクトを作成するときに発生する手順を示しています。

![読み取り操作の要求オブジェクトを作成する手順](images/kmdf-creating-request-objects.png)

次の手順は、前の図の番号に対応しています。

1.  ユーザーモードアプリケーションは、Microsoft Win32 の**ReadFile**関数を呼び出してファイルを読み取ります。

2.  **ReadFile**関数は、カーネルモードで実行される i/o マネージャーを呼び出します。

3.  I/o マネージャーは、IRP 構造体を割り当て、 [**irp\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)格納して、構造体に関数コードを読み取ります。

4.  I/o マネージャーは、ドライバー *x*の[**DispatchRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)標準ドライバールーチンを呼び出し、IRP 構造体へのポインターを渡します。 Driver *x*はフレームワークベースのドライバーであるため、このフレームワークにはドライバーの*DispatchRead*ルーチンが用意されています。

5.  フレームワークは、IRP 構造体を表す要求オブジェクトを作成します。 フレームワークは、要求オブジェクトをドライバーのいずれかのキューオブジェクトに追加します。

6.  フレームワークは、ドライバーの[*EvtIoRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_read)要求ハンドラーを呼び出し、キューオブジェクトハンドルと要求オブジェクトハンドルを渡します。

### <a name="request-objects-created-by-a-driver"></a>ドライバーによって作成された要求オブジェクト

フレームワークベースのドライバーは、要求オブジェクトを作成することもできます。 たとえば、ドライバーは、ドライバーの[i/o ターゲット](using-i-o-targets.md)よりも大きいサイズのデータに対して読み取りまたは書き込みの要求を受け取った場合に、要求オブジェクトを作成することがあります。 このような状況では、ドライバーはデータをいくつかの小さな要求に分割し、追加の要求オブジェクトを使用して、これらの小さな要求を1つ以上の i/o ターゲットに送信することができます。

要求オブジェクトを作成するには、ドライバーが[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)に続けて、 [**WdfUsbTargetPipeFormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)などの要求を初期化するフレームワークオブジェクトメソッドを呼び出す必要があります。

ドライバーが wdm ディスパッチルーチンで WDM Irp を受信し、フレームワークを使用してサービスを実行または転送する場合、ドライバーは[**Wdfrequestcreatefromirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreatefromirp)を呼び出すことができます。

 

 





