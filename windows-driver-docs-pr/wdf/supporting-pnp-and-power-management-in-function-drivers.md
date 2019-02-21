---
title: 関数のドライバーでの PnP や電源管理のサポート
description: 関数のドライバーでの PnP や電源管理のサポート
ms.assetid: 487d4a69-a8a8-406c-8572-688388deabe3
keywords:
- PnP WDK KMDF、関数のドライバー
- プラグ アンド プレイ WDK KMDF、関数のドライバー
- 電源管理 WDK KMDF、関数のドライバー
- 機能ドライバー WDK KMDF
- 電源ポリシー WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3097fd14a14bafcf9f618984b6f8e9b5ad404c48
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559856"
---
# <a name="supporting-pnp-and-power-management-in-function-drivers"></a>関数のドライバーでの PnP や電源管理のサポート


*関数のドライバー*デバイスの操作を制御し、デバイスのハードウェアにアクセスするためです。 これらのドライバーの PnP や電源管理操作をサポートして、通常いくつかのイベントのコールバック関数を登録する必要があるときに、[デバイス オブジェクトを作成する](creating-a-framework-device-object.md)します。

通常、関数ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)イベント コールバック関数の呼び出し[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135)次のコールバック関数を登録します。

-   [*EvtDevicePrepareHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540880)ドライバーにデバイスのシステムによって割り当てられたリソースを提供します。 ドライバーは、ハードウェアをドライバーにアクセスできるように、プロセッサの仮想アドレス空間に、デバイスのバスの相対メモリのマッピングなどの操作を実行できます。

-   [*EvtDeviceD0Entry*](https://msdn.microsoft.com/library/windows/hardware/ff540848)ドライバーのデバイスがその作業 (D0) 状態になるなど、読み込み、ファームウェアであるために必要なするごとに、操作を実行します。

-   [*EvtDeviceD0Exit*](https://msdn.microsoft.com/library/windows/hardware/ff540855)ドライバーのデバイスがの作業 (D0) 状態のままし、低電力状態に入るたびに必要な操作を実行します。

-   [*EvtDeviceReleaseHardware*](https://msdn.microsoft.com/library/windows/hardware/ff540890)、システム リソースを解放するを[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)割り当てられます。

すべてのフレームワークで定義されたコールバック関数と同様に、上記の一覧で使用されているは省略可能です。 ドライバーでは、その必要がある場合にのみ、それらを指定するがあります。

ドライバーの関数を呼び出すことができます[ **WdfDeviceSetPnpCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff546898)と[ **WdfDeviceSetPowerCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/ff546901)デバイスの PnP を報告してオペレーティング システムに電源管理機能。

通常、フレームワークを使用する*電源管理対象の I/O キュー*ほとんどの I/O 要求。 I/O キューが電源管理対象の場合、フレームワークは、デバイスの作業 (D0) 状態にある場合にのみ、ドライバーに要求を配信します。 電源管理対象の I/O キューの詳細については、次を参照してください。[の I/O キューの電源管理](power-management-for-i-o-queues.md)します。

通常、デバイスの機能のドライバーは、*電源ポリシー所有者*ドライバー スタックの。 電源ポリシー所有者は、適切な決定[デバイスの電源状態](https://msdn.microsoft.com/library/windows/hardware/ff543162)デバイスの電源の状態が変更されるたびに、デバイスのドライバー スタックへのデバイスと送信要求。 Framework ベースのドライバーでは、フレームワークは、ドライバーのデバイスの電源状態の変更を要求するコードを指定する必要はありませんので、責任を処理します。

電源ポリシーの所有者が 2 つの責任を負う: がアイドル状態と、システムのままにする場合は、低電力状態を入力するデバイスの機能を制御、 [(S0) の状態を操作](https://msdn.microsoft.com/library/windows/hardware/ff564591)、生成するデバイスの機能を制御し、低電力状態から外部イベントを検出した場合に、信号をスリープ解除します。 場合は、デバイスがアイドル状態または機能をスリープ解除、関数には、ドライバーは追加のコールバック関数を提供できます。 電源ポリシーの所有者の役割の詳細については、次を参照してください。[電源ポリシー所有権](power-policy-ownership.md)します。

 

 





