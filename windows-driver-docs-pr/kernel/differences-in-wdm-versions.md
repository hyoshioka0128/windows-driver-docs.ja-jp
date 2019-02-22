---
title: WDM バージョン間の違い
description: WDM バージョン間の違い
ms.assetid: 735b01c4-4eff-4c8e-ab60-3813d1830112
keywords:
- WDM ドライバー WDK カーネルのバージョン
- WDK WDM のバージョン
- WDK WDM の互換性
- WDK WDM システム間の互換性
- プラグ アンド プレイ WDK WDM
- ドライバー サポート ルーチン WDK WDM
- 電源管理 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c1d4ba1aadc2d130d8760aac290af4be8631969
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538345"
---
# <a name="differences-in-wdm-versions"></a>WDM バージョン間の違い





システム間の互換性を確保する最も簡単な方法では、WDM の番号の小さい方のバージョンでサポートされている唯一の機能を使用するドライバーを作成します。 ただし、このできるとは限りません。 場合によっては、ドライバーでは、以降のバージョンの WDM で利用できる機能を活用するために、または Windows オペレーティング システムの違いを補正するコードを追加が必要です。

### <a name="wdm-differences-in-driver-support-routines"></a>WDM ドライバー サポート ルーチンの違い

Windows Driver Kit (WDK) のリファレンス ページの各[ドライバー サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544200)ルーチンが WDM の特定のバージョンに制限されている場合、またはその動作は、オペレーティング システムのバージョンでは異なる場合を示します。 システム間 driver で任意のドライバー サポート ルーチンを使用する前に必ず、バージョン固有の制限や動作を理解してください。

### <a name="wdm-differences-in-plug-and-play"></a>プラグ アンド プレイ WDM の相違点

次のプラグ アンド プレイ I/O 要求パケット (IRP) は、Windows 2000 および、NT ベース オペレーティング システム (WDM バージョン 1.10 以降) の以降のバージョンでのみサポートされます。

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://msdn.microsoft.com/library/windows/hardware/ff551760)

Windows 98 で次の Irp がさらに、異なる方法でに作業]、[NT ベースのオペレーティング システムで作業する方法から。

[**IRP\_MN\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551755)と[ **IRP\_MN\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738)

[**IRP\_MN\_クエリ\_削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551705)

### <a name="wdm-differences-in-power-management"></a>電源管理 WDM な相違点

次の電源管理機能と I/O 要求が Windows 98 の間の演算で異なる/Me オペレーティング システムと NT ベースのオペレーティング システム。

[**PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)

[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

[**PoRegisterDeviceForIdleDetection**](https://msdn.microsoft.com/library/windows/hardware/ff559721)

[**IRP\_MN\_クエリ\_電源**](https://msdn.microsoft.com/library/windows/hardware/ff551699)

[**IRP\_MN\_SET\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff551744)

電源 Irp、Windows 98 でドライバーを完了したときに IRQL で電源 Irp の完了する必要があります/= パッシブ\_レベル、NT ベースのオペレーティング システム上のドライバーが IRQL でこのような Irp を完了するまでパッシブ =\_レベルまたは IRQL = ディスパッチ\_レベルです。

DO\_POWER\_PAGABLE フラグ、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147) Windows 98 で構造体が異なる方法で使用される/Me NT ベースのよりもシステムのオペレーティングオペレーティング システム。

### <a name="wdm-differences-in-kernel-mode-driver-operation"></a>WDM カーネル モード ドライバー操作の違い

Windows 98 のカーネル モード WDM ドライバー]、[浮動小数点演算、MMX、3 dnow を使用するための特定のガイドラインに従う必要があります Me!、または Intel の SSE 拡張機能。 詳細については、次を参照してください。[を使用する浮動小数点または WDM ドライバーで MMX](using-floating-point-or-mmx-in-a-wdm-driver.md)します。

Windows 98/私の一部のドライバーに適切なことができない可能性があるワーカー スレッドの固定数を提供します。

 

 




