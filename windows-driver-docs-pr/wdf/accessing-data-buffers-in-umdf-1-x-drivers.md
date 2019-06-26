---
title: UMDF 1.x ドライバーでのデータ バッファーへのアクセス
description: UMDF 1.x ドライバーでのデータ バッファーへのアクセス
ms.assetid: cbd67ada-696e-403e-9b35-d8ed06a844d5
keywords:
- データ バッファーの WDK UMDF
- バッファー WDK UMDF
- 要求の WDK UMDF、データ バッファーの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4220987969081c5b918c4ee30dff3a0948b0f38
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363866"
---
# <a name="accessing-data-buffers-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのデータ バッファーへのアクセス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、読み取り、書き込み、またはデバイスの I/O 操作の要求を受け取る、要求オブジェクトには、入力バッファーまたは出力バッファー、またはその両方が含まれます。 (いくつかのデバイスの I/O 制御要求入力 2 つの入力、2 つの出力、または 2 つの入力/出力バッファー。)

入力バッファーには、ドライバーが必要な情報が含まれています。 書き込み要求、通常この情報はデータ関数ドライバーがデバイスに送信する必要があります。 デバイス I/O 制御要求では、入力バッファーには、ドライバーを実行する必要があります操作の種類を示す情報が含まれます。

出力バッファーは、ドライバーからの情報を受け取ります。 読み取り要求は、通常、この情報は関数ドライバーがデバイスから受信するデータです。 デバイス I/O 制御要求では、出力バッファーは状態または I/O が指定されている要求のコードを管理するその他の情報を受け取る可能性があります。

要求のデータ バッファーにアクセスするには、ドライバーを使用する手法は、デバイスのデータ バッファーにアクセスするため、ドライバーのメソッドに依存できます。 UMDF には、次のバッファーへのアクセス方法がサポートされています。

-   バージョン 1.9 より前の UMDF バージョンのみをサポート、 [I/O バッファー](#using-buffered-i-o-in-umdf-drivers)メソッドにアクセスします。 UMDF のこれらのバージョンを実行している UMDF ベースのドライバーでは、すべての読み取り、書き込み、およびデバイス I/O 制御要求のバッファー内の I/O メソッドのみを使用できます。 I/O 要求のデータ バッファーにアクセスする UMDF ベースのドライバーを使用する必要があります、 [ **IWDFIoRequest::GetInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)と[ **IWDFIoRequest::GetOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory)オブジェクトのメソッド。

-   UMDF バージョン 1.9 以降では、2 つのメソッドにアクセスします。 [I/O バッファー](#using-buffered-i-o-in-umdf-drivers)と[ダイレクト I/O](#using-direct-i-o-in-umdf-drivers)、UMDF ベースのドライバーを利用できます。 UMDF バージョン 1.9 向けに書かれた以降 UMDF ドライバーを使用する必要があります、 [ **IWDFIoRequest2::RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [ **IWDFIoRequest2::RetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)、または[ **IWDFIoRequest2::RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)オブジェクトのデータ バッファーにアクセスするメソッド。

3 つ目と呼ばれるメソッドにアクセス[バッファーも直接 I/O](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)、UMDF ベースを使用可能なドライバーではありませんが、UMDF は UMDF バージョンをサポートするメソッドに「も」メソッドから一部の I/O 要求を変換することができます。

ほとんどの場合は、UMDF ベースのドライバーは、バッファー内の I/O を使用しているか、ダイレクト I/O UMDF およびドライバーかどうか、データ バッファーへのアクセスに同じ UMDF オブジェクト メソッドを呼び出します。 ダイレクト I/O は、多くの場合、バッファー I/O より優れたパフォーマンスを提供します。

このトピックの次のセクションについて説明します。

-   指定する方法、[優先バッファーへのアクセス方法](#specifying-a-preferred-buffer-access-method)と[優先バッファー取得モード](#specifying-a-buffer-retrieval-mode)

-   どの UMDF[選択](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)バッファー メソッドと取得に使用するモード

-   ドライバーのできます[取得](#how-a-driver-can-obtain-the-access-method-for-an-i-o-request)UMDF を使用しているバッファーへのアクセス メソッド

-   使用するためのガイドライン、[バッファー](#using-buffered-i-o-in-umdf-drivers)、[直接](#using-direct-i-o-in-umdf-drivers)、および[バッファーも直接](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)バッファーへのアクセス方法

### <a href="" id="specifying-a-preferred-buffer-access-method"></a> 優先バッファーへのアクセス方法を指定します。

UMDF バージョン 1.9 以降では、バッファーとダイレクトの両方の I/O アクセス方式をサポートします。 ドライバーが呼び出すことによって、すべてのデバイスの読み取り、書き込み、およびデバイス I/O 制御要求に使用する場合、アクセスする方法を指定できます[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)呼び出す前に[ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)デバイス オブジェクトを作成します。 たとえば、ドライバーの基本設定を指定する場合のバッファー内の I/O メソッドのみ読み取りおよび書き込み要求、そのデバイスのいずれかの[UMDF ドライバーのホスト プロセス](umdf-driver-host-process.md)使用に配信するとき、バッファー内の I/O メソッドの読み取りし、書き込みを要求しますそのデバイスのドライバーです。 ドライバーは、ダイレクト I/O の優先順位を指定する場合 UMDF できます (はない可能性があります) を使用して、ダイレクト I/O。 UMDF がダイレクト I/O を使用する場合の詳細については、次を参照してください。 [UMDF がバッファーへのアクセス メソッドを選択、I/O 要求の](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)します。

ドライバーをサポートするデバイスごとに、ドライバーは、バッファー内の I/O、ダイレクト I/O、またはいずれかのバッファーの基本設定を指定またはデバイスのダイレクト I/O。 ドライバーでは、読み取りのアクセス方法の 1 つのタイプを指定でき、要求とデバイスの I/O 制御要求のためのアクセス方法の別の型を記述することができます。 ドライバーではアクセス メソッドの基本設定を指定しない場合、UMDF には、バッファー内のメソッドが使用されます。

デバイス I/O 制御要求では、I/O 制御コード (IOCTL) バッファーのアクセス方法を指定します。 (Ioctl でアクセス方法を指定する方法の詳細については、次を参照してください[I/O 制御コードを定義する](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。)。ただし、UMDF を使用するアクセスの方法では、IOCTL が示すアクセス方法とは一致可能性があります。

-   前のバージョン 1.9 UMDF バージョンでは、UMDF は常にすべての I/O 制御要求をバッファー内のアクセス方法を使用します。

-   UMDF バージョン 1.9 以降では、IOCTL がバッファー内の I/O を指定する場合、バッファー内の I/O アクセス メソッドを使用します。 IOCTL がダイレクト I/O を指定する場合と、ドライバーを呼び出す場合[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)ダイレクト I/O ダイレクト I/O、UMDF の基本設定を使用または使用してのことを示すバッファーI/O、」の説明に従って[UMDF がバッファーへのアクセス メソッドを選択、I/O 要求の](#how-umdf-chooses-a-buffer-access-method-for-an-i-o-request)します。 UMDF が Ioctl「バッファー内の I/O もダイレクト I/O でもない」メソッドの指定をサポートする方法については、次を参照してください。 [I/O を使用していないバッファーも UMDF ドライバーでのダイレクト I/O](#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)します。

### <a href="" id="specifying-a-buffer-retrieval-mode"></a> バッファー取得モードを指定します。

前のバージョン 1.9 UMDF バージョンでは、UMDF 常に、I/O 要求のバッファーを使用できるように、ドライバー (にバッファーをコピーすることによって、 [UMDF ドライバーのホスト プロセス](umdf-driver-host-process.md)) UMDF が I/O 要求を受信するようになります。 このバッファー取得モードと呼びます*迅速に検索できる*します。 障害が発生した場合、UMDF はエラー状態の値を持つ I/O 要求を完了し、ドライバーには、I/O 要求を配信しません。

UMDF バージョン 1.9 以降は、両方の即時の取得をサポートし、*の取得を遅延*モード。 遅延の取得モードは、ドライバーが、バッファーにアクセスしようとするまで、ドライバーのホスト プロセスには、I/O 要求のバッファーのコピーを延期します。 障害が発生した場合、バッファーのアクセス関数は、ドライバーにエラー状態値を返します。

呼び出すときに、ドライバーがバッファー取得のモードを指定できます[ **IWDFDeviceInitialize2::SetIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)デバイスごとにします。 次の規則を使用します。

-   場合は、ドライバーでは、遅延の取得モードを指定する必要がありますもダイレクト I/O アクセス メソッドを指定します。 ダイレクト I/O は、遅延の取得でのみ機能します。

-   すべてのドライバーは UMDF バージョン 1.9 で実行するように記述し、後でする必要がありますモードの指定、遅延の取得、すべての I/O 要求のドライバーにバッファーまたはダイレクト I/O を選択するかどうかをメソッドにアクセスします。 遅延の取得は、ドライバーを使用しないバッファーにアクセスしないため、パフォーマンスの向上を提供します。

ドライバーではバッファー取得のモードを指定しない場合、UMDF には、迅速に検索できるが使用されます。

ドライバー スタック内のすべての UMDF ベースのドライバーでは、同じ検索モードを使用する必要があります。 一部のドライバーが迅速に検索できるを指定し、いくつかの指定の遅延の取得場合、UMDF には、迅速に検索できるが使用されます。

### <a href="" id="how-umdf-chooses-a-buffer-access-method-for-an-i-o-request"></a> UMDF が I/O 要求のバッファーのアクセス方法を選択する方法

ドライバーでは、呼び出し時に指定するアクセス メソッド[ **IWDFDeviceInitialize2::SetIoTypePreference**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdeviceinitialize2-setiotypepreference)UMDF を使用する 1 つができない可能性があります。 UMDF は、次の規則を使用して判断するために使用するメソッドへのアクセスします。

-   ドライバー スタック内のすべての UMDF ベースのドライバーでは、デバイスのバッファーにアクセスするため、同じメソッドを使用する必要があります。 UMDF では、他のドライバーの使用のみバッファー I/O デバイスの中に、一部のドライバーでバッファー内の I/O またはデバイスのダイレクト I/O のいずれかを好むことを決定、UMDF はすべてのドライバー バッファー内の I/O を使用します。 1 つ以上のスタックのドライバーは、ダイレクト I/O だけを好む開発者も、バッファー内の I/O だけを必要に応じて、UMDF は、システム イベント ログにイベントが記録し、ドライバー スタックを開始できません。

    ドライバーが呼び出せる[ **IWDFDevice2::GetDeviceStackIoTypePreference** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-getdevicestackiotypepreference) UMDF がデバイスの読み取り/書き込みに割り当てられているバッファーへのアクセス方法を決定する要求と I/O 制御要求。

-   呼び出すときによっては、ドライバーがダイレクト I/O の優先順位を指定**IWDFDeviceInitialize2::SetIoTypePreference**、最適なパフォーマンスを UMDF がデバイスの要求の 1 つ以上のバッファー内の I/O を使用します。 たとえば、UMDF は、ドライバーのバッファーへのデータ コピーに直接アクセスするためのバッファーをマップできるよりも高速、場合、小さなバッファーのバッファー内の I/O を使用します。

    必要に応じて、21 を設定することができます\_DWORD に型指定された**DirectTransferThreshold**フレームワークを使用して、フレームワークがダイレクト I/O を使用する最小バッファー サイズを確認するレジストリ値。 通常、フレームワークは、最適なパフォーマンスを提供する値を使用するために、このレジストリ値を提供する必要はありません。 **DirectTransferThreshold**値が、デバイスの下にある**デバイス パラメーター\\WUDF**サブキーで、デバイスの下にある[ハードウェア キー](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-registry-trees-and-keys)します。

    フレームワークでは、次の規則を使用してで指定した値に基づいて、しきい値を決定**DirectTransferThreshold**します。 指定された数値、**ページ\_サイズ**4096、Itanium ベース システム以外の有効なのです。

    -   設定した場合**DirectTransferThreshold**任意未満の値以上 8192 (2 または\***ページ\_サイズ**)、フレームワークは、8192、しきい値を設定します。 フレームワークでは、8192 (バイト単位) より小さいバッファーのバッファー内の I/O とダイレクト I/O が 8,192 バイト以上のバッファーを使用します。

    -   設定した場合**DirectTransferThreshold** 8192 より大きい値はすべてに、フレームワークに切り上げますの正確な倍数**ページ\_サイズ**します。 ここでも、フレームワークを使用、しきい値より小さいバッファーのバッファー内の I/O とダイレクト I/O のしきい値以上のバッファー。

-   UMDF を開始し、メモリ ページの境界で終了するバッファー領域のみのダイレクト I/O を使用します。 先頭またはバッファーの末尾がページの境界上に入らない場合 UMDF はバッファーの部分のバッファー内の I/O を使用します。 つまり、UMDF バッファー内の I/O とダイレクト I/O の両方オプションは使用のいくつかの I/O 要求で構成される大規模なデータ転送。

-   デバイス I/O 制御の要求の UMDF はダイレクト I/O I/O 制御コード (IOCTL) は、ダイレクト I/O を指定し、ドライバーが呼び出されている場合は、すべてのデバイスの UMDF ベースである場合にのみ**IWDFDeviceInitialize2::SetIoTypePreference**を指定するには直接アクセスするメソッド。

ドライバーは、バッファーのアクセス方法に関係なく、データ バッファーへのアクセスに同じ一連の要求オブジェクトのメソッドを使用します。 そのため、ほとんどのドライバー通常必要はないかどうか UMDF はまたはを使用してバッファー内の I/O ダイレクト I/O の I/O 要求を把握します。

### <a href="" id="how-a-driver-can-obtain-the-access-method-for-an-i-o-request"></a> ドライバーが I/O 要求のアクセス方法を取得する方法

いくつかの場合、アクセス方法がわかっている場合、デバイスとドライバーのパフォーマンスを向上できます。 このような場合、ドライバーを呼び出すことができます[ **IWDFIoRequest2::GetEffectiveIoType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-geteffectiveiotype) I/O 要求をバッファーへのアクセス メソッドを取得します。

たとえば、通常ダイレクト I/O を使用する高スループット デバイスがあるとします。 ダイレクト I/O を使用しているため、ドライバーは、検証後に、パラメーターは、アプリケーションによって変更しないことを確認する、パラメーターを検証する前にローカル ドライバーのメモリをアプリケーションで指定されたパラメーターをコピーする必要があります。

バッファー内の I/O を使用するため、ドライバーでは、バッファーを受け取ることがあります、ため、バッファー内の I/O バッファーが既にコピーされて、アプリケーション データは変更できませんし、ドライバーがそれらを検証する前にパラメーターをコピーする必要はありません。 そのため、ドライバーは、それらを検証する前にパラメーターをコピーする必要がありますを決定する各要求のバッファーのアクセス方法を確認する必要があります。

### <a href="" id="using-buffered-i-o-in-umdf-drivers"></a> UMDF ドライバーでバッファー内の I/O の使用

バッファー内の I/O には、ドライバーを使用している場合、UMDF 動作は、要求の種類によって異なります。 読み取りと書き込みを要求すると、ドライバーのホスト プロセスは、ドライバーがアクセスできる 1 つの中間バッファーを作成します。

書き込み要求の場合は、ドライバーのホスト プロセスは、ドライバー スタックを呼び出す前に、呼び出し元アプリケーションの入力バッファーから入力情報を転送します。 通常、ドライバーは、中間バッファーからの入力情報を読み取るし、デバイスへの書き込み。

読み取り要求は、ドライバーは通常、デバイスから情報を読み取るし、中間バッファーに格納します。 ドライバーのホスト プロセスは、アプリケーションの出力バッファーに中間バッファーからの出力データをコピーします。

デバイス I/O コントロール要求、ただし、ドライバーのホスト プロセスを作成、ドライバーがアクセスできる 2 つの独立したバッファーします。 WDM、KMDF ドライバー、I/O 制御の要求を使用して送信される読み取り、書き込み、およびデバイスの I/O の結果に、ドライバーが 1 つ、中間バッファーにアクセスするバッファリングの動作は異なることに注意してください。 この場合、出力バッファーが最初に、何もと、そこからドライバーを読み取りません。 さらに、ドライバーは、入力バッファーに書き込むデータが破棄され、呼び出し元アプリケーションに返されません。

選択するタイミングに関するガイドラインは、I/O バッファーを参照してください[ **WDF\_デバイス\_IO\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)します。

UMDF バージョン 1.9 以降では、要求のバッファーの即時と遅延のいずれかの取得をサポートできます。 詳細については、次を参照してください。 [ **WDF\_デバイス\_IO\_バッファー\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi_types/ne-wudfddi_types-_wdf_device_io_buffer_retrieval)します。

イミディ エイト バッファー取得モードを使用するドライバーを使用する必要があります[ **IWDFIoRequest::GetInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getinputmemory)と[ **IWDFIoRequest::GetOutputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getoutputmemory) 、バッファーにアクセスします。

遅延バッファー取得モードを使用するドライバーは、バッファーを呼び出すことによってアクセスできる[ **IWDFIoRequest2::RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [ **IWDFIoRequest2:。RetrieveInputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)、または[ **IWDFIoRequest2:。RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)します。

### <a href="" id="using-direct-i-o-in-umdf-drivers"></a> UMDF ドライバーでのダイレクト I/O の使用

場合は、ドライバーは、ダイレクト I/O を使用して、ドライバーのホスト プロセスが指定すると、I/O 要求 (通常はユーザー モード アプリケーション) の実行者が物理メモリにバッファー領域をロックし、ドライバーを提供するバッファー領域のアクセシビリティを確認しますバッファー領域に直接アクセスします。

選択するタイミングに関するガイドラインはダイレクト I/O を参照してください[ **WDF\_デバイス\_IO\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi_types/ne-wudfddi_types-_wdf_device_io_type)します。

ドライバーは、バッファーを呼び出すことによってアクセスできる[ **IWDFIoRequest2::RetrieveInputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputbuffer)、 [ **IWDFIoRequest2::RetrieveInputMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveinputmemory)、 [ **IWDFIoRequest2::RetrieveOutputBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputbuffer)、または[ **IWDFIoRequest2::RetrieveOutputMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-retrieveoutputmemory)します。

### <a href="" id="using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers"></a> UMDF ドライバーで I/O もダイレクト I/O バッファーを使用しても

呼ばれるバッファーへのアクセス方法、 *I/O もダイレクト I/O メソッドをバッファーも*(または略して「も」メソッド) ドライバーのアプリケーションの要求のバッファー ポインターに直接アクセスを許可します。 UMDF ベースのドライバーでは、このアクセス方法を使用できません。

ただし、[定義](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)コード (Ioctl) が、要求が「も」メソッドを使用することを指定の一部のデバイスの I/O 制御します。 必要に応じて、UMDF は、このようなデバイスの I/O 制御要求のバッファーへのアクセス メソッド I/O バッファーへの変換またはダイレクト I/O。 次の手順を使用します。

1.  含める、 [UmdfMethodNeitherAction](specifying-wdf-directives-in-inf-files.md)ディレクティブで、 [ **INF DDInstall セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)ドライバーの INF ファイル。 ディレクティブの UMDF ドライバーへのアクセス「も」方法を使用するデバイス I/O 制御要求を渡す必要があることを示す値を設定することができます。 (それ以外の場合、UMDF がエラー状態の値を持つこれらの I/O 要求を完了する。)

2.  UMDF には、オブジェクトのメソッドを使用して、I/O 要求のバッファーにアクセス[I/O バッファー](#using-buffered-i-o-in-umdf-drivers)または[ダイレクト I/O](#using-direct-i-o-in-umdf-drivers)します。

UMDF がバッファー内の I/O またはダイレクト I/O アクセス メソッドを変換できる場合にのみ、「も」メソッドを使用する IOCTL 要求のサポートを有効にする必要があります。 IOCTL で説明されているバッファーの仕様の規則に従っていないカスタマイズされた要求を指定する場合など、 [I/O 制御コードの説明をバッファー](https://docs.microsoft.com/windows-hardware/drivers/kernel/buffer-descriptions-for-i-o-control-codes)UMDF にバッファーを変換できません。

 

 





