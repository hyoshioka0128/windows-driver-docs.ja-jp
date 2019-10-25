---
title: WDM バージョンの相違点
description: WDM バージョンの相違点
ms.assetid: 735b01c4-4eff-4c8e-ab60-3813d1830112
keywords:
- WDM ドライバー WDK カーネル、バージョン
- バージョン WDK WDM
- 互換性 WDK WDM
- クロスシステム互換性 WDK WDM
- WDK WDM のプラグアンドプレイ
- ドライバーサポートルーチン WDK WDM
- 電源管理 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d44dc520ab0e86eb200a8b5b9a9e3f2ec574113
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838738"
---
# <a name="differences-in-wdm-versions"></a>WDM バージョンの相違点





システム間の互換性を確保する最も簡単な方法は、WDM の最低番号バージョンでサポートされている機能のみを使用するドライバーを作成することです。 ただし、これは常に可能であるとは限りません。 場合によっては、新しいバージョンの WDM で使用できる機能を利用したり、Windows オペレーティングシステム間の違いを補うために、追加のコードが必要になることがあります。

### <a name="wdm-differences-in-driver-support-routines"></a>WDM のドライバーサポートルーチンの相違点

各[ドライバーサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の Windows Driver KIT (WDK) のリファレンスページでは、ルーチンが特定のバージョンの WDM に限定されているかどうか、またはオペレーティングシステムのバージョンによって動作が異なるかどうかが示されます。 クロスシステムドライバーでドライバーサポートルーチンを使用する前に、バージョン固有の制限または動作について理解しておく必要があります。

### <a name="wdm-differences-in-plug-and-play"></a>プラグアンドプレイの WDM の相違点

次のプラグアンドプレイ i/o 要求パケット (IRP) は、Windows 2000 以降のバージョンの NT ベースのオペレーティングシステム (WDM バージョン1.10 以降) でのみサポートされています。

[**IRP\_\_驚く\_削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

さらに、次の Irp は、NT ベースのオペレーティングシステムでの作業方法と Windows 98/Me で動作が異なります。

[**Irp\_、\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)と irp\_\_停止し\_[**デバイスを削除\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_\_クエリ\_\_デバイスの削除**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

### <a name="wdm-differences-in-power-management"></a>WDM の電源管理の相違点

次の電源管理機能と i/o 要求は、Windows 98/Me オペレーティングシステムと NT ベースのオペレーティングシステムの間で動作が異なります。

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**IRP\_\_クエリ\_電力**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_\_設定\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

電源 Irp を完了するとき、Windows 98/Me のドライバーは、IRQL = パッシブ\_レベルで電源 Irp を完了する必要があります。一方、NT ベースのオペレーティングシステム上のドライバーは、IRQL = パッシブ\_レベルまたは IRQL = ディスパッチ\_レベルでこのような Irp を完了できます。

[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の DO\_POWER\_pagable フラグは、NT ベースのオペレーティングシステムとは異なる方法で、Windows 98/Me オペレーティングシステムで使用されます。

### <a name="wdm-differences-in-kernel-mode-driver-operation"></a>カーネルモードドライバー操作の WDM の相違点

Windows 98/Me 用のカーネルモード WDM ドライバーは、浮動小数点演算、MMX、3DNOW!、または Intel の SSE 拡張機能を使用するための特定のガイドラインに従う必要があります。 詳細については、「 [WDM ドライバーでの浮動小数点または MMX の使用](using-floating-point-or-mmx-in-a-wdm-driver.md)」を参照してください。

Windows 98/Me では、一部のドライバーに対して十分ではない可能性のある固定数のワーカースレッドを提供しています。

 

 




