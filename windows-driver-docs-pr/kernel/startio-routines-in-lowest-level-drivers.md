---
title: 最下位レベルのドライバーで StartIo ルーチン
description: 最下位レベルのドライバーで StartIo ルーチン
ms.assetid: f79f8929-bcf4-46a2-bf0e-0f8fb0720dd9
keywords:
- StartIo ルーチン、最下位レベルのドライバー
- I/O 制御要求の WDK カーネル
- バッファー内の I/O の WDK カーネル
- ダイレクト I/O WDK カーネル
- WDK Irp の同期
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b100a04e9389f40d152f9c70f50760c1f0af43a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550932"
---
# <a name="startio-routines-in-lowest-level-drivers"></a>最下位レベルのドライバーで StartIo ルーチン





ドライバーのディスパッチ ルーチンへの I/O マネージャーの呼び出しは、最初の段階でデバイスの I/O 要求を満たすことです。 [ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチンは、2 番目の段階です。 すべてのデバイス ドライバー、 *StartIo*ルーチンを呼び出す可能性があります[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370)からその[ *DispatchRead* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ *DispatchWrite* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンでは、通常、I/O のサブセットの制御コードでサポートおよびその[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 **IoStartPacket**ルーチンは、デバイスのデバイスのシステム提供のキューに IRP を追加します。 または、ドライバーの呼び出し直後に、キューが空の場合*StartIo* IRP を処理するルーチン。

ドライバーの場合を想定できます*StartIo*ルーチンを呼び出すと、ターゲット デバイスがビジー状態ではありません。 これは、I/O マネージャーを呼び出すため*StartIo*下 2 つの状況は、いずれかのルーチンが呼び出されてだけ、ドライバーのディスパッチの**IoStartPacket**とデバイスのキューが空、またはドライバーの[*DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)ルーチンが完了している別の要求とが呼び出されてだけ[**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358) IRP が [次へ] をキューから削除します。

前に、 *StartIo*最上位レベルのデバイス ドライバーのルーチンを呼び出すと、ドライバーのディスパッチ ルーチンを調査および必要に応じて、有効なを設定するには、IRP のバッファーのアドレスがマップされている場合、ユーザーのバッファーにロックダウンする必要がありますがキューに登録されてその*StartIo*ルーチン。 最上位レベルのデバイス ドライバーは、ダイレクト I/O (またはバッファーもダイレクト I/O)、そのデバイス オブジェクトを設定する場合、ドライバーがユーザーのバッファーをロックを延期することはできません、 *StartIo*ルーチンはすべて*StartIo*IRQL で任意のスレッド コンテキストでルーチンを呼び出すディスパッチ =\_レベル。

**注**  へのアクセスをドライバーのメモリ バッファーのいずれかの*StartIo*ルーチンをロック ダウンされているか常駐、システム容量のメモリから割り当てられている必要があります、任意のスレッド コンテキストでアクセスできるようにする必要があります。

 

一般に、いずれかの低レベル デバイス ドライバーの*StartIo*ルーチンは、通話を担当[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174) IRP が入力内容を行うと要求固有の処理は、そのデバイス上の I/O 操作を開始する必要があります。 要求固有の処理を次に含めることができます。

-   設定するか、ドライバーは、現在の要求に関するすべての状態情報を更新します。 ターゲット デバイス オブジェクトの拡張機能でデバイスまたはドライバーによって割り当てられた非ページ プールの別の場所、状態情報は格納されている可能性があります。

    たとえば、InterruptExpected ブール値を現在の転送操作では、デバイス ドライバーはその*StartIo*ルーチンにこの変数を設定する可能性があります**TRUE**します。 ドライバーは、現在の操作のタイムアウト カウンターを保持している場合、 *StartIo*ルーチンは、この値は、セットアップ場合がありますまたは*StartIo*ルーチンは、ドライバーのキューが[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチン。

    場合、 *StartIo*ルーチンは、状態情報へのアクセスを共有または[ハードウェア リソース](hardware-resources.md)他のドライバーのルーチンでは、状態の情報やリソースをスピン ロックで保護する必要があります。 (を参照してください[スピンロック](spin-locks.md))。

    場合、 *StartIo*ルーチン、ドライバーの状態の情報やリソースへのアクセスと共有[ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチン、 *StartIo*を使用する必要があります[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)を呼び出す、 [ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)状態にアクセスするルーチンまたはリソース情報です。 (を参照してください[クリティカル セクションを使用して](using-critical-sections.md))。

-   IRP をシーケンス番号を割り当てる場合は、ドライバーは IRP の処理中にデバイス I/O エラーを記録する必要があります。

    参照してください[ログ エラー](logging-errors.md)詳細についてはします。

-   必要に応じて、変換、ドライバーの I/O では、パラメーターがデバイスに固有の値に場所をスタックかどうか。

    たとえば、ディスク ドライバーは、転送操作では、物理ディスク アドレスに開始セクターまたはバイトのオフセットを計算する必要があります、転送の要求された長さが交差するかどうか、特定の境界をセクターまたはの転送の容量を超えるその物理デバイス。

-   ドライバーは、リムーバブル メディア デバイスを制御する場合はメディアのチェック I/O のデバイスをプログラミングして、メディアが変更された場合、その上にあるファイル システムを通知する前に変更します。

    詳細については、次を参照してください。[リムーバブル メディアをサポートしている](supporting-removable-media.md)します。

-   デバイス DMA を使用する場合にチェックするかどうか、要求された**長さ**(転送されるバイト数の IRP のドライバーの I/O スタックの場所にある) で説明したように部分的な転送操作に分割する必要があります[入力/出力手法](i-o-programming-techniques.md)、密接に結合されたより高度なドライバーと仮定した場合も、デバイス ドライバーの大規模な転送が presplit されません。

    *StartIo*もこのようなデバイス ドライバーのルーチンがこの呼び出しを担当することができます[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) を呼び出すため、ドライバーがパケットに基づくDMAを使用する場合と、[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)ドライバーの[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン。

    参照してください[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)、および[キャッシュの一貫性を維持](maintaining-cache-coherency.md)、さらに詳細です。

-   デバイス PIO、バッファーの基本の仮想アドレスのマッピングを使用している場合は、IRP で説明されている**Irp -&gt;MdlAddress**、システム容量でアドレスを[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559).

    読み取り要求の場合、デバイス ドライバーの*StartIo*ルーチンが通話を担当できる[ **KeFlushIoBuffers** ](https://msdn.microsoft.com/library/windows/hardware/ff552041) PIO する前に操作を開始します。 参照してください[キャッシュの一貫性を維持](maintaining-cache-coherency.md)詳細についてはします。

-   非 WDM ドライバーは、コント ローラー オブジェクトを使用している場合は、呼び出す[ **IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)を登録するその[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン。

-   ドライバーがキャンセル可能な Irp であるかどうか、入力 IRP が既に確認を処理する場合は取り消されました。

-   完了するまで処理される前に、入力の IRP が取り消されたことができる場合、 *StartIo*ルーチンを呼び出す必要があります[ **IoSetCancelRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff549674) IRP とエントリのポイント、ドライバーの[*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742)ルーチン。 *StartIo*ルーチンは、その呼び出しをキャンセル スピン ロックを取得する必要があります**IoSetCancelRoutine**します。 また、ドライバーを使用できる[ **IoSetStartIoAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff550330)を設定する、*オブジェクト*属性、 *StartIo*ルーチンを**TRUE**します。 これにより、システムに渡された IRP をキャンセルしようとしていますから*StartIo*への呼び出しによって[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)します。

一般的な規則としてはバッファー内の I/O を使用するドライバーより簡単な*StartIo*ダイレクト I/O を使用するよりも日常的な。 バッファー内の I/O を使用するドライバーは、少量のダイレクト I/O を使用するときに、転送要求ごとのデータを転送 (かどうか DMA または PIO) 大量のシステム メモリ内で物理的なページ境界にまたがることがロックされたバッファー間でデータを転送します。

高度なドライバーは、通常は、それぞれのデバイス ドライバーの一致するようにそれらのデバイス オブジェクトを設定する物理デバイス ドライバーの上に配置します。 ただし、最上位レベルのドライバー、特に、ファイル システム ドライバーは、直接も、バッファー内の I/O のデバイス オブジェクトを設定できます。

バッファー内の I/O のそれらのデバイス オブジェクトを設定するドライバーをドライバーに送信するすべての Irp で有効なバッファーを渡す I/O マネージャー利用できます。 ダイレクト I/O のデバイス オブジェクトを設定する下位レベルのドライバーは、中間ドライバーを通じて基になる低レベル デバイス ドライバーに送信すべての Irp で有効なバッファーを渡す、チェーン内の最上位レベルのドライバーを使用できます。

### <a name="using-buffered-io-in-startio-routines"></a>StartIo ルーチンでバッファー内の I/O の使用

ドライバーの場合、 [ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、または[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、要求が有効で、呼び出すことを決定します[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)、I/O マネージャーには、ドライバーの[ *StartIo*。](https://msdn.microsoft.com/library/windows/hardware/ff563858)デバイスのキューが空の場合、IRP を直ちに処理するルーチン。 キューが空でない場合**IoStartPacket** IRP がキューに配置します。 呼び出しでは最終的には、 [**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)からドライバーの[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンが原因で IRP のデキューを呼び出してドライバーの I/O マネージャー *StartIo*ルーチン。

*StartIo*ルーチンの呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)し、要求を満たすために実行する必要があります操作を決定します。 これは、I/O 要求を実行する物理デバイスをプログラミングする前に必要な方法で IRP を前処理します。

場合、物理へのアクセスとデバイス (またはデバイスの拡張機能) を同期する必要があります、 [ *InterruptService* ](https://msdn.microsoft.com/library/windows/hardware/ff547958)ルーチン、 *StartIo*ルーチンは、を呼び出す必要があります[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチンに必要なデバイスのプログラミングを実行します。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

バッファー内の I/O を使用する物理デバイス ドライバーをまたはに各 IRP のドライバーを検索する I/O マネージャーによって割り当てられた、システムの領域バッファーからデータを転送する**Irp -&gt;AssociatedIrp.SystemBuffer**します。

### <a name="using-direct-io-in-startio-routines"></a>StartIo ルーチンで直接 I/O の使用

ドライバーの場合、 [ *DispatchRead*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、 [ *DispatchWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)、または[ *DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチンは、要求が有効で、呼び出すことを決定します[ **IoStartPacket**](https://msdn.microsoft.com/library/windows/hardware/ff550370)、I/O マネージャーには、ドライバーの*StartIo*ルーチンを。デバイスのキューが空の場合は、IRP を直ちに処理します。 キューが空でない場合**IoStartPacket** IRP がキューに配置します。 呼び出しでは最終的には、 [**います**](https://msdn.microsoft.com/library/windows/hardware/ff550358)からドライバーの[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079)または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンが原因で IRP のデキューを呼び出してドライバーの I/O マネージャー *StartIo*ルーチン。

*StartIo*ルーチンの呼び出し[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174)し、要求を満たすために実行する必要があります操作を決定します。 必要に応じて、部分的な転送の範囲に大きな DMA 転送要求を分割することについての状態の保存などの任意の方法で IRP を前処理、**長さ**の転送要求に分割する必要があります。 I/O 要求を実行する物理デバイスをプログラムします。

場合に、物理的なアクセス デバイス (またはデバイスの拡張機能) は、ドライバーの ISR と同期する必要があります、 *StartIo*ドライバーによって提供されるルーチンを使用する必要があります*SynchCritSection*ルーチンを実行する、必要なプログラミングします。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

ダイレクト I/O を使用するすべてのドライバーにデータを読み取るかの IRP である、ドライバーがによって検出されたメモリ記述子のリスト (MDL) で説明されている、ロックされたバッファーからデータを書き込みます**Irp -&gt;MdlAddress**します。 通常、このようなドライバーは、デバイス制御要求のバッファー内の I/O を使用します。 詳細については、次を参照してください。 [StartIo ルーチン内での I/O 制御要求の処理](#ddk-handling-i-o-control-requests-in-startio-routines-kg)します。

MDL 型は、ドライバーに直接アクセスしないで不透明な型です。 代わりに、PIO を使用するドライバーは呼び出すことによってユーザー スペースのバッファーをマップし直す[ **MmGetSystemAddressForMdlSafe** ](https://msdn.microsoft.com/library/windows/hardware/ff554559)で**Irp -&gt;MdlAddress**をパラメーターとして。 また DMA を使用するドライバーを渡す**Irp -&gt;MdlAddress**するバッファーのアドレスを自分のデバイスの論理範囲にマップし直され、転送操作中にルーチンをサポートするためにします。

最下位レベルのデバイス ドライバーの基になるデバイス ドライバーの場合、大規模な DMA 転送要求をより高度なドライバーを密接に結合された分割しない限り、 *StartIo*ルーチンは、各転送要求をそのデバイスを超えるを分割する必要があります1 つの転送操作で管理できます。 システムを使用するドライバー DMA は、転送要求は大きすぎるシステム DMA コント ローラーまたは単一の転送操作で処理するようにデバイスを分割する必要があります。

そのドライバーがアダプターのドライバーに割り当てられたオブジェクトは、DMA チャネル、およびドライバーによって提供されるを表すシステム DMA コント ローラーを経由の転送を同期する必要が、デバイスが下位の DMA デバイスの場合は、 [ *AdapterControl*](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン。 バス マスター DMA のデバイスのドライバーもアダプターのドライバーに割り当てられたオブジェクトを使用して、その転送を同期する必要があり、指定する必要があります、 *AdapterControl*ルーチン、システムのパケットに基づく DMA サポートを使用している場合、または[ *AdapterListControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540513)ルーチン システムのスキャッター/ギャザーのサポートを使用している場合。

ドライバーの設計によって、コント ローラー オブジェクトと、物理デバイスでの転送とデバイスの管理操作を同期し、指定があります、 [ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)ルーチン。

参照してください[アダプター オブジェクトと DMA](adapter-objects-and-dma.md)と[コント ローラー オブジェクト](using-controller-objects.md)詳細についてはします。

### <a href="" id="ddk-handling-i-o-control-requests-in-startio-routines-kg"></a>StartIo ルーチン内での I/O 制御要求の処理

デバイス I/O 制御要求のサブセットのみがドライバーから渡される一般に、 [ *DispatchDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)または[ *DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)さらに、ドライバーの処理に関する日常的な*StartIo*ルーチン。 ドライバーの*StartIo*ルーチンは、デバイスの状態の変更が必要か、現在のデバイスの状態に関する揮発性の情報を返す有効なデバイス コントロール要求を処理するためにのみにします。

新しい各ドライバーでは、同じ種類のデバイスの他のすべてのドライバーとパブリックの I/O 制御コードの同じセットをサポートする必要があります。 システム定義のパブリックのデバイス固有の種類の I/O 制御コード[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)バッファー内の要求の要求。

その結果、物理デバイス ドライバーがの IRP で各ドライバーが検出されたシステム領域バッファーとの間のデータ転送を行う**Irp -&gt;AssociatedIrp.SystemBuffer**デバイス制御要求のためです。 ダイレクト I/O に対してそのデバイス オブジェクトの設定もドライバーは、パブリック I/O 制御コードを持つデバイス制御の要求を満たすためにバッファー内の I/O を使用します。

各 I/O 制御コードの定義は、その要求の転送されたデータがバッファリングされるかどうかを判断します。 ドライバー固有の I/O 制御コードが非公開で定義されている[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)ペア間の要求コードは、ドライバーによってバッファリング メソッド、メソッドを直接、またはメソッドにも定義できます。 非公開で定義されている I/O 制御コードを定義する一般的な規則としてメソッドを使用してどちらの場合より高度なドライバーを密接に結合する必要がありますバッファーを割り当てる要求に必要です。

### <a name="programming-the-device-for-io-operations"></a>デバイスの I/O 操作のプログラミング

通常、 *StartIo* 、最下位レベルのデバイス ドライバーのルーチンはメモリへのアクセスを同期する必要がありますまたはデバイスに登録、共有、ドライバーの ISR を使用して[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)を呼び出すドライバーによって提供される[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチン。 ドライバーの*StartIo*ルーチン、 *SynchCritSection* DIRQL での I/O の物理デバイスを実際にプログラミング ルーチンです。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

呼び出しの前に**KeSynchronizeExecution**、 *StartIo*ルーチンは、要求に必要な処理を行う必要があります。 最初の部分転送範囲を計算し、その他のドライバーのルーチンの元の要求に関する状態情報を保存、前処理が含まれます。

デバイス ドライバーは、DMA を使用している場合、 *StartIo*ルーチンを呼び出す通常[ **AllocateAdapterChannel** ](https://msdn.microsoft.com/library/windows/hardware/ff540573)ドライバーによって提供されると[ *AdapterControl* ](https://msdn.microsoft.com/library/windows/hardware/ff540504)ルーチン。 このような場合、 *StartIo*ルーチンは、物理デバイスをプログラミングする責任を延期、 *AdapterControl*ルーチン。 これには、さらに、呼び出すことができます**KeSynchronizeExecution**ドライバーが提供する*SynchCritSection*ルーチン DMA 転送用のデバイスのプログラムします。

 

 




