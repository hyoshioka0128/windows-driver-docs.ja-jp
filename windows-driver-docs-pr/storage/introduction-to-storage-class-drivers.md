---
title: 記憶域クラス ドライバーの概要
description: 記憶域クラス ドライバーの概要
ms.assetid: 0ea462a9-5e6f-419f-af36-50f50901143d
keywords:
- ストレージクラスドライバー WDK, ストレージクラスドライバーについて
- クラスドライバー WDK ストレージ、ストレージクラスドライバーについて
- HBA WDK ストレージ
ms.date: 10/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 94049848af080157b95f778f6eb7190f7a56cca2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838091"
---
# <a name="introduction-to-storage-class-drivers"></a>記憶域クラス ドライバーの概要

## <span id="ddk_introduction_to_storage_class_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_STORAGE_CLASS_DRIVERS_KG"></span>

*ストレージクラスドライバー*は、適切に確立された scsi クラス/ポートインターフェイスを使用して、システムが記憶ポートドライバー (現在は SCSI、IDE、USB、および IEEE 1394) を供給する任意のバス上のその種類の大容量記憶装置デバイスを制御します。 ストレージデバイスが接続されている特定のバスは、ストレージクラスドライバーに対して透過的です。

すべてのストレージクラスドライバーでは、*コマンド記述子ブロック*(cdbs) を含む*SCSI 要求ブロック*(SRBs) を作成し、介在するフィルタードライバーを介して、それらを送信することによって、ユーザーアプリケーションまたは上位レベルのドライバーからの i/o 要求を処理します。基になるストレージポートドライバー。

ストレージクラスドライバーは、SRB 内のアドレス指定情報を提供しません。 代わりに、ポートドライバー (またはそれよりも下位のドライバー) は、必要なアドレス指定を行います。 ストレージポートドライバーは、SRBs を、基になるホストバスアダプター (HBA) が必要とする形式に変換します。これは、SCSI または1394ホストバスアダプター、IDE コントローラー、その他のハードウェアである可能性があり、コマンドをデバイスに発行します。 Windows Driver Kit (WDK) では、"HBA" という用語は、そのような基になるアダプターまたはコントローラーを意味します。

I/o マネージャーと、ストレージクラスドライバーの上に階層化された上位レベルのドライバーには、ほとんどのストレージクラスドライバーは標準のカーネルモード中間ドライバーです。 したがって、すべてのクラスドライバーには[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチン、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチン、 [**Unload**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)ルーチン、1つ以上の[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチン、および[**DispatchPnP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)と[**DispatchPower**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンが必要です。再生と電源 Irp。

また、ストレージクラスドライバーは、システム制御の Irp を処理する[**DispatchSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンも必要とします。また、ドライバーデザイナーによって決定された[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンなど、他の標準の上位レベルのドライバールーチンを持つことができます。 システム制御と標準カーネルモードドライバールーチンの詳細については、「[標準ドライバールーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)」を参照してください。

PnP マネージャーには、ストレージクラスドライバーは、個々のデバイスを駆動する[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)です。 ストレージクラスドライバーは、[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)として機能し、デバイスの子デバイスを列挙することもできます。 たとえば、ディスクなどのパーティション分割されたメディアデバイスのクラスドライバーは、パーティションを表す PDOs の一覧を返します。 このような PDO はそれぞれ、ターゲットデバイスとしてアドレス指定でき、独自のクラスドライバーによって処理されます。

**注:** このセクションで説明するように、プリンターやスキャナーなどの SCSI デバイス用のドライバーを実装する必要があり  。 このような SCSI デバイスのドライバーは、同じ SCSI クラス/ポートインターフェイスを利用してデバイスを制御し、Irp の処理、SRBs の構築、および記憶装置のドライバーと同様に基になるポートドライバーへの送信を行います。
