---
title: ベンダー提供のパラレル ドライバーの要件
description: ベンダー提供のパラレル ドライバーの要件
ms.assetid: 2194ad1a-3548-4b67-9268-4245389cf264
keywords:
- ベンダーから提供された並列ドライバー WDK、ベンダーから提供された並列ドライバーについて
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67da7d07a26993d6abedab3777478bef20e2340
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377217"
---
# <a name="requirements-for-vendor-supplied-parallel-drivers"></a>ベンダー提供のパラレル ドライバーの要件





このセクションでは、パラレル ポートおよびパラレル ポートに接続されたデバイス用のドライバーのベンダーから提供された Microsoft Windows の要件について説明します。

関数のベンダーから提供されたドライバーおよびパラレル ポート バス ドライバーは、必要なため、[システム提供平行ドライバー](system-supplied-parallel-drivers.md)これらの関数を提供します。 システム提供平行ドライバーでは、パラレル ポート、パラレル ポートに接続されたデバイスを操作するために広範なサポートを提供します。

パラレル ポートに接続されている並列のデバイスのドライバーをベンダーによって提供される関数は省略可能です。 システム提供平行ドライバー提供広範なサポート、ロウ デバイスとしての並列のデバイスを直接制御するため、デバイスの親を操作するためにパラレル ポート。

仕入先は、並列のデバイスの機能のドライバーを提供する場合、ドライバーはプラグ アンド プレイし、電源管理をサポートする必要があります。 ドライバーに WDM ドライバーがあることをお勧めします。

次のトピックでは、デバイスとデバイスの親のパラレル ポートの並列のデバイスのベンダーによって提供される関数のドライバーの動作について説明します。

[パラレル ポートの動作](operating-a-parallel-port.md)

[パラレル ポートに接続されている並列のデバイスの動作](operating-a-parallel-device-attached-to-a-parallel-port.md)

 

 




