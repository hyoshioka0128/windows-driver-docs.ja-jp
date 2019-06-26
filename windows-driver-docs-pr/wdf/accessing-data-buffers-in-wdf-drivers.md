---
title: WDF ドライバー (KMDF または UMDF) でのデータ バッファーへのアクセス
description: Windows Driver Frameworks (WDF) ドライバーは、読み取り、書き込み、またはデバイスの I/O 操作の要求を受け取る、要求オブジェクトには、入力バッファー、出力バッファー、またはその両方が含まれます。
ms.assetid: ceba2279-b0fb-4261-b439-723d5dad967b
keywords:
- 要求の WDK KMDF、データ バッファーの処理
- データ バッファーの WDK KMDF
- 入力バッファー WDK KMDF
- 出力バッファー WDK KMDF
- バッファー WDK KMDF
- バッファー内の I/O WDK KMDF
- ダイレクト I/O WDK KMDF
- バッファーも直接 I/O WDK KMDF
- I/O 要求の WDK KMDF、データ バッファー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6980ab1aa5068f5583685fb587a55ed35a3e2658
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363868"
---
# <a name="accessing-data-buffers-in-wdf-drivers-kmdf-or-umdf"></a>WDF ドライバー (KMDF または UMDF) でのデータ バッファーへのアクセス


Windows Driver Frameworks (WDF) ドライバーは、読み取り、書き込み、またはデバイスの I/O 操作の要求を受け取る、要求オブジェクトには、入力バッファー、出力バッファー、またはその両方が含まれます。

入力バッファーには、ドライバーが必要な情報が含まれています。 書き込み要求、この情報は通常値がデータを関数のドライバーがデバイスに送信する必要があります。 デバイス I/O 制御要求では、入力バッファーには、ドライバーを実行する必要があります操作の種類を示す情報が含まれます。

出力バッファーは、ドライバーからの情報を受け取ります。 読み取り要求は、この情報は通常値が関数のドライバーがデバイスから受信するデータです。 デバイス I/O 制御要求では、出力バッファーは状態または要求の I/O 制御コードで指定したその他の情報を受け取る可能性があります。

要求のデータ バッファーにアクセスするには、ドライバーを使用する手法は、デバイスのデータ バッファーにアクセスするため、ドライバーの方法によって異なります。 次の 3 つのアクセス方法はあります。

-   [I/O バッファー](#buffered)します。 I/O マネージャーは、ドライバーと共有している中間バッファーを作成します。
-   [ダイレクト I/O](#direct)します。 I/O マネージャーは、物理メモリにバッファー領域をロックし、バッファーの領域に直接アクセスすると、ドライバーを提供します。
-   [バッファーも直接 I/O](#neither)します。 I/O マネージャーは、要求のバッファー領域の仮想アドレスを含む、ドライバーを提供します。 I/O マネージャーでは、要求のバッファー領域を検証しないため、ドライバーは、バッファー領域がアクセスできるし、物理メモリにバッファー領域をロックことを確認する必要があります。

カーネル モード ドライバー フレームワーク (KMDF) ドライバーは、3 つのアクセス方法のいずれかを使用できます。 ユーザー モード ドライバー フレームワーク (UMDF) ドライバーは読み取り、書き込み、および、IOCTL 要求をバッファリングまたはダイレクト I/O を使用でき、できます[を指定する要求を変換、**メソッド\_NEITHER**メソッド](managing-buffer-access-methods-in-umdf-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)します。

## <a href="" id="ddk-preprocessing-i-o-requests-df"></a>バッファーへのアクセス方法を指定します。


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

読み取りと書き込みを要求すると、ドライバー スタックのすべてのドライバーは下位のドライバーがメソッドを使用に関係なく、「も」メソッドを使用できます、最上位レベルのドライバーを除く、デバイスのバッファーにアクセスするため、同じメソッドを使用する必要があります。

以降のバージョン 1.13 では、KMDF ドライバー アクセス方法を指定のすべてのデバイスの読み取りと書き込み要求を呼び出して[ **WdfDeviceInitSetIoTypeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)デバイスごとにします。 たとえば、ドライバーでは、そのデバイスの 1 つのバッファー内の I/O メソッドを指定する場合は、読み取りおよび書き込み要求、デバイスのドライバーを提供するとき I/O マネージャー バッファー内の I/O メソッドは使用します。

デバイス I/O 制御要求の場合は、I/O 制御コード (IOCTL) には、バッファーへのアクセス方法を指定するビットが含まれています。 その結果、KMDF ドライバーは何も操作の Ioctl のバッファリング方法を選択する必要はありません。 Ioctl の詳細については、次を参照してください。 [I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)します。 読み取りおよび書き込みとは異なり、同じアクセス方法を指定する必要はありませんすべてのデバイスの Ioctl を要求します。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF ドライバーを指定します*設定*へのアクセスのために、フレームワークを使用するメソッドの読み書き、要求とデバイスの I/O 要求を制御します。 UMDF ドライバーを提供する値のみの設定は、フレームワークによって使用されるとは限りません。 詳細については、次を参照してください。 [UMDF ドライバーを使用したバッファー アクセス方法を管理する](managing-buffer-access-methods-in-umdf-drivers.md)します。

UMDF ドライバーは、呼び出すことによって、デバイスの読み取り、書き込み、IOCTL 要求のすべてのアクセス方法を指定[ **WdfDeviceInitSetIoTypeEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)デバイスごとにします。 たとえば、ドライバーでは、そのデバイスの 1 つのバッファー内の I/O メソッドを指定する場合、そのデバイスのドライバーを読み取り、書き込み、IOCTL 要求を配信する場合フレームワークにはバッファー内の I/O メソッドが使用されます。

Ioctl KMDF と UMDF の間には、バッファーへのアクセス方法の違いに注意してください。 KMDF ドライバーでは、Ioctl のバッファーへのアクセス メソッドは指定しない一方、UMDF ドライバーは、Ioctl のバッファーへのアクセス方法を指定しないでください。

WDF ドライバーでは、I/O ターゲットを使用する I/O メソッドの不適切な手法を使用して、I/O 要求のバッファーを記述、フレームワークは、バッファーの説明を修正します。 たとえば、ドライバーに渡されるバッファーを記述する、MDL を使用している場合[ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)I/O のターゲット バッファー内の I/O を使用している場合、(バッファーである必要がありますを使用して指定仮想アドレス MDLs ではなく)、フレームワークは、バッファーの説明を MDL から仮想アドレスと長さに変換します。 ただしがより効率的な場合は、ドライバーは、正しい形式でバッファーを指定します。

Framework メモリ オブジェクト、ルック アサイド リスト、MDLs、およびローカル バッファーについては、次を参照してください。[メモリ バッファーを使用して](using-memory-buffers.md)します。

メモリ バッファーを削除する時期については、次を参照してください。[メモリ バッファーのライフ サイクル](memory-buffer-life-cycle.md)します。

## <a href="" id="buffered"></a> バッファー内の I/O のデータ バッファーへのアクセス


ドライバーは、バッファー内の I/O を使用して、その動作はデータ要求、KMDF または UMDF の使用かどうかの種類に応じて変更します。

<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

KMDF ドライバーでは、バッファー内の I/O を使用する場合、I/O マネージャーは、ドライバーは、要求の種類ごとにアクセスできる 1 つの中間バッファーを作成します。 動作を次に示します。

-   書き込み要求。 I/O マネージャーは、ドライバー スタックを呼び出す前に、呼び出し元のアプリの入力バッファーから入力情報を転送します。 次に、KMDF ドライバーは中間バッファーからの入力情報を読み取るし、デバイスに書き込みます。
-   読み取りを要求します。 KMDF ドライバーでは、デバイスから情報を読み取るし、によって中間バッファーに格納されます。 次に、I/O マネージャーは、アプリの出力バッファーに中間バッファーからの出力データをコピーします。
-   デバイス I/O 制御要求。 KMDF ドライバーでは、読み取りまたはまたは中間バッファーから、その要求のデータを書き込みます。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF ドライバーでは、バッファー内の I/O を使用すると、ドライバーのホスト プロセスには、要求の種類に応じて、1 つまたは 2 つの中間バッファーが作成されます。 動作を次に示します。

-   書き込み要求。 フレームワークでは、1 つのバッファーを作成し、呼び出し元のアプリの入力バッファーからの入力情報を転送して、ドライバー スタックを呼び出しています。 UMDF ドライバーでは、中間バッファーからの入力情報を読み取るし、デバイスに書き込みます。
-   読み取りを要求します。 UMDF ドライバーでは、デバイスから情報を読み取るし、フレームワークが作成されるバッファーに格納します。 ドライバーのホスト プロセスは、アプリの出力バッファーに中間バッファーからの出力データをコピーします。
-   デバイス I/O 制御要求。 フレームワークは、ドライバーがアクセスできる IOCTL の入力と出力バッファーに対応する 2 つのバッファーを作成します。 フレームワークでは、IOCTL から新しい中間バッファーに、入力情報をコピーし、ドライバーが使用できるようにします。 フレームワークが、出力バッファーの内容をコピーしていないため、ドライバーからの読み取りを試行しないでください (それ以外の場合、最終的にガベージ データの読み取り)。 ドライバーは出力バッファーに書き込まれるすべてのデータは、IOCTL バッファーを元に戻すがコピーされ、I/O 要求が正常に完了すると、アプリに返されます。 ドライバーは、入力バッファーに書き込むデータが破棄され、呼び出し元のアプリに返されないことに注意してください。

KMDF と UMDF ドライバーを呼び出し、バッファーを表す framework メモリ オブジェクトを識別するハンドルを取得する[ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)または[ **WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)かどうかに応じて、これは、読み取りまたは書き込み要求。 ドライバーを呼び出して、バッファーへのポインターを取得できます[ **WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)します。 ドライバーの呼び出し、バッファーを読み書きする[ **WdfMemoryCopyFromBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[ **WdfMemoryCopyToBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)します。

ドライバーを呼び出し、仮想アドレスと、バッファーの長さを取得する[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[ **WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer).

KMDF ドライバーを呼び出し、バッファーのメモリ記述子一覧 (MDL) をビルドして、割り当て、する[ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[ **WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl).

## <a href="" id="direct"></a> ダイレクト I/O のデータ バッファーへのアクセス


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

I/O マネージャーが指定すると、(通常はユーザー モード アプリケーション) の I/O 要求の発信元が物理メモリにバッファー領域をロックし、し、ドライバーを提供するバッファー領域のアクセシビリティを検証する場合は、ドライバーは、ダイレクト I/O を使用して、バッファー領域への直接アクセスします。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

ドライバーがダイレクト i/o は、基本設定を指定し、ダイレクト I/O のすべての UMDF 要件を満たしているかどうか (を参照してください[UMDF ドライバーを使用したバッファー アクセス方法を管理する](managing-buffer-access-methods-in-umdf-drivers.md))、フレームワーク、I/O から受け取るメモリ バッファーをマップします。ドライバーのホストに直接 manager は、プロセス アドレス空間と、バッファーの領域に直接アクセスできるため、ドライバーを提供します。

ドライバーの呼び出し、バッファー領域を表す framework メモリ オブジェクトを識別するハンドルを取得する[ **WdfRequestRetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)または[ **WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)します。 ドライバーを呼び出して、バッファーへのポインターを取得できます[ **WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)します。 ドライバーの呼び出し、バッファーを読み書きする[ **WdfMemoryCopyFromBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[ **WdfMemoryCopyToBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)します。

ドライバーを呼び出し、仮想アドレスとバッファー領域の長さを取得する[ **WdfRequestRetrieveInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[ **WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer).

デバイスのドライバーがダイレクト I/O を使用している場合、I/O マネージャー MDLs を使用してバッファーについて説明します。 KMDF ドライバーを呼び出し、バッファーの MDL へのポインターを取得する[ **WdfRequestRetrieveInputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[ **WdfRequestRetrieveOutputWdmMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl). UMDF ドライバー MDLs にアクセスできません。

## <a href="" id="neither"></a> バッファーも直接 I/O のデータ バッファーへのアクセス


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

ドライバーと呼ばれるバッファーへのアクセス メソッドを使用するかどうか、 *I/O もダイレクト I/O メソッドもバッファー* (または略して「も」メソッド)、I/O マネージャーが単にアドレスを仮想のドライバーを提供しますの実行者要求のバッファー領域の指定された I/O 要求。 I/O マネージャーでは、I/O 要求のバッファー領域を検証しないため、ドライバーは、バッファー領域がアクセスできるし、物理メモリにバッファー領域をロックことを確認する必要があります。

I/O マネージャーを提供する仮想アドレスは、I/O 要求の発信元のプロセスのコンテキストでのみアクセスできます。 発信元のプロセスのコンテキストで実行するには、ドライバー スタックの最上位レベルのドライバーのみが保証されます。

I/O 要求のバッファー領域へのアクセスを取得する最上位レベルのドライバーが提供する必要があります、 [ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数。 フレームワークでは、ドライバーの I/O 要求を受信するたびにこのコールバック関数を呼び出します。

要求をバッファーへのアクセス メソッドが「も」の場合は、KMDF ドライバーは、各バッファーは、次を行う必要があります。

1.  呼び出す[ **WdfRequestRetrieveUnsafeUserInputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)または[ **WdfRequestRetrieveUnsafeUserOutputBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)にバッファーの取得仮想アドレス。

2.  呼び出す[ **WdfRequestProbeAndLockUserBufferForRead** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforread)または[ **WdfRequestProbeAndLockUserBufferForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforwrite)およびロックのプローブ、バッファーおよびバッファーのメモリ オブジェクトのフレームワークを識別するハンドルを取得します。

3.  要求のメモリ オブジェクトのハンドルを保存[コンテキスト領域](using-request-object-context.md)します。

4.  呼び出す[ **WdfDeviceEnqueueRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)フレームワークに要求を返します。

フレームワークは、その後、ドライバーの I/O キューのいずれかに要求を追加します。 ドライバーが指定されている場合[要求ハンドラー](request-handlers.md)フレームワークが最終的に、適切な要求ハンドラーを呼び出します。

要求ハンドラーは、要求のコンテキストの領域から、要求のメモリ オブジェクトのハンドルを取得できます。 ドライバーは、ハンドルを渡すことができます[ **WdfMemoryGetBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)バッファーのアドレスを取得します。

場合によっては、最上位レベルのドライバーする必要がありますを使用して、前の手順をユーザー モード バッファーにアクセスするドライバーは、「も」アクセス メソッドを使用していない場合でもです。 たとえば、ドライバーがバッファー内の I/O を使用するとします。 バッファー内のアクセス メソッドを使用する I/O 制御コードは、ユーザー モード バッファーへの埋め込みポインターを格納する構造体を渡すことがあります。 このような場合は、ドライバーが提供する必要があります、 [ *EvtIoInCallerContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を構造体からポインターを抽出し、前を使用して、手順 2 ~ 4 です。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF ドライバーは、この種類のバッファーを直接処理する必要はありませんので UMDF バッファーも、直接の I/O の種類のバッファーをサポートしていません。

ただし、フレームワークが受信した場合のようなバッファーから読み取り/書き込み I/O マネージャーで、利用できるように UMDF ドライバーにバッファー内の I/O またはドライバーが選択されているアクセス方法によって、ダイレクト I/O として。 フレームワーク IOCTL「も」バッファー メソッドを指定する場合、バッファー内の I/O またはダイレクト I/O が、INF ディレクティブの有無に基づいて IOCTL 要求のバッファーへのアクセス メソッド必要に応じて変換できます。 参照してください[UMDF ドライバーを使用したバッファー アクセス方法を管理する](managing-buffer-access-methods-in-umdf-drivers.md)の詳細。

 

 





