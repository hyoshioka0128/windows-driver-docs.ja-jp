---
title: DispatchDeviceControl および DispatchInternalDeviceControl ルーチン
description: DispatchDeviceControl および DispatchInternalDeviceControl ルーチン
ms.assetid: 0bf8868e-bc5a-4fa7-9ff6-270f7a7bc850
keywords:
- ディスパッチ ルーチンの WDK カーネル、DispatchDeviceControl ルーチン
- ディスパッチ ルーチンの WDK カーネル、DispatchInternalDeviceControl ルーチン
- DispatchDeviceControl ルーチン
- DispatchInternalDeviceControl ルーチン
- IRP_MJ_DEVICE_CONTROL I/O 関数のコード
- IRP_MJ_INTERNAL_DEVICE_CONTROL I/O 関数のコード
- デバイスの内部コントロール ディスパッチ ルーチン WDK カーネル
- デバイス制御ディスパッチ ルーチン WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0576b92cb428692943256f00cb4c24a73f92d6d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381710"
---
# <a name="dispatchdevicecontrol-and-dispatchinternaldevicecontrol-routines"></a>DispatchDeviceControl および DispatchInternalDeviceControl ルーチン


ドライバーのディスパッチ ルーチン (を参照してください[ **DRIVER_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)) の I/O 関数のコードの Irp の処理[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)、それぞれ.

I/O 制御コードのセットを定義しているシステムの周辺機器の一般的な種類がごと、 **IRP\_MJ\_デバイス\_コントロール**要求。 各種類のデバイス用の新しいドライバーは、これらの要求をサポートする必要があります。 ほとんどの場合、デバイスの種類ごとにパブリックこれら I/O 制御コードは、ユーザー モード アプリケーションにはエクスポートされません。 


これらシステム定義の I/O 制御コードの一部は上位レベルのドライバーが Irp を呼び出すことによって、基になるデバイス ドライバーの作成で使用[ **IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iobuilddeviceiocontrolrequest)します。 他のユーザーは、Win32 関数を呼び出すことによって、基になるデバイス ドライバーとの通信に Win32 コンポーネントによって使用される[ **DeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (Microsoft Windows SDK のドキュメントで説明) かを有効にします。システム サービスを呼び出します。 I/O マネージャーが、IRP を設定し、主要な関数のコードを格納**IRP\_MJ\_デバイス\_コントロール**とでは、特定の I/O 制御コード、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location)で構造体**Parameters.DeviceIoControl.IoControlCode**します。 次に、I/O マネージャーを呼び出す、 *DispatchDeviceControl*チェーンの最上位レベルのドライバーの日常的な。

新しいドライバーのサポートし、相互運用するように設計特定システム提供のドライバー、オペレーティング システムものセットを定義の I/O 制御コード**IRP\_MJ\_内部\_デバイス\_コントロール**要求。 ほとんどの場合では、これらのパブリックの I/O 制御コードは、基になるデバイス ドライバーを使用した相互運用するより高度なドライバーのアドオンを許可します。

システム提供平行ドライバーがドライバーのベンダーから提供された送信 I/O 制御コードが内部のセットをサポートする例として、 **IRP\_MJ\_内部\_デバイス\_コントロール**要求。 詳細については、次を参照してください。[パラレル ポートの内部のデバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[並列デバイスに対するデバイス コントロール要求は内部](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

システム定義の I/O 制御コードを通じて要求されたほぼすべての操作は、この種の要求は頻度の低い大量のデータの転送を必要とするために、バッファー内の I/O を使用します。 ダイレクト I/O に対してそのデバイス オブジェクトの設定もドライバーは Irp のバッファーの内外に転送するデータとデバイス制御要求の送信される**Irp -&gt;AssociatedIrp.SystemBuffer** (以外の特定の種類の密接に結合された Win32 マルチ メディアのドライバーのデバイス ドライバーが最上位レベル)。

さらに、ドライバーは、他のドライバーがそれとの通信に使用できるプライベートの I/O 制御コードのセットを定義できます。 パブリックの I/O 制御コードは、オペレーティング システム自体に組み込まれているために、パブリックの I/O 制御コードは新しいをのみである Microsoft Corporation と協力して、システムに追加できます。

一連のドライバーのさまざまな種類のサポートが必要な I/O 制御コードをパブリックおよびプライベートの I/O 制御コードを定義するについての詳細については、Windows Driver Kit (WDK) のデバイスに固有の参照セクションを参照してください。

 

 




