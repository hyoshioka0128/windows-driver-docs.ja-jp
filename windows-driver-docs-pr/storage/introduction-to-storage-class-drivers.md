---
title: 記憶域クラス ドライバーの概要
description: 記憶域クラス ドライバーの概要
ms.assetid: 0ea462a9-5e6f-419f-af36-50f50901143d
keywords:
- ストレージクラスドライバー WDK, ストレージクラスドライバーについて
- クラスドライバー WDK ストレージ、ストレージクラスドライバーについて
- HBA WDK ストレージ
ms.date: 12/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 21229a8955192cbf8bb39ad6875f58c2f62b0370
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606386"
---
# <a name="introduction-to-storage-class-drivers"></a>記憶域クラス ドライバーの概要

*ストレージクラスドライバー*は、適切に確立された scsi クラス/ポートインターフェイスを使用して、システムが記憶ポートドライバー (現在は SCSI、IDE、USB、および IEEE 1394) を供給する任意のバス上のその種類の大容量記憶装置デバイスを制御します。 ストレージデバイスが接続されている特定のバスは、ストレージクラスドライバーに対して透過的です。

任意のストレージクラスドライバーは、*コマンド記述子ブロック*(cdbs) を含む*SCSI 要求ブロック*(SRBs) を構築し、介在するフィルタードライバーを介して基になるストレージポートドライバーに送信することによって、ユーザーアプリケーションまたは上位レベルのドライバーからの i/o 要求を処理します。

ストレージクラスドライバーは、SRB 内のアドレス指定情報を提供しません。 代わりに、ポートドライバー (またはそれよりも下位のドライバー) は、必要なアドレス指定を行います。 ストレージポートドライバーは、SRBs を、基になるホストバスアダプター (HBA) が必要とする形式に変換します。これは、SCSI または1394ホストバスアダプター、IDE コントローラー、その他のハードウェアである可能性があり、コマンドをデバイスに発行します。 Windows Driver Kit (WDK) では、"HBA" という用語は、そのような基になるアダプターまたはコントローラーを意味します。

I/o マネージャーと、ストレージクラスドライバーの上に階層化された上位レベルのドライバーには、ほとんどのストレージクラスドライバーは標準のカーネルモード中間ドライバーです。 したがって、すべてのクラスドライバーには、 [**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチン、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン、 [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン、1つ以上の[**iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン、およびプラグアンドプレイと電源 Irp を処理するための[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)と[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが必要です。

また、ストレージクラスドライバーは、システム制御の Irp を処理する[**DispatchSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンも必要とします。また、ドライバーデザイナーによって決定された[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンなど、他の標準の上位レベルのドライバールーチンを持つことができます。 システム制御と標準カーネルモードドライバールーチンの詳細については、「[標準ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)」を参照してください。

PnP マネージャーには、ストレージクラスドライバーは、個々のデバイスを駆動する[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)です。 ストレージクラスドライバーは、[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)として機能し、デバイスの子デバイスを列挙することもできます。 たとえば、ディスクなどのパーティション分割されたメディアデバイスのクラスドライバーは、パーティションを表す PDOs の一覧を返します。 このような PDO はそれぞれ、ターゲットデバイスとしてアドレス指定でき、独自のクラスドライバーによって処理されます。

> [!NOTE]
> このセクションで説明するように、プリンターやスキャナーなどの SCSI デバイス用のドライバーを実装する必要があります。 このような SCSI デバイスのドライバーは、同じ SCSI クラス/ポートインターフェイスを利用してデバイスを制御し、Irp の処理、SRBs の構築、および記憶装置のドライバーと同様に基になるポートドライバーへの送信を行います。
