---
title: DriverEntry のオプションの役割
description: DriverEntry のオプションの役割
ms.assetid: 859282f7-6b40-47a8-b845-cdb7c26585dd
keywords:
- DriverEntry WDK カーネルでは、省略可能な責任
- ハードウェア リソースの要求
- 実行ワーカー スレッドの WDK カーネル
- ワーカー スレッドの WDK カーネル
- システム容量のメモリ割り当ての WDK カーネル
- システム リソースのストレージの WDK カーネル
- システム リソースを格納します。
- ハードウェア リソースよります WDK カーネル
- リソースよります WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d3dbacd2e761badad7defa649e8088719ce6694
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384953"
---
# <a name="driverentrys-optional-responsibilities"></a>DriverEntry のオプションの役割





基になるデバイスの性質と、ドライバーのデザインの階層型のドライバーのチェーン内の特定のドライバーの位置に応じて、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンも担当できる、次の。

-   呼び出す[ **IoAllocateDriverObjectExtension** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)を作成して、ドライバーがドライバー全体でデータのストレージを必要とする場合は、ドライバー オブジェクトの拡張機能を初期化します。 ドライバー オブジェクトの拡張機能は、ドライバー固有のデータ構造です。 たとえば、ドライバーでは、レジストリ パス、またはその他のグローバル情報を格納するのにそのドライバー オブジェクトの拡張機能を使用する場合があります。

-   呼び出す[ **PsCreateSystemThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pscreatesystemthread)場合は、ドライバーは、このようなスレッドを使用する (ファイル システム ドライバーの場合) などの最上位レベル ドライバー executive ワーカー スレッドを作成します。 この場合、ドライバーにはワーカーの種類のコールバック ルーチンがいる必要がありますも\_スレッド\_、PVOID 1 つの入力を受け取るルーチン*パラメーター*します。

-   登録、 [*を再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nc-ntddk-driver_reinitialize)ルーチン。 (を参照してください[再初期化ルーチンを記述](writing-a-reinitialize-routine.md))。

-   ここでは、ポートまたはクラスのドライバーと連動しているデバイスに固有ミニポートまたは miniclass ドライバーがあるように説明しているのとは異なるクラスに固有の初期化要件を処理します。 デバイスの種類の特定のドキュメントの詳細については Windows Driver Kit (WDK) を参照してください。

### <a name="providing-storage-for-system-resources"></a>ストレージ システム リソースを提供します。

デバイスごとのオブジェクトを割り当てる必要がある、 [ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) PnP を処理するルーチンまたはディスパッチ ルーチン[ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求ではなく、 **DriverEntry**します。

ただし、ドライバーは、その他のドライバーの使用の空きシステム メモリを割り当てる必要があります。 そうである場合、 **DriverEntry**ルーチンは、次のルーチンのいずれか (または複数) を呼び出すことができます。

-   **IoAllocateDriverObjectExtension**ドライバー オブジェクトに関連付けられたコンテキストの領域を作成します。

-   [**Exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)ページまたは非ページ システム容量のメモリ

-   [**MmAllocateNonCachedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmallocatenoncachedmemory)または[ **MmAllocateContiguousMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemory)のキャッシュで固定された非ページ システム スペースのメモリ (I/O バッファーの使用)

すべて**DriverEntry**ルーチンは IRQL でシステムのスレッドのコンテキストで実行 = パッシブ\_レベル。 このため、メモリが割り当てられた**exallocatepoolwithtag に**ドライバーがシステムのページング ファイルを保持するデバイスを制御しない限り、ページ プールからの初期化中にのみ使用があることができます。 割り当てられたメモリを解放する必要があります[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)する前に**DriverEntry**コントロールを返します。 ただし、ドライバーが設定された、*を再初期化*ルーチンを呼び出すときに、このメモリへのポインターを渡すことができます[ **IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization)ドライバーのこと*を再初期化*ルーチンのメモリの割り当てを解放します。

### <a href="" id="claiming-hardware-resources-"></a>ハードウェア リソースの要求

以前、非 PnP ドライバーは、レジストリからリソースを要求しています。 PnP ドライバーは、その一方で、デバイスのリソースからの要求もリソース要件をレジストリに直接書き込みます。 代わりに、これらのドライバー、PnP マネージャーの列挙プロセスの一部として、特定の PnP Irp への応答の要件を報告します。 PnP ドライバー、PnP で割り当てられたリソースを受け取る**IRP\_MN\_開始\_デバイス**要求。

特定のミニポート ドライバーなど、PnP マネージャーと直接対話しないドライバー、PnP マネージャーとの対話は、クラスまたはポートのドライバーによって課される別のレポート要件があります。 このような要件は、デバイス クラスに固有です。 デバイスおよびクラスに固有の詳細については、Windows Driver Kit (WDK) に関連するデバイス クラスに関するドキュメントを参照してください。

### <a name="using-the-registry"></a>レジストリを使用

A **DriverEntry**ルーチンは、レジストリを使用して、ドライバーを初期化するために必要な情報の一部を取得する可能性があります、またはその他のドライバーのレジストリの情報を設定可能性がありますを使用するサブシステムを保護します。 情報の種類は、デバイスの種類によって異なります。 ドライバーは、レジストリを使用して、アクセスできる**Zw * Xxx*** と**Rtl * Xxx*** ルーチン。 **DriverEntry**ルーチンの*RegistryPath*パラメーターが、ドライバーのレジストリ キーへのパスを指定する、カウントされた Unicode 文字列を指す<strong>\\レジストリ\\マシン\\システム\\CurrentControlSet\\サービス\\* DriverName</strong><em>します。ポインターが後に無効になっているために、ルーチンはポインター自体ではなく、文字列のコピーを保存する必要があります **DriverEntry</em>* を返します。

 

 




