---
title: I/O 制御コードの概要
description: I/O 制御コードの概要
ms.assetid: 8b9e09ef-56f9-42b9-9b65-04bc380f3a1e
keywords:
- I/o 制御コード WDK カーネル、i/o 制御コードについて
- コントロールコード WDK Ioctl、i/o 制御コードについて
- Ioctl WDK カーネル、i/o 制御コードについて
- プライベート Ioctl WDK カーネル
- パブリック Ioctl WDK カーネル
- Ioctl WDK ユーザーモード
- ユーザーモードコンポーネント WDK Ioctl
- I/o 制御コード WDK ユーザーモード
- コントロールコード WDK ユーザーモード
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11e88ea3f951dd148e8f69ebee6a3b489ec91c07
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828211"
---
# <a name="introduction-to-io-control-codes"></a>I/O 制御コードの概要





I/o 制御コード (Ioctl) は、ユーザーモードのアプリケーションとドライバー間の通信、またはスタック内のドライバー間の内部通信に使用されます。 I/o 制御コードは、Irp を使用して送信されます。

ユーザーモードのアプリケーションは、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出すことによって、ioctl をドライバーに送信します。これについては Microsoft Windows SDK のドキュメントを参照してください。 **DeviceIoControl**を呼び出すと、i/o マネージャーによって[**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求が作成され、最上位のドライバーに送信されます。

さらに、上位レベルのドライバーは、 **irp\_MJ\_デバイス\_コントロール**または[**irp\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求を作成して送信することによって、下位レベルのドライバーに ioctl を送信できます。 ドライバーは、 [*DispatchDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)および[*DispatchInternalDeviceControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンでこれらの要求を処理します。 (ユーザーモードのアプリケーションは、 **IRP\_MJ\_内部\_デバイス\_制御**要求を送信することはできません)。

一部の Ioctl は "public" であり、一部は "プライベート" です。 一般に、パブリック Ioctl は、Windows Driver Kit (WDK) または Windows SDK のいずれかで、Microsoft によってシステム定義および文書化されています。 ユーザーモードコンポーネントから[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)への呼び出しによって送信される場合もあれば、1つのカーネルモードドライバーから別のカーネルモードドライバーに送信される場合もあります。その場合は、 **irp\_MJ\_デバイス\_CONTROL**または**irp\_MJ\_INTERNAL を使用します。デバイス\_制御**要求を\_します。 パブリック Ioctl の例としては、 [SCSI ポート I/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)や[I8042prt Mouse 内部デバイス制御要求](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)などがあります。

一方、プライベート Ioctl は、互いに通信するためにベンダーのソフトウェアコンポーネントによって排他的に使用されることを意図しています。 プライベート Ioctl は、通常、ベンダーが提供するヘッダーファイルで定義され、一般には文書化されていません。 パブリック Ioctl と同様に、ユーザーモードコンポーネントの[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)への呼び出しによって送信される場合や、1つのカーネルモードドライバーから別のカーネルモードドライバーに送信される場合があります。そのためには、 **irp\_MJ\_デバイス\_CONTROL**または**irp\_MJ を使用します。内部の\_デバイス\_制御**要求を\_します。

パブリックとプライベートの両方の Ioctl のコーディングに違いはありません。 ただし、システム定義の Ioctl に使用されるものと比較して、ベンダー定義の Ioctl で使用できる内部コードに違いがあります。 使用可能なパブリック Ioctl がニーズに合わない場合は、ソフトウェアコンポーネントが相互に通信するために使用できる新しいプライベート Ioctl を定義できます。 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

 

 




