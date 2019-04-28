---
title: WDM デバイス オブジェクトの種類
description: WDM デバイス オブジェクトの種類
ms.assetid: 89cc888d-3097-4637-96d2-6b9c59878d2f
keywords:
- 機能のデバイス オブジェクトの WDK カーネル
- FDO WDK カーネル
- 物理デバイス オブジェクトの WDK カーネル
- Pdo WDK カーネル
- デバイス オブジェクト WDK カーネルの種類
- フィルター DOs WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed5f771e5eff6ac60f6c2b313888d7484fb4ea26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377014"
---
# <a name="types-of-wdm-device-objects"></a>WDM デバイス オブジェクトの種類





WDM デバイス オブジェクトの 3 つの種類があります。

1.  物理デバイス オブジェクト (PDO) – にバス上のデバイスを表す、[バス ドライバー](bus-drivers.md)します。

2.  機能のデバイス オブジェクト (FDO) – にデバイスを表す、[関数ドライバー](function-drivers.md)します。

3.  デバイス オブジェクトのフィルター (フィルター操作を行います) – デバイスを表します、[フィルター ドライバー](filter-drivers.md)します。

次の 3 つの種類のデバイス オブジェクトは、型のすべて[**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)が、異なる方法で使用され、別のデバイスの拡張機能を持つことができます。

ドライバーは、デバイス オブジェクトを作成してデバイスの I/O を処理するドライバーのスタックに追加します ([**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397)) と、デバイス スタックへの追加 ([ **IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300))。 **IoAttachDeviceToDeviceStack**デバイス スタックの現在の先頭を決定し、デバイス スタックの一番上に新しいデバイス オブジェクトをアタッチします。

 

 




