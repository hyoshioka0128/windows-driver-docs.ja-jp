---
title: WDF ドライバー (KMDF または UMDF) でのデータ バッファーへのアクセス
description: Windows Driver Framework (WDF) ドライバーが読み取り、書き込み、またはデバイス i/o 制御要求を受信すると、要求オブジェクトには入力バッファー、出力バッファー、またはその両方が含まれます。
ms.assetid: ceba2279-b0fb-4261-b439-723d5dad967b
keywords:
- WDK KMDF、データバッファーの処理を要求する
- データバッファー WDK KMDF
- 入力バッファー WDK KMDF
- 出力バッファー WDK KMDF
- WDK KMDF のバッファー
- バッファーされる i/o WDK KMDF
- ダイレクト i/o WDK KMDF
- バッファーも直接 i/o WDK KMDF もありません
- I/o 要求 (WDK KMDF、データバッファー)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed05fb46f85d09394f4d093521d3c53c668c95dd
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242851"
---
# <a name="accessing-data-buffers-in-wdf-drivers-kmdf-or-umdf"></a>WDF ドライバー (KMDF または UMDF) でのデータ バッファーへのアクセス


Windows Driver Framework (WDF) ドライバーが読み取り、書き込み、またはデバイス i/o 制御要求を受信すると、要求オブジェクトには入力バッファー、出力バッファー、またはその両方が含まれます。

入力バッファーには、ドライバーが必要とする情報が含まれています。 書き込み要求の場合、この情報は通常、関数ドライバーがデバイスに送信する必要があるデータです。 デバイス i/o 制御要求の場合、入力バッファーには、ドライバーが実行する必要のある操作の種類を示す情報が含まれている場合があります。

出力バッファーは、ドライバーから情報を受信します。 読み取り要求の場合、この情報は通常、関数ドライバーがデバイスから受け取るデータです。 デバイス i/o 制御要求の場合、出力バッファーは、要求の i/o 制御コードによって指定された状態またはその他の情報を受け取ることがあります。

ドライバーが要求のデータバッファーにアクセスするときに使用する技法は、デバイスのデータバッファーにアクセスするためのドライバーの方法によって異なります。 次の3つのアクセス方法があります。

-   [バッファー](#buffered)された i/o。 I/o マネージャーは、ドライバーと共有する中間バッファーを作成します。
-   [ダイレクト i/o](#direct)。 I/o マネージャーは、バッファー領域を物理メモリにロックしてから、ドライバーにバッファー領域への直接アクセスを提供します。
-   [バッファーも直接 I/o もありませ](#neither)ん。 I/o マネージャーは、ドライバーに要求のバッファー領域の仮想アドレスを提供します。 I/o マネージャーは、要求のバッファー領域を検証しません。そのため、ドライバーは、バッファー領域がアクセス可能であることを確認し、バッファー領域を物理メモリにロックする必要があります。

カーネルモードドライバーフレームワーク (KMDF) ドライバーは、3つのアクセス方法のいずれかを使用できます。 ユーザーモードドライバーフレームワーク (UMDF) ドライバーでは、読み取り、書き込み、および IOCTL 要求に対してバッファーされたまたは直接 i/o を使用できます。また、[メソッドを指定する要求は、**どちら**のメソッド\_も変換](managing-buffer-access-methods-in-umdf-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)できます。

## <a href="" id="ddk-preprocessing-i-o-requests-df"></a>バッファーアクセスメソッドの指定


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

読み取りおよび書き込み要求の場合、ドライバースタック内のすべてのドライバーは、デバイスのバッファーにアクセスするために同じ方法を使用する必要があります。ただし、最上位レベルのドライバーでは、どの方法が下位のドライバーで使用されるかに関係なく、"どちらの" 方法も使用できます。

バージョン1.13 以降では、KMDF ドライバーは、デバイスごとに[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出すことによって、すべてのデバイスの読み取り要求と書き込み要求のアクセス方法を指定します。 たとえば、ドライバーが1つのデバイスに対してバッファーされた i/o メソッドを指定した場合、i/o マネージャーは、そのデバイスのドライバーに読み取り要求と書き込み要求を配信するときに、バッファーされた i/o メソッドを使用します。

デバイス i/o 制御要求の場合、i/o 制御コード (IOCTL) には、バッファーアクセス方法を指定するビットが含まれます。 その結果、KMDF ドライバーは、Ioctl のバッファリング方法を選択するために何らかのアクションを実行する必要がありません。 Ioctl の詳細については、「 [I/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください。 読み取り要求と書き込み要求とは異なり、デバイスのすべての Ioctl で同じアクセス方法を指定する必要はありません。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF ドライバーは、フレームワークが読み取り要求と書き込み要求に使用するアクセス方法の*設定*と、デバイスの i/o 制御要求を指定します。 UMDF ドライバーが提供する値は、基本設定のみであり、フレームワークによって使用されるとは限りません。 詳細については、「 [UMDF ドライバーでのバッファーアクセスメソッドの管理](managing-buffer-access-methods-in-umdf-drivers.md)」を参照してください。

UMDF ドライバーでは、デバイスごとに[**Wdfdeviceinitsetiotypeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetiotypeex)を呼び出すことによって、デバイスのすべての読み取り、書き込み、および IOCTL 要求のアクセス方法を指定します。 たとえば、ドライバーがいずれかのデバイスに対してバッファーされた i/o メソッドを指定した場合、フレームワークは、そのデバイスのドライバーに読み取り、書き込み、および IOCTL 要求を配信するときに、バッファーされた i/o メソッドを使用します。

KMDF と UMDF の間の Ioctl に対するバッファーアクセス手法の違いに注意してください。 KMDF ドライバーでは、Ioctl のバッファーアクセス方法は指定されませんが、UMDF ドライバーは Ioctl のバッファーアクセス方法を指定します。

I/o ターゲットが使用する i/o メソッドに対して不適切な手法を使用して、WDF ドライバーで i/o 要求のバッファーが記述されている場合、フレームワークはバッファーの説明を修正します。 たとえば、ドライバーが、 [**Wdfiotargetsendreadsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)渡されるバッファーを記述するために mdl を使用する場合、および i/o ターゲットがバッファー I/o (mdls ではなく仮想アドレスを使用してバッファーを指定する必要があります) を使用している場合、フレームワークは、バッファーの説明を MDL から仮想アドレスと長さに変換します。 ただし、ドライバーで正しい形式のバッファーを指定した方が効率的です。

フレームワークメモリオブジェクト、ルックアサイドリスト、MDLs、およびローカルバッファーの詳細については、「[メモリバッファーの使用](using-memory-buffers.md)」を参照してください。

メモリバッファーが削除されるタイミングの詳細については、「[メモリバッファーの有効](memory-buffer-life-cycle.md)期間」を参照してください。

## <a href="" id="buffered"></a>バッファリングされる i/o のデータバッファーへのアクセス


ドライバーがバッファー i/o を使用している場合、データ要求の種類と、KMDF または UMDF のどちらを使用しているかに応じて、その動作が変わります。

<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

KMDF ドライバーがバッファー i/o を使用する場合、i/o マネージャーは、ドライバーがすべての種類の要求にアクセスできる中間バッファーを1つ作成します。 次のような処理が行われます。

-   書き込み要求。 I/o マネージャーは、ドライバースタックを呼び出す前に、呼び出し元アプリの入力バッファーから入力情報を転送します。 次に、KMDF ドライバーは、中間バッファーから入力情報を読み取り、デバイスに書き込みます。
-   読み取り要求。 KMDF ドライバーは、デバイスから情報を読み取り、中間バッファーに格納します。 次に、i/o マネージャーによって、出力データが中間バッファーからアプリの出力バッファーにコピーされます。
-   デバイス i/o 制御要求。 KMDF ドライバーは、中間バッファーとの間でその要求のデータの読み取りまたは書き込みを行います。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF ドライバーでバッファー i/o が使用されている場合、ドライバーホストプロセスは、要求の種類に応じて、1つまたは2つの中間バッファーを作成します。 次のような処理が行われます。

-   書き込み要求。 フレームワークは、1つのバッファーを作成し、呼び出し元のアプリの入力バッファーから入力情報を転送してから、ドライバースタックを呼び出します。 UMDF ドライバーは、中間バッファーから入力情報を読み取り、それをデバイスに書き込みます。
-   読み取り要求。 UMDF ドライバーは、デバイスから情報を読み取って、フレームワークによって作成されたバッファーに格納します。 ドライバーホストプロセスは、中間バッファーからアプリの出力バッファーに出力データをコピーします。
-   デバイス i/o 制御要求。 このフレームワークは、ドライバーがアクセスできる IOCTL の入力バッファーと出力バッファーに対応する2つのバッファーを作成します。 フレームワークは、IOCTL からの入力情報を新しい中間バッファーにコピーし、ドライバーで使用できるようにします。 フレームワークは出力バッファーの内容をコピーしないため、ドライバーからの読み取りは試行されません (それ以外の場合は、ガベージデータの読み取りが終了します)。 ドライバーが出力バッファーに書き込むデータは、元の IOCTL バッファーにコピーされて、i/o 要求が正常に完了したときにアプリに返されます。 ドライバーが入力バッファーに書き込むデータはすべて破棄され、呼び出し元のアプリには返されないことに注意してください。

バッファーを表すフレームワークメモリオブジェクトへのハンドルを取得するには、KMDF と UMDF の両方のドライバーが、読み取りまたは書き込みのどちらの要求かに応じて、 [**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)または[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)を呼び出します。 ドライバーは、 [**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出すことによって、バッファーへのポインターを取得できます。 バッファーの読み取りと書き込みを行うには、ドライバーは[**Wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[**wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)を呼び出します。

バッファーの仮想アドレスと長さを取得するために、ドライバーは[**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)を呼び出します。

バッファーのメモリ記述子リスト (MDL) を割り当ててビルドするには、KMDF ドライバーが[**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)を呼び出します。

## <a href="" id="direct"></a>直接 i/o のデータバッファーへのアクセス


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

ドライバーが直接 i/o を使用している場合、i/o マネージャーは、i/o 要求の発信元 (通常はユーザーモードアプリケーション) によって指定されたバッファー領域のアクセシビリティを検証し、バッファー領域を物理メモリにロックして、バッファー領域への直接アクセスをドライバーに提供します。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

ドライバーでダイレクト i/o の優先順位が指定されており、ダイレクト i/o のすべての UMDF 要件が満たされている場合 (「 [UMDF ドライバーでのバッファーアクセスメソッドの管理](managing-buffer-access-methods-in-umdf-drivers.md)」を参照してください)、フレームワークは、i/o マネージャーから受信したメモリバッファーをドライバーのホストプロセスのアドレス空間に直接マップします。

バッファー領域を表すフレームワークメモリオブジェクトへのハンドルを取得するために、ドライバーは[**WdfRequestRetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputmemory)または[**WdfRequestRetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputmemory)を呼び出します。 ドライバーは、 [**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)を呼び出すことによって、バッファーへのポインターを取得できます。 バッファーの読み取りと書き込みを行うには、ドライバーは[**Wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopyfrombuffer)または[**wdfmemorycopyfrombuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorycopytobuffer)を呼び出します。

バッファー領域の仮想アドレスと長さを取得するために、ドライバーは[**WdfRequestRetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputbuffer)または[**WdfRequestRetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputbuffer)を呼び出します。

デバイスのドライバーが直接 i/o を使用している場合、i/o マネージャーは MDLs を使用してバッファーを記述します。 KMDF ドライバーは、バッファーの MDL へのポインターを取得するために、 [**WdfRequestRetrieveInputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveinputwdmmdl)または[**WdfRequestRetrieveOutputWdmMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveoutputwdmmdl)を呼び出します。 UMDF ドライバーは MDLs にアクセスできません。

## <a href="" id="neither"></a>バッファーにも直接 i/o でもデータバッファーにアクセスする


<a href="" id="kmdf-drivers"></a>**KMDF ドライバー**  

お使いのドライバーが、バッファーに格納された*i/o メソッドまたは直接 i/o メソッド*(または "どちらでもありません") として知られているバッファーアクセス方法を使用している場合、i/o マネージャーは単に、要求のバッファー領域に対して指定された i/o 要求の発信元によってドライバーを提供します。 I/o マネージャーは、i/o 要求のバッファー領域を検証しません。そのため、ドライバーは、バッファー領域がアクセス可能であることを確認し、バッファー領域を物理メモリにロックする必要があります。

I/o マネージャーによって提供される仮想アドレスには、i/o 要求の発信元のプロセスコンテキストでのみアクセスできます。 ドライバースタック内の最上位レベルのドライバーのみが、発信元のプロセスコンテキストで実行されることが保証されています。

I/o 要求のバッファー領域へのアクセスを取得するには、最高レベルのドライバーが[*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を提供する必要があります。 フレームワークは、ドライバーの i/o 要求を受け取るたびに、このコールバック関数を呼び出します。

要求のバッファーアクセスメソッドが "どちらも" ではない場合、KMDF ドライバーは、各バッファーに対して次の操作を行う必要があります。

1.  [**WdfRequestRetrieveUnsafeUserInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuserinputbuffer)または[**WdfRequestRetrieveUnsafeUserOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestretrieveunsafeuseroutputbuffer)を呼び出して、バッファーの仮想アドレスを取得します。

2.  [**WdfRequestProbeAndLockUserBufferForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforread)または[**WdfRequestProbeAndLockUserBufferForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestprobeandlockuserbufferforwrite)を呼び出して、バッファーをプローブしてロックし、バッファーのフレームワークメモリオブジェクトへのハンドルを取得します。

3.  メモリオブジェクトハンドルを要求の[コンテキスト空間](using-request-object-context.md)に保存します。

4.  [**Wdfdeviceenqueuerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceenqueuerequest)呼び出します。これにより、フレームワークに要求が返されます。

その後、このフレームワークは、ドライバーの i/o キューのいずれかに要求を追加します。 ドライバーが[要求ハンドラー](request-handlers.md)を提供した場合、フレームワークは最終的に適切な要求ハンドラーを呼び出します。

要求ハンドラーは、要求のコンテキスト空間から要求のメモリオブジェクトハンドルを取得できます。 ドライバーは、バッファーのアドレスを取得するためにハンドルを[**WdfMemoryGetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdfmemorygetbuffer)に渡すことができます。

場合によっては、ドライバーが "どちらの" アクセス方法を使用していない場合でも、最上位レベルのドライバーがユーザーモードのバッファーにアクセスするには、前の手順を使用する必要があります。 たとえば、ドライバーがバッファーされた i/o を使用しているとします。 バッファーされたアクセスメソッドを使用する i/o 制御コードは、ユーザーモードバッファーへの埋め込みポインターを含む構造体を渡す場合があります。 このような場合、ドライバーは、構造からポインターを抽出し、前の手順 2. ~ 4. を使用する、 [*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)コールバック関数を提供する必要があります。

<a href="" id="umdf-drivers"></a>**UMDF ドライバー**  

UMDF では、バッファーも直接 i/o 型のバッファーもサポートされていないため、UMDF ドライバーはこの種類のバッファーを直接処理する必要はありません。

ただし、このようなバッファーを、i/o マネージャーから読み取りまたは書き込み用に受信した場合、ドライバーによって選択されたアクセス方法に応じて、UMDF ドライバーが、バッファー内 i/o またはダイレクト i/o として使用できるようになります。 "指定されていません" バッファーメソッドを指定する IOCTL をフレームワークが受信した場合は、必要に応じて、INF ディレクティブの有無に基づいて、IOCTL 要求のバッファーアクセスメソッドをバッファー i/o またはダイレクト i/o に変換できます。 詳細については、「 [UMDF ドライバーでのバッファーアクセスメソッドの管理](managing-buffer-access-methods-in-umdf-drivers.md)」を参照してください。

 

 





