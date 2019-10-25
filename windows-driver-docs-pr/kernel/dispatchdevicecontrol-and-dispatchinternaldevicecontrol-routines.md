---
title: DispatchDeviceControl および DispatchInternalDeviceControl ルーチン
description: DispatchDeviceControl および DispatchInternalDeviceControl ルーチン
ms.assetid: 0bf8868e-bc5a-4fa7-9ff6-270f7a7bc850
keywords:
- ディスパッチルーチン WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチルーチン WDK カーネル、DispatchInternalDeviceControl ルーチン
- DispatchDeviceControl ルーチン
- DispatchInternalDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL i/o 関数のコード
- IRP_MJ_INTERNAL_DEVICE_CONTROL i/o 関数のコード
- 内部デバイス制御ディスパッチルーチン WDK カーネル
- デバイス制御ディスパッチルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84b04e62b40fe08666dce5cbc6c829cc9229cf1c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836889"
---
# <a name="dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines"></a>DispatchDeviceControl および DispatchInternalDeviceControl ルーチン


ドライバーのディスパッチルーチン (「 [**DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)」を参照) は、 [**irp\_MJ\_デバイス\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)および[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)の i/o 関数コードを使用して irp を処理します。4.3.

システムは、すべての一般的な種類の周辺機器について、 **IRP\_MJ\_デバイス\_制御**要求の i/o 制御コードのセットを定義します。 デバイスの種類ごとに新しいドライバーは、これらの要求をサポートする必要があります。 ほとんどの場合、デバイスの種類ごとにこれらのパブリック i/o 制御コードは、ユーザーモードアプリケーションにエクスポートされません。 


これらのシステム定義の i/o 制御コードの一部は、 [**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)を呼び出すことによって基になるデバイスドライバーの irp を作成する上位レベルのドライバーによって使用されます。 その他は、win32 関数[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Microsoft Windows SDK のドキュメントで説明) を呼び出して、基になるデバイスドライバーと通信するために win32 コンポーネントによって使用されます。この関数は、システムサービスを呼び出します。 I/o マネージャーは、IRP を設定し、主要な関数コード**IRP\_MJ\_デバイス\_制御**、および[**IO\_スタックの\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)構造体**に特定の i/o 制御コードを格納します。DeviceIoControl. IoControlCode**。 次に、i/o マネージャーはチェーン内の最上位レベルのドライバーの*DispatchDeviceControl*ルーチンを呼び出します。

システムで提供される特定のドライバーが新しいドライバーとの相互運用をサポートするように設計されている場合、オペレーティングシステムは、**内部\_デバイス\_制御**要求に対して、IRP\_MJ の一連の i/o 制御コード\_定義します。 ほとんどの場合、これらのパブリック i/o 制御コードにより、上位レベルのアドオンのドライバーは、基になるデバイスドライバーと相互運用できます。

例として、システムによって提供されるパラレルドライバーでは、ベンダーから提供されたドライバーが IRP\_\_MJ で送信する内部 i/o 制御コードのセットをサポートしています。これは、**内部\_デバイス\_制御**要求です。 詳細については、「[パラレルポートに対する内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」および「[並列デバイスの内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

システム定義の i/o 制御コードを介して要求されるほとんどすべての操作は、バッファー i/o を使用します。これは、この種類の要求で大量のデータを転送する必要がほとんどないためです。 つまり、direct i/o 用にデバイスオブジェクトを設定するドライバーであっても、AssociatedIrp (特定の種類の上位レベルを除く&gt;) でバッファーとの間で送受信されるデータを含むデバイス制御要求の Irp が送信され**ます。** Win32 マルチメディアドライバーが密接に結合されたデバイスドライバー)。

さらに、ドライバーは、他のドライバーが通信に使用できるプライベート i/o 制御コードのセットを定義できます。 公開 i/o 制御コードはオペレーティングシステム自体に組み込まれているため、新しいパブリック i/o 制御コードをシステムに追加できるのは、Microsoft Corporation と連携している場合のみです。

さまざまな種類のドライバーがサポートする必要があるパブリック i/o 制御コードのセットと、プライベート i/o 制御コードの定義については、Windows Driver Kit (WDK) のデバイス固有の参照セクションを参照してください。

 

 




