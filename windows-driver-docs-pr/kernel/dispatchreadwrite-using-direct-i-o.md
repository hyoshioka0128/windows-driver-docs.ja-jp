---
title: ダイレクト I/O を使用した DispatchReadWrite
description: ダイレクト I/O を使用した DispatchReadWrite
ms.assetid: 5174fe1f-aee5-4c8a-87a1-7f185ed4e242
keywords:
- DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチルーチン WDK カーネル
- IRP_MJ_WRITE i/o 関数コード
- IRP_MJ_READ i/o 関数コード
- データ転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- データの転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- ダイレクト i/o WDK カーネル
- I/o WDK カーネル、ダイレクト i/o
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40e4aeb46846dec245a93629c59885867b48dff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836837"
---
# <a name="dispatchreadwrite-using-direct-io"></a>ダイレクト I/O を使用した DispatchReadWrite





ダイレクト i/o 用にデバイスオブジェクトを設定する下位レベルのデバイスドライバーは、デバイスからシステムの物理メモリに転送されたデータを返すことによって読み取り要求を満たします。これは、MDL によって **&gt;MdlAddress**に記述されています。 システムの物理メモリからデバイスにデータを転送することによって、書き込み要求を満たします。

下位レベルのドライバーでは、読み取り/書き込み要求を非同期的に処理する必要があります。 したがって、すべての下位レベルのドライバーの[*DispatchReadWrite*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンは、有効なパラメーターを使用して[**irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)irp を渡す必要があります。詳細については、「」を参照してください。 [Irp をドライバースタックから下に移動](passing-irps-down-the-driver-stack.md)します。

下位レベルのドライバーに送信される読み取り/書き込み Irp の場合、 **irp-&gt;MdlAddress**の MDL によって記述されたページングされた物理メモリは、要求された転送を実行するための正しいアクセス権を既に調査済みであり、既にによってロックダウンされています。チェーン内の最上位レベルのドライバー、または i/o マネージャー。 ダイレクト i/o 用にデバイスオブジェクトを設定する中間または最下位レベルのドライバーは、既に実行されているため、 [**MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)を呼び出すことはできません。 最下位レベルのドライバーは、 [**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出します。 (Windows 98 のドライバーは代わりに[**MmGetSystemAddressForMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmgetsystemaddressformdl)を呼び出します。 Windows Me のドライバー、Windows 2000 以降のバージョンの Windows では**MmGetSystemAddressForMdlSafe**を使用する必要があります)。

すべての中間または最下位のデバイスドライバーの*DispatchReadWrite*ルーチンは、上位レベルのドライバーを信頼できないために、有効なパラメーターを持つ irp だけを渡すことができる場合、その i/o スタックの場所にあるパラメーターを検証する必要があります。 *DispatchReadWrite*ルーチンでパラメーターエラーが検出された場合は、「 [irp の完了](completing-irps.md)」で既に説明されているように、適切なエラー状態\_*XXX*値を使用して IRP を完了する必要があります。 パラメーターが有効な場合、[より上位のドライバーの DispatchReadWrite](dispatchreadwrite-in-higher-level-drivers.md)のガイドラインに従って、中間ドライバーの*DispatchReadWrite*ルーチンは、後続の処理のために要求をに渡す必要があります。

最下位レベルのデバイスドライバーの*DispatchReadWrite*ルーチンは、転送要求で[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、他のドライバールーチンによる後続の処理を行うために IRP を渡し、状態\_PENDING を返します。詳細については、「」[を参照してください。Irp をドライバースタックに渡し](passing-irps-down-the-driver-stack.md)ます。

デバイスドライバーの*DispatchReadWrite*ルーチンは、ドライバーによって決定された*キー*値を使用して[**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)を呼び出すことによって、i/o スループットを向上させるために、irp がデバイスに対してキューに配置される順序を制御できることに注意してください。 ドライバーの別のルーチンは、後で IRP をデキューし、要求された長さを部分転送操作に分割する必要があるかどうかを判断し、データを転送するようにデバイスをプログラムします。

一般に、サイズの大きい転送要求をデバイスの制限に合うように分割する必要があるデバイスドライバーは、特定の転送要求に対してデバイスを設定する直前まで、これらの操作を延期する必要があります。 このようなデバイスドライバーの*DispatchReadWrite*ルーチンでは、デバイス固有の転送制約に対して着信 irp の i/o スタックの場所を確認したり、部分転送の範囲を計算したりすることはできません。ドライバーがこれらのチェックを延期して、[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) (またはその他のドライバールーチン) の直前に、転送操作のためにデバイスをプログラムします。

 

 




