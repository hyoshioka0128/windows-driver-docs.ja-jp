---
title: クラス/ポート ドライバーの Dispatch(Internal)DeviceControl
description: クラス/ポート ドライバーの Dispatch(Internal)DeviceControl
ms.assetid: 94f6050d-c47e-4fb2-8b7f-afadcf12e0b8
keywords:
- ディスパッチルーチン WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ DispatchDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL i/o 関数コード
- デバイス制御ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41b28235bd9f84966652ab907744ba746ffb5513
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828320"
---
# <a name="dispatchinternaldevicecontrol-in-classport-drivers"></a>クラス/ポート ドライバーの Dispatch(Internal)DeviceControl





クラスとポートのペアの上位レベルのドライバーは、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで irp を完了することがあります。 たとえば、クラスドライバーは、初期化中に、基になるデバイスの機能に関する情報を収集して格納することができます。これは、その後の[**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求でシークされる可能性があり、その結果、保存します。基になるデバイスドライバーに要求を渡さずに要求を満たすことによる処理時間。 また、クラスドライバーは、IRP のパラメーターを確認し、有効なパラメーターを持つ要求のみをポートドライバーに送信するように設計されている場合もあります。

また、厳密に結合されたクラス/ポートドライバーでは、ドライバー固有またはデバイス固有の内部 i/o 制御コードのセットを定義することもできます。このコードでは、クラスドライバーは、内部\_デバイスに対して、ポートへの要求[ **\_制御する IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)使用できます。driver.

たとえば、システムキーボードおよびマウスクラスのドライバーの*DispatchCreateClose*ルーチンは、システム定義の内部デバイスコントロール要求を送信して、基になるポートドライバーに対するキーボードおよびマウスの割り込みを有効または無効にします。 これらのシステムクラスドライバーは、基になるポートドライバーの要求 **\_制御する内部\_デバイス\_、IRP\_MJ**を設定します。 これらのシステムクラスドライバーと相互運用できる新しいキーボードまたはマウスポートドライバーは、これらのパブリック内部デバイス制御要求もサポートする必要があります。

システム並列クラス/ポートドライバーモデルには同様の機能があります。 新しい並列クラスドライバーは、 **irp\_MJ\_内部\_\_デバイス**の irp を設定することによって、システムのパラレルポートドライバーからサポートを受けることができます。この場合、パブリック IOCTL\_パラレル\_ポート\_*XXX*の制御コードを使用して要求を制御します。 システムパラレルポートドライバーは置き換えることができますが、新しいドライバーでは、このような内部デバイス制御要求のセットもサポートする必要があります。

これらのパブリック内部デバイス制御要求の詳細については、Windows Driver Kit (WDK) のデバイス固有のドキュメントを参照してください。 プライベート i/o 制御コードを定義する方法の詳細については、「 [I/o 制御コードの使用](using-i-o-control-codes.md)」を参照してください。

ポート/クラスドライバーのペアが密接に結合されている場合、クラスドライバーは、ポートドライバーに渡さずに特定のデバイス制御要求の処理を処理することがあります。 新しいクラス/ポートドライバーのペアでは、クラスドライバーの*DispatchDeviceControl*ルーチンは次のいずれかを実行できます。

-   独自の i/o スタックの場所にあるパラメーターの有効性を確認し、パラメーターエラーが検出された場合は i/o 状態ブロックを設定し、 [**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して\_\_IO の優先*順位を上げ*ますそれ以外の場合は、 [**IogetnextiIoCallDriver Stacklocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)を呼び出して、独自の i/o スタックの場所をポートドライバーのにコピーし、IRP を[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)に渡します。

-   または、パラメーターをチェックせずに、IRP 内のポートドライバーの i/o スタックの場所を設定する以外に、処理のためにポートドライバーに渡すこともできません。

SCSI クラスドライバーには、デバイス制御要求を処理するための特別な要件があります。 これらの要件の詳細については、「 [Storage Drivers](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)」を参照してください。

 

 




