---
title: バッファーされる i/o を使用した DispatchReadWrite
description: バッファーされる i/o を使用した DispatchReadWrite
ms.assetid: bb8ce47d-5722-4050-9492-bec154744597
keywords:
- DispatchReadWrite ルーチン
- ディスパッチルーチン WDK カーネル、DispatchReadWrite ルーチン
- 読み取り/書き込みディスパッチルーチン WDK カーネル
- IRP_MJ_WRITE i/o 関数コード
- IRP_MJ_READ i/o 関数コード
- データ転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- データの転送 WDK カーネル、読み取り/書き込みディスパッチルーチン
- バッファーされる i/o WDK カーネル
- I/o WDK カーネル、バッファー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38c70fdc899eed218af9897efad3a00c604a25e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838723"
---
# <a name="dispatchreadwrite-using-buffered-io"></a>バッファーされる i/o を使用した DispatchReadWrite





バッファーに格納された i/o のデバイスオブジェクトを設定する最も下位レベルのデバイスドライバーは、そのデバイスから転送されたデータを**Irp-&gt;AssociatedIrp**にあるロックダウンされたシステム領域バッファーに返すことによって、読み取り要求を満たします。 同じバッファーからデバイスにデータを転送することによって、書き込み要求を満たします。

そのため、通常、このようなデバイスドライバーの*DispatchReadWrite*ルーチンは、転送要求の受信時に次のことを行います。

1.  [**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出し、転送要求の方向を決定します。

2.  要求のパラメーターが有効かどうかを確認します。

    -   読み取り要求の場合、ルーチンは通常、ドライバーの*Iostacklocation*-&gt;パラメーターをチェックし**ます。 Length**値を使用して、バッファーがデバイスから転送されたデータを受信するのに十分な大きさかどうかを確認します。

        たとえば、システムキーボードのクラスドライバーは、Win32 ユーザー入力スレッドからの読み取り要求だけを処理します。 このドライバーは、デバイスからキーストロークを格納する構造体、キーボード\_入力\_データを定義します。また、特定の時点で、読み取り要求を処理するために、これらの構造体の一部を内部リングバッファーに保持します。

    -   書き込み要求の場合、ルーチンは通常、**パラメーター**の値を確認し、必要に応じて**Irp-&gt;AssociatedIrp**のデータをチェックします。つまり、そのデバイスが構造化されたデータパケットのみを受け入れるかどうかを確認します。定義済みの値の範囲を持つメンバーが含まれています。

3.  パラメーターが無効な場合は、「 [irp の完了](completing-irps.md)」で既に説明したように、 *DISPATCHREADWRITE*ルーチンは irp を直ちに完了します。 それ以外の場合、ルーチンは、「 [irp をドライバースタックに渡す](passing-irps-down-the-driver-stack.md)」で説明されているように、他のドライバールーチンによってさらに処理するために、irp をに渡します。

通常、バッファー内 i/o を使用する最下位レベルのデバイスドライバーは、要求元によって指定されたサイズのデータの読み取りまたは書き込みを行うことにより、転送要求を満たす必要があります。 このようなドライバーは、デバイスとの間で送受信されるデータの構造を定義する可能性が高く、システムキーボードクラスドライバーと同様に、内部的に構造化データをバッファーする可能性があります。

内部でデータをバッファーに格納するドライバーは、 [**irp\_MJ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-flush-buffers)をサポートしている必要があります。\_は、バッファー要求をフラッシュ\_、 [**irp\_MJ\_のシャットダウン**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-shutdown)要求もサポートします。

チェーン内の最上位レベルのドライバーは、通常、読み取り/書き込み要求を下位のドライバーに渡す前に、入力 IRP のパラメーターを確認する役割を担います。 そのため、多くの下位レベルのドライバーでは、読み取り/書き込みの IRP 内の i/o スタックの場所に有効なパラメーターがあると想定できます。 チェーン内の最下位レベルのドライバーが、データ転送に関するデバイス固有の制約を認識している場合、そのドライバーは i/o スタックの場所にあるパラメーターの有効性を確認するために必要です。

 

 




