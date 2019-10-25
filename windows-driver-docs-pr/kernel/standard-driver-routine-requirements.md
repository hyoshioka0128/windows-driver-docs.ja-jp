---
title: 標準ドライバー ルーチンの要件
description: 標準ドライバー ルーチンの要件
ms.assetid: 49b382ad-c282-41d2-b8b3-68eca4e12b9c
keywords:
- 標準ドライバールーチン WDK カーネル、要件
- ドライバールーチン WDK カーネル、要件
- ルーチン WDK カーネル、要件
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0870238d846b4f0813ce5c4df07770ef807e7075
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838412"
---
# <a name="standard-driver-routine-requirements"></a>標準ドライバー ルーチンの要件





カーネルモードドライバーを設計するときは、次の点に注意してください。

-   各ドライバーには、ドライバー全体のデータ構造とリソースを初期化する[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンが必要です。 I/o マネージャーは、ドライバーの読み込み時に**Driverentry**ルーチンを呼び出します。

-   すべてのドライバーには、i/o 要求パケット (Irp) を受信して処理するディスパッチルーチンが少なくとも1つ必要です。 各ドライバーは、ドライバー [ **\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造にディスパッチルーチンのエントリポイントを配置する必要があります。これは、ドライバーが受け取ることができる各[IRP 主要な関数コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)に適用されます。 ドライバーは、各 IRP 主要な関数コードに対して個別のディスパッチルーチンを持つことができます。または、複数の関数コードを処理する1つ以上のディスパッチルーチンを持つことができます。

-   すべての WDM ドライバーには、[*アンロード*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチンが必要です。 ドライバーは、*アンロード*ルーチンのエントリポイントをドライバーのドライバーオブジェクトに配置する必要があります。 [Pnp ドライバーのアンロードルーチン](pnp-driver-s-unload-routine.md)の役割は最小限ですが、 [pnp 以外のドライバーのアンロードルーチン](non-pnp-driver-s-unload-routine.md)は、ドライバーが使用しているシステムリソースを解放する必要があります。

-   すべての WDM ドライバーには、ドライバーオブジェクトの*AddDevice*が必要です。 *AddDevice*ルーチンは、ドライバーによって制御される PnP デバイスごとにデバイスオブジェクトの作成と初期化を行います。

-   ドライバーは、 [*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを持つことができます。このルーチンは、ドライバーがシステムによって提供される irp キューに対してキューに登録されている irp の i/o 操作を開始するために、i/o マネージャーが呼び出します。 *StartIo*ルーチンが含まれていないドライバーは、受信する irp の内部キューを設定して管理するか、ディスパッチルーチン内のすべての irp を完了する必要があります。 上位レベルのドライバーは、ディスパッチルーチンから直接 Irp を下位レベルのドライバーに渡すだけで、 *StartIo*ルーチンを持つことはできません。

-   特定のミニポートドライバーは、上記の要件の例外です。 ミニポートドライバーの要件の詳細については、Windows Driver Kit (WDK) のデバイスタイプ固有のドキュメントを参照してください。

-   ドライバーが他の種類の標準ルーチンを持っているかどうかは、そのドライバーがシステムにどのように適合しているか (たとえば、システムが提供するドライバーと相互運用しているかどうか) によって、そのドライバーの機能によって異なります。 詳細については、WDK のデバイスタイプに固有のドキュメントを参照してください。

 

 




