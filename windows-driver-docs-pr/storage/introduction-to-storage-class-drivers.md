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
ms.openlocfilehash: 10cce3a7243996a0e11b82202b1e68e0e7672e9e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382112"
---
# <a name="introduction-to-storage-class-drivers"></a>記憶域クラス ドライバーの概要


## <span id="ddk_introduction_to_storage_class_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_STORAGE_CLASS_DRIVERS_KG"></span>


A*記憶域クラス ドライバー*システムがストレージ ポート ドライバー (現在 SCSI、IDE、USB および IEEE 1394) を提供する任意のバスにその型のマス ストレージ デバイスを制御するために確立された SCSI クラス/ポート インターフェイスを使用します。 ストレージ デバイスが接続されている特定のバスは、記憶域クラス ドライバーに対して透過的です。

任意のストレージ クラス ドライバーでは、ユーザーのアプリケーションまたはより高度なドライバーからの I/O 要求を処理を構築して*SCSI 要求のブロック*(される Srb) を含む*記述子のブロックをコマンド*(Cdb) して、送信します。使用する基になる記憶域ポート ドライバー、介在するフィルター ドライバー。

ストレージ クラス ドライバーは、SRB のアドレス指定情報を提供しません。 代わりに、ポート ドライバー (またはまだ下ドライバー) は、対処の必要な責任を負います。 記憶域ポート ドライバーは、される Srb を基になるホスト バス アダプター (HBA)、SCSI 可能性のあるまたは 1394 ホスト バス アダプター、IDE コント ローラー、またはこのようなその他のハードウェアで必要な形式に変換し、デバイスにコマンドを発行します。 Windows Driver Kit (WDK) で"HBA"という用語は、このような基になるアダプターまたはコント ローラーを表します。

I/O マネージャーとストレージ クラス ドライバーの上に配置より高度なドライバーの場合には、ほとんどのストレージ クラス ドライバーは、標準のカーネル モード中間ドライバーです。 したがってすべてのクラス ドライバーが必要、 [ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン、 [ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521) 、ルーチン、 [ **アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチンを 1 つまたは複数[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン、plus [ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)と[ **DispatchPower** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)プラグ アンド プレイと電源 Irp を処理するルーチン。

ストレージ クラス ドライバーが必要、 [ **DispatchSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)システム コントロールの Irp を処理するルーチンとその他標準より高度なドライバーのルーチンなどがあることができます、 [ **StartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff563858)ルーチン、ドライバー デザイナーによって決定されます。 システム コントロールと標準のカーネル モード ドライバーのルーチンの詳細については、次を参照してください。[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)します。

PnP マネージャーでは、ストレージ クラス ドライバーは、[関数ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff546516)、ドライブの個々 のデバイスは、いずれのか。 ストレージ クラス ドライバーとしても機能、[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704)、そのデバイスのデバイスを子を列挙します。 たとえば、ディスクなどのパーティション分割されたメディア デバイスのクラス ドライバーの一覧を返します Pdo のパーティションを表します。 このような各 PDO は、ターゲット デバイスとしてアドレス指定することができ、独自のクラス ドライバーによりサービスを提供します。

**注**  このセクションで説明した、プリンターやスキャナーなどの SCSI デバイスのドライバーを実装する必要があります。 このような SCSI デバイスのドライバーでは、そのデバイスを制御するのと同じ SCSI クラス/ポート インターフェイスを利用し、同様の役割を Irp の処理、作成される Srb、およびストレージ デバイスのドライバーとは、基になるポート ドライバーに送信するが。

 

 

 




