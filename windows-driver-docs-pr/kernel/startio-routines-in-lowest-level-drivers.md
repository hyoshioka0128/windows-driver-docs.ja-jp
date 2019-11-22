---
title: 最下位レベル ドライバーの StartIo ルーチン
description: 最下位レベル ドライバーの StartIo ルーチン
ms.assetid: f79f8929-bcf4-46a2-bf0e-0f8fb0720dd9
keywords:
- StartIo ルーチン、最下位レベルのドライバー
- I/o 制御要求の WDK カーネル
- バッファーされる i/o WDK カーネル
- ダイレクト i/o WDK カーネル
- WDK Irp の同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7a9cd9c287fa5e45cfbd9f884da4bb827ac549
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836233"
---
# <a name="startio-routines-in-lowest-level-drivers"></a>最下位レベル ドライバーの StartIo ルーチン





I/o マネージャーによるドライバーのディスパッチルーチンの呼び出しは、デバイス i/o 要求を満たすための最初の段階です。 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンは2番目の段階です。 *StartIo*ルーチンを使用するすべてのデバイスドライバーは、 [*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンと[*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出す可能性があります。通常は、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでサポートされている i/o 制御コードのサブセットです。 **Iostartpacket**ルーチンは、デバイスのシステムによって提供されるデバイスキューに irp を追加します。または、キューが空の場合、は直ちにドライバーの*StartIo*ルーチンを呼び出して irp を処理します。

ドライバーの*StartIo*ルーチンが呼び出されたときに、ターゲットデバイスがビジー状態でないと見なすことができます。 これは、i/o マネージャーが2つの状況下で*StartIo*を呼び出すためです。いずれかのドライバーのディスパッチルーチンが**Iostartpacket**を呼び出しましたが、デバイスキューが空であるか、またはドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチンが別の要求を完了していて、次の IRP をデキューするために[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出しました。

最上位レベルのデバイスドライバーの*StartIo*ルーチンが呼び出される前に、そのドライバーのディスパッチルーチンは、必要に応じて、 *StartIo*にキューされている IRP に有効なマップ済みバッファーアドレスを設定するために、ユーザーバッファーを調査し、ロックダウンする必要があります。ルーチン. 最上位レベルのデバイスドライバーによって、ダイレクト i/o 用にデバイスオブジェクトが設定されている場合 (またはバッファーされていない場合や直接 i/o の場合)、ドライバーはユーザーバッファーの*StartIo*ルーチンへのロックダウンを遅らせることはできません。すべての*StartIo*ルーチンは、IRQL = DISPATCH\_レベルで任意のスレッドコンテキストで呼び出されます。

   ドライバーの*StartIo*ルーチンによってアクセスされるバッファーメモリは、ロックダウンするか、常駐システム領域のメモリから割り当てて、任意のスレッドコンテキストでアクセスできるようにする必要がある**ことに注意**してください。

 

一般に、すべての下位レベルのデバイスドライバーの*StartIo*ルーチンは、入力 IRP を使用して[**Ioget entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出し、その後、i/o 操作を開始するために必要な要求固有の処理を実行します。ドライブ. 要求固有の処理には、次のものが含まれます。

-   ドライバーによって管理される現在の要求に関する状態情報を設定または更新します。 状態情報は、ターゲットデバイスオブジェクトのデバイス拡張機能、またはドライバーによって割り当てられた非ページプール内の他の場所に格納されることがあります。

    たとえば、デバイスドライバーが現在の転送操作で InterruptExpected ブール値を保持している場合、その*StartIo*ルーチンによってこの変数が**TRUE**に設定されることがあります。 ドライバーが現在の操作のタイムアウトカウンターを保持している場合、その*StartIo*ルーチンがこの値を設定しているか、 *StartIo*ルーチンがドライバーの[*customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンをキューに入れている可能性があります。

    *StartIo*ルーチンが状態情報または[ハードウェアリソース](hardware-resources.md)へのアクセスを他のドライバールーチンと共有している場合は、状態情報またはリソースがスピンロックによって保護されている必要があります。 (「[スピンロック](spin-locks.md)」を参照してください)。

    *StartIo*ルーチンが、ドライバーの[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンを使用して状態情報またはリソースへのアクセスを共有する場合、 *StartIo*は[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用して、にアクセスする[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを呼び出す必要があります。状態またはリソース情報。 (「[クリティカルセクションの使用」を](using-critical-sections.md)参照してください)。

-   Irp の処理中にドライバーがデバイス i/o エラーをログに記録する必要がある場合に備えて、シーケンス番号を IRP に割り当てます。

    詳細については、「[ログエラー](logging-errors.md) 」を参照してください。

-   必要に応じて、ドライバーの i/o スタック位置のパラメーターをデバイス固有の値に変換します。

    たとえば、ディスクドライバーは、転送操作のために物理ディスクアドレスへの開始セクターまたはバイトオフセットを計算する必要があり、要求された転送の長さが特定のセクター境界を越えるか、物理デバイス。

-   ドライバーがリムーバブルメディアデバイスを制御している場合、i/o 用にデバイスをプログラミングする前にメディアの変更を確認し、メディアが変更された場合はそのファイルシステムに通知します。

    詳細については、「[リムーバブルメディアのサポート](supporting-removable-media.md)」を参照してください。

-   デバイスで DMA が使用されている場合は、[入力/出力の手法](i-o-programming-techniques.md)で説明されているように、要求された**長さ**(転送されるバイト数) を部分転送操作に分割する必要があるかどうかを確認します。密結合の上位レベルのドライバーでは、デバイスドライバーに対して大きな転送が行われないと仮定しています。

    また、このようなデバイスドライバーの*StartIo*ルーチンは、 [**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)を呼び出すこともできます。また、ドライバーがパケットベースの DMA を使用する場合は、ドライバーの[*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンで[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出す必要があります。

    詳細については、「[アダプターオブジェクトと DMA](adapter-objects-and-dma.md)」、および「[キャッシュの一貫性の維持](maintaining-cache-coherency.md)」を参照してください。

-   デバイスで PIO が使用されている場合は、 **&gt;** irp の irp に記述されているバッファーのベース仮想アドレスを[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)のシステムスペースアドレスにマップします。

    読み取り要求の場合、PIO 操作を開始する前に、デバイスドライバーの*StartIo*ルーチンが[**Keflushiobuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keflushiobuffers)の呼び出しを行うことができます。 詳細については、「[キャッシュの一貫性の維持](maintaining-cache-coherency.md)」を参照してください。

-   WDM 以外のドライバーがコントローラーオブジェクトを使用している場合は、 [**IoAllocateController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioallocatecontroller)を呼び出して[ *、そのコントローラーコントローラーを*](https://msdn.microsoft.com/library/windows/hardware/ff542049)登録します。

-   ドライバーがキャンセル可能な Irp を処理する場合は、入力 IRP が既にキャンセルされているかどうかを確認します。

-   入力 IRP を完了に処理する前にキャンセルできる場合、 *StartIo*ルーチンは irp とドライバーの[*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)ルーチンのエントリポイントを使用して[**iosetcancelroutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)を呼び出す必要があります。 *StartIo*ルーチンは、 **iosetcancelroutine**の呼び出しのキャンセルスピンロックを取得する必要があります。 また、ドライバーで[**Iosetstartioattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iosetstartioattributes)を使用して、 *StartIo*ルーチンの*キャンセル*不可能な属性を**TRUE**に設定することもできます。 これにより、 [**Iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)の呼び出しによって*StartIo*に渡された IRP をシステムがキャンセルしようとするのを防ぎます。

一般的な規則として、バッファー i/o を使用するドライバーには、直接 i/o を使用するものよりも単純な*StartIo*ルーチンがあります。 バッファーされた i/o を使用するドライバーは、転送要求ごとに少量のデータを転送します。また、直接 i/o (DMA または PIO) を使用するドライバーは、システムメモリ内の物理的なページ境界にまたがることができるロックダウンバッファーとの間で大量のデータを転送します。

物理デバイスドライバーの上位に階層化された上位レベルのドライバーは、通常、それぞれのデバイスドライバーのデバイスオブジェクトと一致するようにデバイスオブジェクトを設定します。 ただし、最上位レベルのドライバー (特にファイルシステムドライバー) では、ダイレクトもバッファリングもされていない i/o に対してデバイスオブジェクトを設定できます。

バッファー内の i/o 用にデバイスオブジェクトを設定するドライバーは、i/o マネージャーを使用して、ドライバーに送信されるすべての Irp に有効なバッファーを渡すことができます。 ダイレクト i/o 用にデバイスオブジェクトを設定する低レベルのドライバーでは、チェーン内の最上位レベルのドライバーを使用して、中間ドライバーを介して送信されるすべての Irp 内の有効なバッファーを下位レベルの下位デバイスドライバーに渡すことができます。

### <a name="using-buffered-io-in-startio-routines"></a>StartIo ルーチンでのバッファーされる i/o の使用

ドライバーの[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、または[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンによって要求が有効であると判断され、 [**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)が呼び出されると、i/o マネージャーはドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを呼び出して IRP を処理します。デバイスキューが空の場合、直ちに。 キューが空でない場合は、 **Iostartpacket**が IRP をキューに置いています。 最終的には、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンから[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出すと、i/o マネージャーによって IRP がデキューされ、ドライバーの*StartIo*ルーチンが呼び出されます。

*StartIo*ルーチンは[**Ioget entilocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出し、要求を満たすために実行する必要がある操作を決定します。 I/o 要求を実行するために物理デバイスをプログラミングする前に、必要な方法で IRP を前処理します。

物理デバイス (またはデバイス拡張機能) へのアクセスを[*InterruptService*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kservice_routine)ルーチンと同期する必要がある場合は、 *StartIo*ルーチンが[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを呼び出して、必要なデバイスプログラミングを実行する必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

バッファーされた i/o を使用する物理デバイスドライバーは、i/o マネージャーによって割り当てられたシステム領域バッファーとの間でデータを転送します。これは、ドライバーが**irp-&gt;AssociatedIrp**の各 irp で検出します。

### <a name="using-direct-io-in-startio-routines"></a>StartIo ルーチンでの Direct i/o の使用

ドライバーの[*DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、 [*DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)、または[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンによって要求が有効であると判断され、 [**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)が呼び出されると、i/o マネージャーはドライバーの*StartIo*ルーチンを呼び出して IRP を処理します。デバイスキューが空の場合、直ちに。 キューが空でない場合は、 **Iostartpacket**が IRP をキューに置いています。 最終的には、ドライバーの[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンから[**iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出すと、i/o マネージャーによって IRP がデキューされ、ドライバーの*StartIo*ルーチンが呼び出されます。

*StartIo*ルーチンは[**Ioget entilocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出し、要求を満たすために実行する必要がある操作を決定します。 大量の DMA 転送要求を部分転送範囲に分割し、分割する必要がある受信転送要求の**長さ**に関する状態を保存するなど、必要な方法で IRP を事前に作成します。 次に、i/o 要求を実行するように物理デバイスをプログラムします。

物理デバイス (またはデバイス拡張機能) へのアクセスをドライバーの ISR と同期する必要がある場合、 *StartIo*ルーチンでは、ドライバーによって提供される*SynchCritSection*ルーチンを使用して必要なプログラミングを実行する必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

ダイレクト i/o を使用するドライバーは、i/o 記述子リスト (MDL) によって記述されたロックダウンバッファーからデータを読み取るか、データを書き込むことができます。これは、ドライバーが irp で irp **-&gt;MdlAddress**を検出したときに発生します。 このようなドライバーでは、通常、デバイス制御要求にバッファー i/o が使用されます。 詳細については、「 [StartIo ルーチンで I/o 制御要求を処理](#ddk-handling-i-o-control-requests-in-startio-routines-kg)する」を参照してください。

MDL 型は、ドライバーが直接アクセスしない不透明な型です。 代わりに、PIO を使用するドライバーは、パラメーターとして[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer) **mdladdress**を指定して&gt;を呼び出すことによって、ユーザー空間のバッファーを再マップします。 DMA を使用するドライバーは、転送操作中にルーチンをサポートするために、 **Irp&gt;MdlAddress**も渡して、デバイスの論理範囲に再マップされたバッファーアドレスを持つようにします。

密接に結合された上位レベルのドライバーが、基になるデバイスドライバーに対して大きな DMA 転送要求を分割しない限り、最下位レベルのデバイスドライバーの*StartIo*ルーチンは、デバイスで管理できるサイズより大きい転送要求を1つずつ分割する必要があります。転送操作です。 システム dma を使用するドライバーは、システム DMA コントローラーに対して大きすぎる転送要求や、デバイスが1回の転送操作で処理する必要がある転送要求を分割するために必要です。

デバイスが下位 DMA デバイスの場合、そのドライバーは、ドライバーによって割り当てられたアダプターオブジェクト (DMA チャネルを表す) とドライバーによって提供される[*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンを使用して、システムの dma コントローラーを経由した転送を同期する必要があります。 また、バスマスタ DMA デバイスのドライバーは、ドライバーによって割り当てられたアダプターオブジェクトを使用して転送を同期する必要があります。また、システムのパケットベースの DMA サポートを使用する場合は*Adaptercontrol*ルーチンを指定する必要があり、それ以外の場合は[*AdapterListControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_list_control)ルーチンを指定する必要があります。システムのスキャッター/ギャザーサポートを使用します。

ドライバーの設計によっては、物理デバイスに対する転送およびデバイス制御操作がコントローラーオブジェクトと同期され、コントローラー[*の制御ルーチンが*](https://msdn.microsoft.com/library/windows/hardware/ff542049)提供される場合があります。

詳細については、「[アダプターオブジェクトと DMA](adapter-objects-and-dma.md)および[コントローラーオブジェクト](using-controller-objects.md)」を参照してください。

### <a href="" id="ddk-handling-i-o-control-requests-in-startio-routines-kg"></a>StartIo ルーチンでの i/o 制御要求の処理

一般に、ドライバーの*StartIo*ルーチンによる処理を続けるために、ドライバーの[*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)または[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンからは、デバイスの i/o 制御要求のサブセットのみが渡されます。 ドライバーの*StartIo*ルーチンは、デバイスの状態の変更を必要とする有効なデバイス制御要求だけを処理するか、現在のデバイスの状態に関する揮発性情報を返す必要があります。

各新しいドライバーは、同じ種類のデバイスの他のすべてのドライバーと同じセットのパブリック i/o 制御コードをサポートする必要があります。 システムは、 [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求をバッファリングされた要求として使用する、デバイスタイプ固有のパブリック i/o 制御コードを定義します。

このため、物理デバイスドライバーは、各ドライバーが irp で&gt;検出したシステム領域のバッファーとの間のデータ転送を**AssociatedIrp**のデバイス制御要求に対して行います。 ダイレクト i/o 用にデバイスオブジェクトを設定するドライバーも、バッファー内 i/o を使用して、パブリック i/o 制御コードを使用したデバイス制御要求を処理します。

各 i/o 制御コードの定義によって、その要求に対して転送されるデータがバッファリングされるかどうかが決まります。 ドライバー固有の IRP\_MJ のプライベートに定義された i/o 制御コード[ **\_内部\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)では、ペアになっているドライバー間で制御要求を実行すると、メソッドバッファー、メソッドダイレクト、またはメソッドを使用してコードを定義できません。 一般的な規則として、プライベートに定義された i/o 制御コードは、厳密に結合された上位レベルのドライバーがその要求に対してバッファーを割り当てる必要がある場合は、どちらのメソッドでも定義する必要があります。

### <a name="programming-the-device-for-io-operations"></a>I/o 操作のためのデバイスのプログラミング

通常、最下位レベルのデバイスドライバーの*StartIo*ルーチンは、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を使用してドライバーが提供する[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)を呼び出すことによって、ドライバーの ISR と共有するメモリまたはデバイスへのアクセスを同期する必要があります。ルーチン. ドライバーの*StartIo*ルーチンは、 *SynchCritSection*ルーチンを使用して、dirql の i/o の物理デバイスを実際にプログラミングします。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

**KeSynchronizeExecution**を呼び出す前に、 *StartIo*ルーチンは要求に必要なすべての前処理を行う必要があります。 前処理では、最初の部分転送範囲を計算し、他のドライバールーチンの元の要求に関する状態情報を保存することがあります。

デバイスドライバーが DMA を使用する場合、 *StartIo*ルーチンは通常、ドライバーが提供する[*adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンを使用して[**allocateadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pallocate_adapter_channel)を呼び出します。 このような状況では、 *StartIo*ルーチンは、物理デバイスを*adaptercontrol*ルーチンにプログラミングする責任を後回しにします。 さらに、 **KeSynchronizeExecution**を呼び出して、ドライバーによって提供される*SynchCritSection*ルーチンプログラムが DMA 転送用にデバイスを作成することができます。

 

 




