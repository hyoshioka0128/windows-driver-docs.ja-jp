---
title: DriverEntry のオプションの役割
description: DriverEntry のオプションの役割
ms.assetid: 859282f7-6b40-47a8-b845-cdb7c26585dd
keywords:
- DriverEntry WDK カーネル、オプションの役割
- ハードウェアリソースの要求
- executive ワーカースレッドの WDK カーネル
- ワーカースレッドの WDK カーネル
- システム領域のメモリ割り当て (WDK カーネル)
- システムリソースストレージ WDK カーネル
- システムリソースの格納
- WDK カーネルを要求するハードウェアリソース
- WDK カーネルを要求するリソース
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d9183bc620d54ca0de824a09be4e87d941a415
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838715"
---
# <a name="driverentrys-optional-responsibilities"></a>DriverEntry のオプションの役割





階層化されたドライバーのチェーン内の特定のドライバーの位置、基になるデバイスの特性、ドライバーの設計によっては、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンも次のことを担当します。

-   ドライバーがドライバー全体のデータのための記憶域を必要とする場合、 [**Ioallocatedriverobjectextension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)を呼び出してドライバーオブジェクト拡張機能を作成および初期化します。 ドライバーオブジェクト拡張は、ドライバー固有のデータ構造体です。 たとえば、ドライバーは、ドライバーオブジェクト拡張機能を使用して、レジストリパスまたはその他のグローバル情報を格納する場合があります。

-   ドライバーが、そのようなスレッドを使用する最上位レベルのドライバー (ファイルシステムドライバーなど) である場合は、 [**PsCreateSystemThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread)を呼び出して、executive ワーカースレッドを作成します。 この場合、ドライバーは、1つの入力 PVOID*パラメーター*を受け取るワーカー\_スレッド\_ルーチンのコールバックルーチンも持っている必要があります。

-   [*再初期化*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)ルーチンを登録しています。 (「[再初期化ルーチンの記述」を](writing-a-reinitialize-routine.md)参照してください)。

-   ここで説明したものとは異なるクラス固有の初期化要件を処理します。たとえば、デバイス固有のミニポートまたは miniclass ドライバーがポートやクラスドライバーと連携して動作する場合などです。 詳細については、Windows Driver Kit (WDK) のデバイスタイプに固有のドキュメントを参照してください。

### <a name="providing-storage-for-system-resources"></a>システムリソースの記憶域の提供

デバイスごとのオブジェクトは、 **Driverentry**ではなく\_デバイスの要求を[**開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device) [*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンまたはディスパッチ\_ルーチンで割り当てる必要があります。

ただし、ドライバーでは、他のドライバー全体の使用に対して、追加のシステム領域メモリの割り当てが必要になる場合があります。 その場合、 **Driverentry**ルーチンは、次のルーチンの1つ (または複数) を呼び出すことができます。

-   **Ioallocatedriverobjectextension**、driver オブジェクトに関連付けられたコンテキスト領域を作成します。

-   ページングされたシステム領域または非ページシステム領域のメモリの[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)

-   キャッシュによって調整された非ページシステムスペースメモリの[**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)または[**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory) (i/o バッファーに使用)

すべての**Driverentry**ルーチンは、IRQL = パッシブ\_レベルでシステムスレッドのコンテキストで実行されます。 そのため、システムページファイルを保持するデバイスがドライバーによって制御されていない限り、初期化時に排他的に使用するために**Exallocatepoolwithtag**で割り当てられたメモリは、ページプールからしか使用できません。 **Driverentry**が制御を返す前に、割り当てられたメモリを[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)と共に解放する必要があります。 ただし、*再初期化*ルーチンを設定するドライバーは、 [**IoRegisterDriverReinitialization**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioregisterdriverreinitialization)を呼び出すときにこのメモリへのポインターを渡すことができます。これにより、ドライバーの*再初期化*ルーチンはメモリ割り当ての解放を担当します。

### <a href="" id="claiming-hardware-resources-"></a>ハードウェアリソースの要求

以前の非 PnP ドライバーは、レジストリからリソースを要求していました。 一方、PnP ドライバーは、からデバイスリソースの要求を行いません。また、リソース要件をレジストリに直接書き込むこともありません。 代わりに、これらのドライバーは、PnP マネージャーの列挙プロセスの一環として、特定の PnP Irp に応答して要件を報告します。 PnP ドライバーは、割り当てられたリソースを PnP IRP で受信し、 **\_デバイス要求を開始\_\_** します。

PnP マネージャーと直接やり取りしないドライバー (特定のミニポートドライバーなど) は、PnP マネージャーと対話するクラスまたはポートドライバーによって異なるレポート要件を持つ場合があります。 このような要件は、デバイスクラスに固有のものです。 デバイス固有およびクラス固有の詳細については、Windows Driver Kit (WDK) の関連するデバイスクラスのドキュメントを参照してください。

### <a name="using-the-registry"></a>レジストリの使用

**Driverentry**ルーチンでは、レジストリを使用して、ドライバーを初期化するために必要な情報の一部を取得したり、他のドライバーまたは保護されたサブシステム用にレジストリに情報を設定したりすることがあります。 情報の性質は、デバイスの種類によって異なります。 ドライバーは、 **Zw * xxx*** および**Rtl * xxx*** ルーチンを使用してレジストリにアクセスできます。 **Driverentry**ルーチンの*RegistryPath*パラメーターは、ドライバーのレジストリキーへのパスを指定する\\、カウントされた Unicode 文字列を指しています。 <strong>\\コンピューター\\System\\CurrentControlSet\\サービス\\* ドライバー 1</strong><em>.ルーチンは、ポインター自体ではなく、文字列のコピーを保存する必要があります。これは、**Driverentry</em>が返された後にポインターが無効になるため*です。

 

 




