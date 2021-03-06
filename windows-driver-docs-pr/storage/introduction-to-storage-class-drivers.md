---
title: 記憶域クラス ドライバーの概要
description: 記憶域クラス ドライバーの概要
ms.assetid: 0ea462a9-5e6f-419f-af36-50f50901143d
keywords:
- 記憶域クラス ドライバーに関する記憶域クラス ドライバー WDK、
- 記憶域クラス ドライバーについてのクラス ドライバー WDK ストレージ
- HBA の WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67fae9653f9ef8842ff00aff6a2691d9b339c79c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360201"
---
# <a name="introduction-to-storage-class-drivers"></a>記憶域クラス ドライバーの概要


## <span id="ddk_introduction_to_storage_class_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_STORAGE_CLASS_DRIVERS_KG"></span>


A*記憶域クラス ドライバー*システムがストレージ ポート ドライバー (現在 SCSI、IDE、USB および IEEE 1394) を提供する任意のバスにその型のマス ストレージ デバイスを制御するために確立された SCSI クラス/ポート インターフェイスを使用します。 ストレージ デバイスが接続されている特定のバスは、記憶域クラス ドライバーに対して透過的です。

任意のストレージ クラス ドライバーでは、ユーザーのアプリケーションまたはより高度なドライバーからの I/O 要求を処理を構築して*SCSI 要求のブロック*(される Srb) を含む*記述子のブロックをコマンド*(Cdb) して、送信します。使用する基になる記憶域ポート ドライバー、介在するフィルター ドライバー。

ストレージ クラス ドライバーは、SRB のアドレス指定情報を提供しません。 代わりに、ポート ドライバー (またはまだ下ドライバー) は、対処の必要な責任を負います。 記憶域ポート ドライバーは、される Srb を基になるホスト バス アダプター (HBA)、SCSI 可能性のあるまたは 1394 ホスト バス アダプター、IDE コント ローラー、またはこのようなその他のハードウェアで必要な形式に変換し、デバイスにコマンドを発行します。 Windows Driver Kit (WDK) で"HBA"という用語は、このような基になるアダプターまたはコント ローラーを表します。

I/O マネージャーとストレージ クラス ドライバーの上に配置より高度なドライバーの場合には、ほとんどのストレージ クラス ドライバーは、標準のカーネル モード中間ドライバーです。 したがってすべてのクラス ドライバーが必要、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチン、 [ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device) 、ルーチン、 [ **アンロード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)ルーチンを 1 つまたは複数[ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン、plus [ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)プラグ アンド プレイと電源 Irp を処理するルーチン。

ストレージ クラス ドライバーが必要、 [ **DispatchSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)システム コントロールの Irp を処理するルーチンとその他標準より高度なドライバーのルーチンなどがあることができます、 [ **StartIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチン、ドライバー デザイナーによって決定されます。 システム コントロールと標準のカーネル モード ドライバーのルーチンの詳細については、次を参照してください。[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)します。

PnP マネージャーでは、ストレージ クラス ドライバーは、[関数ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/function-drivers)、ドライブの個々 のデバイスは、いずれのか。 ストレージ クラス ドライバーとしても機能、[バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)、そのデバイスのデバイスを子を列挙します。 たとえば、ディスクなどのパーティション分割されたメディア デバイスのクラス ドライバーの一覧を返します Pdo のパーティションを表します。 このような各 PDO は、ターゲット デバイスとしてアドレス指定することができ、独自のクラス ドライバーによりサービスを提供します。

**注**  このセクションで説明した、プリンターやスキャナーなどの SCSI デバイスのドライバーを実装する必要があります。 このような SCSI デバイスのドライバーでは、そのデバイスを制御するのと同じ SCSI クラス/ポート インターフェイスを利用し、同様の役割を Irp の処理、作成される Srb、およびストレージ デバイスのドライバーとは、基になるポート ドライバーに送信するが。

 

 

 




