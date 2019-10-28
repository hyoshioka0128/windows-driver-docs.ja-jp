---
title: UMDF 1.x ドライバーのデータバッファーへのアクセス
description: UMDF 1.x ドライバーのデータバッファーへのアクセス
ms.assetid: cbd67ada-696e-403e-9b35-d8ed06a844d5
keywords:
- データバッファー WDK UMDF
- バッファー WDK UMDF
- WDK UMDF、データバッファーの処理を要求する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ef43e1f944a9310e3f85cbc67120236c3991bb6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843445"
---
# <a name="accessing-data-buffers-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーのデータバッファーへのアクセス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーが読み取り、書き込み、またはデバイス i/o 制御要求を受信すると、要求オブジェクトには、入力バッファーまたは出力バッファーのいずれかまたは両方が含まれます。 (いくつかのデバイス i/o 制御要求では、2つの入力、2つの出力、または2つの入力/出力バッファーが提供します)。

入力バッファーには、ドライバーが必要とする情報が含まれています。 書き込み要求の場合、通常、この情報は、関数ドライバーがデバイスに送信する必要があるデータです。 デバイス i/o 制御要求の場合、入力バッファーには、ドライバーが実行する必要のある操作の種類を示す情報が含まれている場合があります。

出力バッファーは、ドライバーから情報を受信します。 読み取り要求の場合、通常、この情報は関数ドライバーがデバイスから受け取るデータです。 デバイス i/o 制御要求の場合、出力バッファーには、要求の i/o 制御コードによって指定された状態またはその他の情報が表示されることがあります。

ドライバーが要求のデータバッファーにアクセスするときに使用する技法は、デバイスのデータバッファーにアクセスするためのドライバーの方法によって異なります。 UMDF では、次のバッファーアクセスメソッドがサポートされています。

-   バージョン1.9 より前のバージョンの UMDF では、バッファーされた[i/o](#using-buffered-i-o-in-umdf-drivers)アクセス方法のみがサポートされます。 これらのバージョンの UMDF で実行される UMDF ベースのドライバーでは、すべての読み取り、書き込み、およびデバイスの i/o 制御要求に対して、バッファーされた i/o メソッドのみを使用できます。 I/o 要求のデータバッファーにアクセスするには、UMDF ベースのドライバーで[**IWDFIoRequest:: GetInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)オブジェクトと[**IWDFIoRequest:: getinputmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory)オブジェクトのメソッドを使用する必要があります。

-   UMDF バージョン1.9 以降では、2つのアクセスメソッド ([バッファー i/o](#using-buffered-i-o-in-umdf-drivers)と[ダイレクト i/o](#using-direct-i-o-in-umdf-drivers)) を、umdf ベースのドライバーで使用できます。 UMDF バージョン1.9 以降用に記述された UMDF ドライバーでは、 [**IWDFIoRequest2:: RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2:: RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2:: RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)、または[**IWDFIoRequest2:: を使用する必要があります。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)データバッファーにアクセスするための RetrieveOutputMemory オブジェクトメソッド。

3番目のアクセスメソッドは、"バッファーなし" または "[直接](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)i/o" と呼ばれ、umdf ベースのドライバーでは使用できませんが、umdf は、一部の i/o 要求を、"いずれの" メソッドから、umdf version がサポートするメソッドに変換できます。

ほとんどの場合、UMDF ベースのドライバーは、データバッファーにアクセスするために同じ UMDF オブジェクトメソッドを呼び出します。これは、UMDF とドライバーがバッファリングされた i/o または直接 i/o を使用しているかどうかによって決まります。 多くの場合、ダイレクト i/o では、バッファー i/o よりもパフォーマンスが向上します。

このトピックの次のセクションでは、について説明します。

-   推奨される[バッファーアクセス方法](#specifying-a-preferred-buffer-access-method)と推奨される[バッファー取得モード](#specifying-a-buffer-retrieval-mode)を指定する方法

-   使用するバッファーの方法と取得モードを、UMDF でどのように[選択](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)するか

-   UMDF が使用しているバッファーアクセス方法をドライバーが[取得](#how-a-driver-can-obtain-the-access-method-for-an-i-o-request)する方法

-   バッファーに格納された、[直接](#using-direct-i-o-in-umdf-drivers)、[バッファー](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers) [なしのアクセス](#using-buffered-i-o-in-umdf-drivers)方法を使用するためのガイドライン

### <a href="" id="specifying-a-preferred-buffer-access-method"></a>適切なバッファーアクセス方法の指定

UMDF バージョン1.9 以降では、バッファーとダイレクト i/o の両方のアクセス方法がサポートされています。 ドライバーは、 [**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)を呼び出して[**IWDFDeviceInitialize2:: SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)を呼び出してから次のものを作成することによって、デバイスのすべての読み取り、書き込み、デバイスの i/o 制御要求に使用するアクセス方法を指定できます。デバイスオブジェクト。 たとえば、ドライバーが、そのデバイスの1つの読み取りおよび書き込み要求に対してバッファリングされた i/o メソッドの設定を指定した場合、 [UMDF driver ホストプロセス](umdf-driver-host-process.md)は、そのデバイスのドライバーに対して読み取りおよび書き込み要求を行うときに、バッファーされた i/o メソッドを使用します。 ドライバーでダイレクト i/o の優先順位を指定した場合、UMDF は直接 i/o を使用できます (ただし、そうでない場合もあります)。 UMDF が直接 i/o を使用する場合の詳細については、「 [umdf で I/o 要求のバッファーアクセス方法を選択する方法](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)」を参照してください。

ドライバーでサポートされているデバイスごとに、ドライバーは、バッファー内の i/o、直接 i/o、またはバッファーまたはデバイスの直接 i/o のいずれかの設定を指定できます。 このドライバーでは、読み取り要求と書き込み要求に対して1種類のアクセス方法を指定できます。また、デバイスの i/o 制御要求に対して別の種類のアクセス方法を指定することもできます。 ドライバーでアクセス方法の設定が指定されていない場合、UMDF はバッファーされたメソッドを使用します。

デバイス i/o 制御要求の場合、i/o 制御コード (IOCTL) はバッファーアクセスメソッドを指定します。 (Ioctl がアクセス方法を指定する方法の詳細については、「 [I/o 制御コードの定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)」を参照してください)。ただし、UMDF が使用するアクセスメソッドは、IOCTL が指定するアクセスメソッドと一致しない可能性があります。

-   バージョン1.9 より前の UMDF バージョンでは、UMDF は常に、すべての i/o 制御要求に対してバッファーされたアクセスメソッドを使用します。

-   、IOCTL がバッファー i/o を指定する場合、UMDF バージョン1.9 以降では、バッファーされた i/o アクセスメソッドが使用されます。 IOCTL が直接 i/o を指定し、ドライバーが[**IWDFDeviceInitialize2:: SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)を呼び出して、ダイレクト i/o の優先順位が設定されていることを示している場合、または、「 [umdf がバッファーを選択する方法」の説明に従って、umdf i/o を使用している可能性があります。I/o 要求のアクセスメソッド](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)。 "バッファーに接続されていない i/o およびダイレクト i/o" メソッドを指定する Ioctl をサポートする方法の詳細については、「 [Umdf ドライバーでのバッファー i/o と直接 i/o の両方を使用する](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)」を参照してください。

### <a href="" id="specifying-a-buffer-retrieval-mode"></a>バッファー取得モードの指定

バージョン1.9 より前の UMDF バージョンでは、umdf は、i/o 要求を受信するとすぐに、ドライバーで i/o 要求のバッファーを使用できるようにします (これは、umdf[ドライバーホストプロセス](umdf-driver-host-process.md)にバッファーをコピーすることによって行われます)。 このバッファー取得モードは、*即時取得*と呼ばれます。 エラーが発生した場合、UMDF はエラー状態値を使用して i/o 要求を完了し、ドライバーに i/o 要求を配信しません。

UMDF バージョン1.9 以降では、即時取得モードと*遅延取得*モードの両方がサポートされています。 遅延取得モードでは、ドライバーがバッファーにアクセスしようとするまで、i/o 要求のバッファーがドライバーホストプロセスにコピーされます。 エラーが発生した場合、バッファーアクセス関数は、ドライバーにエラー状態の値を返します。

ドライバーは、各デバイスに対して[**IWDFDeviceInitialize2:: SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)を呼び出すときに、バッファー取得モードを指定できます。 次の規則を使用します。

-   ドライバーがダイレクト i/o アクセス方法を指定する場合は、遅延取得モードも指定する必要があります。 ダイレクト i/o は、遅延取得でのみ機能します。

-   UMDF バージョン1.9 以降で実行するように記述されているすべてのドライバーでは、ドライバーがバッファーまたは直接 i/o アクセス方法を選択したかどうかにかかわらず、すべての i/o 要求に対して遅延取得モードを指定する必要があります。 遅延取得では、ドライバーが使用しないバッファーにアクセスしないため、パフォーマンスが向上します。

ドライバーでバッファー取得モードが指定されていない場合、UMDF はすぐに取得を使用します。

ドライバースタック内のすべての UMDF ベースのドライバーは、同じ取得モードを使用する必要があります。 一部のドライバーですぐに取得を指定し、一部のドライバーで遅延取得を指定した場合、UMDF ではすぐに取得が使用されます。

### <a href="" id="how-umdf-chooses-a-buffer-access-method-for-an-i-o-request"></a>UMDF が i/o 要求のバッファーアクセス方法を選択する方法

[**IWDFDeviceInitialize2:: SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)を呼び出すときにドライバーが指定するアクセス方法は、UMDF が使用するものではない可能性があります。 UMDF では、次の規則を使用して、使用するアクセス方法を決定します。

-   ドライバースタック内のすべての UMDF ベースのドライバーは、デバイスのバッファーにアクセスするために同じ方法を使用する必要があります。 UMDF によって、一部のドライバーでバッファー i/o またはデバイスのダイレクト i/o が使用されていると判断されたが、他のドライバーがそのデバイスに対してバッファリングされた i/o のみを優先する場合、UMDF はすべてのドライバーにバッファー i/o を使用します。 1つまたは複数のスタックのドライバーがバッファー内 i/o のみを優先し、他のドライバーが直接 i/o を優先する場合、UMDF はシステムイベントログにイベントを記録し、ドライバースタックを開始しません。

    ドライバーは[**IWDFDevice2:: GetDeviceStackIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-getdevicestackiotypepreference)を呼び出して、UMDF によってデバイスの読み取り/書き込み要求と i/o 制御要求に割り当てられたバッファーアクセスメソッドを特定できます。

-   場合によっては、ドライバーは**IWDFDeviceInitialize2:: SetIoTypePreference**を呼び出すときにダイレクト i/o の優先順位を指定しますが、最適なパフォーマンスを得るために、UMDF は1つ以上のデバイスの要求に対してバッファーされた i/o を使用します。 たとえば、UMDF では、直接アクセス用のバッファーをマップするよりも高速にデータをドライバーのバッファーにコピーできる場合は、小さなバッファーにバッファー i/o を使用します。

    必要に応じて、フレームワークが直接 i/o を使用する最小のバッファーサイズを決定するために使用する REG\_DWORD 型の**Directtransferthreshold**レジストリ値を設定できます。 通常は、最適なパフォーマンスを提供する値がフレームワークによって使用されるため、このレジストリ値を指定する必要はありません。 **Directtransferthreshold**値は、デバイスの**デバイスパラメーター\\wudf**サブキーの下にあります。このサブキーは、デバイスの[ハードウェアキー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)の下にあります。

    このフレームワークでは、 **Directtransferthreshold**に指定した値に基づいてしきい値を決定するために、次の規則を使用します。 指定された数値は、4096の**ページ\_サイズ**を想定しています。これは、Itanium ベースのシステムを除き、有効です。

    -   **Directtransferthreshold**を 8192 (または **\_\* ページサイズ**) 以下の値に設定すると、フレームワークによってしきい値が8192に設定されます。 このフレームワークでは、8192バイト未満のバッファーにはバッファー i/o、8192バイト以上のバッファーにはダイレクト i/o が使用されます。

    -   **Directtransferthreshold**を8192より大きい値に設定すると、フレームワークは**ページ\_サイズ**の次の倍数に切り上げます。 ここでも、フレームワークでは、しきい値より小さいバッファーの場合はバッファー i/o を使用し、しきい値以上の場合はバッファーの直接 i/o を使用します。

-   UMDF は、メモリページの境界で開始および終了するバッファー領域に対してのみ、direct i/o を使用します。 バッファーの先頭または末尾がページの境界上にない場合、UMDF はバッファーのその部分に対してバッファーされた i/o を使用します。 言い換えると、複数の i/o 要求で構成される大規模なデータ転送の場合、UMDF はバッファー i/o とダイレクト i/o の両方を使用することがあります。

-   デバイス i/o 制御要求の場合、UMDF は直接 i/o を指定するのは、i/o 制御コード (IOCTL) が直接 i/o を指定し、デバイスの UMDF ベースのすべてのドライバーが直接アクセスを指定するために**IWDFDeviceInitialize2:: SetIoTypePreference**を呼び出した場合のみです。b.

ドライバーは、バッファーアクセス方法に関係なく、同じセットの要求オブジェクトメソッドを使用してデータバッファーにアクセスします。 そのため、ほとんどのドライバーでは、通常、UMDF がバッファー i/o を使用しているかどうか、または i/o 要求に直接 i/o を使用しているかどうかを知る必要はありません。

### <a href="" id="how-a-driver-can-obtain-the-access-method-for-an-i-o-request"></a>ドライバーが i/o 要求のアクセス方法を取得する方法

場合によっては、アクセス方法がわかっていれば、デバイスとドライバーのパフォーマンスを向上させることができます。 このような場合、ドライバーは[**IWDFIoRequest2:: GetEffectiveIoType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-geteffectiveiotype)を呼び出して、i/o 要求のバッファーアクセス方法を取得できます。

たとえば、通常は直接 i/o を使用する高スループットデバイスを考えてみます。 ドライバーは直接 i/o を使用しているため、パラメーターを検証する前に、アプリケーションが指定したパラメーターをローカルドライバーのメモリにコピーして、検証後にアプリケーションがパラメーターを変更しないようにする必要があります。

ドライバーはバッファー内の i/o を使用するバッファーを受け取ることがあり、バッファーされた i/o バッファーは既にコピーされているため、アプリケーションはデータを変更できず、ドライバーは検証の前にパラメーターをコピーする必要がありません。 そのため、ドライバーは、各要求のバッファーアクセス方法を確認して、検証する前にパラメーターをコピーする必要があるかどうかを判断する必要があります。

### <a href="" id="using-buffered-i-o-in-umdf-drivers"></a>UMDF ドライバーでのバッファーされる i/o の使用

ドライバーがバッファー内 i/o を使用している場合、UMDF 動作は要求の種類によって異なります。 読み取り要求と書き込み要求の場合、ドライバーホストプロセスは、ドライバーがアクセスできる1つの中間バッファーを作成します。

書き込み要求の場合、ドライバーのホストプロセスは、ドライバースタックを呼び出す前に、呼び出し元のアプリケーションの入力バッファーから入力情報を転送します。 通常、ドライバーは中間バッファーから入力情報を読み取り、それをデバイスに書き込みます。

読み取り要求の場合、ドライバーは通常、デバイスから情報を読み取り、中間バッファーに格納します。 ドライバーホストプロセスは、中間バッファーからアプリケーションの出力バッファーに出力データをコピーします。

ただし、デバイスの i/o 制御要求では、ドライバーホストプロセスによって、ドライバーがアクセスできる2つの個別のバッファーが作成されます。 これは、WDM と KMDF ドライバーの動作とは異なります。これは、バッファー i/o を使用して送信される読み取り、書き込み、デバイス i/o 制御要求が、1つの中間バッファーにアクセスするためです。 この場合、出力バッファーには、最初は何も含まれず、ドライバーから読み取ることはできません。 また、ドライバーが入力バッファーに書き込むデータはすべて破棄され、呼び出し元のアプリケーションには返されません。

バッファリングされた i/o を選択するタイミングのガイドラインについては、「 [**WDF\_DEVICE\_IO\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)」を参照してください。

UMDF バージョン1.9 以降では、要求バッファーの即時取得または遅延取得をサポートできます。 詳細については、「 [**WDF\_DEVICE\_IO\_BUFFER\_の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_buffer_retrieval)」を参照してください。

イミディエイトバッファー取得モードを使用するドライバーは、 [**IWDFIoRequest:: GetInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)と[**IWDFIoRequest:: getinputmemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory)を使用してバッファーにアクセスする必要があります。

遅延バッファー取得モードを使用するドライバーは、 [**IWDFIoRequest2:: RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2:: RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2:: RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)を[**呼び出すことによってバッファーにアクセスできます。IWDFIoRequest2:: RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)。

### <a href="" id="using-direct-i-o-in-umdf-drivers"></a>UMDF ドライバーでの Direct i/o の使用

ドライバーが直接 i/o を使用している場合、ドライバーホストプロセスは、i/o 要求の発信元 (通常はユーザーモードアプリケーション) によって指定されたバッファー領域のアクセシビリティを確認し、バッファー領域を物理メモリにロックして、ドライバーを提供します。バッファー領域に直接アクセスできます。

ダイレクト i/o を選択するタイミングのガイドラインについては、「 [**WDF\_DEVICE\_IO\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)」を参照してください。

ドライバーは、 [**IWDFIoRequest2:: RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [**IWDFIoRequest2:: RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [**IWDFIoRequest2:: RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)、または[**IWDFIoRequest2:: RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)を呼び出すことによって、バッファーにアクセスできます。

### <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a>UMDF ドライバーでバッファーされる i/o と直接 i/o のいずれも使用しない

バッファーアクセスメソッド (バッファーに格納されていない i/o または*ダイレクト i/o メソッド*) (または、"どちらの" 方法でも省略可能) は、ドライバーがアプリケーションの要求バッファーポインターに直接アクセスできるようにします。 UMDF ベースのドライバーは、このアクセス方法を使用できません。

ただし、一部のデバイス i/o 制御コード (Ioctl) の[定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)では、要求で "指定なし" メソッドが使用されるように指定されています。 必要に応じて、UMDF は、このようなデバイス i/o 制御要求のバッファーアクセスメソッドをバッファー i/o またはダイレクト i/o に変換できます。 次の手順を使用します。

1.  ドライバーの INF ファイルの[**Inf DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)に[Umdfmethodneitheraction](specifying-wdf-directives-in-inf-files.md)ディレクティブを含めます。 ディレクティブの値を設定して、UMDF が "どちらの" アクセス方法を使用するデバイス i/o 制御要求をドライバーに渡す必要があることを示すことができます。 (それ以外の場合、UMDF は、エラー状態の値を使用してこれらの i/o 要求を完了します)。

2.  UMDF が[バッファー i/o](#using-buffered-i-o-in-umdf-drivers)または[直接](#using-direct-i-o-in-umdf-drivers)i/o に提供するオブジェクトメソッドを使用して、i/o 要求のバッファーにアクセスします。

"なし" メソッドを使用する IOCTL 要求のサポートを有効にする必要があります。これは、UMDF がアクセスメソッドをバッファー i/o またはダイレクト i/o に変換できることが確実である場合に限ります。 たとえば、IOCTL が、 [I/o 制御コードのバッファーの説明](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)に記述されているバッファー指定規則に従っていない、カスタマイズされた要求を指定した場合、UMDF はバッファーを変換できません。

 

 





