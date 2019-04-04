---
title: バス ドライバーでの PnP や電源管理のサポート
description: バス ドライバーでの PnP や電源管理のサポート
ms.assetid: 35a3d734-7d7e-46ee-aba6-fc6a579d4394
keywords:
- PnP WDK KMDF、バス ドライバー
- プラグ アンド プレイ WDK KMDF、バス ドライバー
- 電源管理 WDK KMDF、バス ドライバー
- バス ドライバー WDK KMDF
- WDK KMDF の子デバイス
- バスの WDK KMDF 列挙型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97d8e6c082ab7fe3e65f5fb8f4682f674c89cf28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552890"
---
# <a name="supporting-pnp-and-power-management-in-bus-drivers"></a>バス ドライバーでの PnP や電源管理のサポート


一部のデバイスは完全にシステムに接続されて他のユーザーに接続されているし、システムの実行中に電源が入っていないことができます。 *バス ドライバー*特定して、デバイスをレポートする必要があります、バスに接続されていると、検出し、システムでデバイスの出発と到着を報告する必要があります。

バスのバス ドライバーの識別および報告するデバイスと呼びます*子デバイス*します。 識別して、子デバイスをレポート作成のプロセスが呼び出されます*列挙体のバス*します。 バス ドライバー、バスの列挙中に[デバイス オブジェクトを作成します。](creating-a-framework-device-object.md)その子デバイス。 バスの列挙体の詳細については、[バス上のデバイスを列挙する](enumerating-the-devices-on-a-bus.md)を参照してください。

バス ドライバーとは、基本的に関数ドライバー、またはごくまれにもバス列挙型を処理するフィルター ドライバー、です。 バス ドライバーは通常、関数のドライバー、バス アダプターのですが、関数のドライバーをバスに接続されている子デバイスではありません。

バス ドライバーでは、関数のドライバーが同様の PnP や電源管理の役割もあります。 これらの役割の詳細については、[PnP をサポートしていると関数のドライバーでの電源管理](supporting-pnp-and-power-management-in-function-drivers.md)を参照してください。

 

 





