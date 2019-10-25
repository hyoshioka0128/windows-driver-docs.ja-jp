---
title: WDM デバイス オブジェクトの種類
description: WDM デバイス オブジェクトの種類
ms.assetid: 89cc888d-3097-4637-96d2-6b9c59878d2f
keywords:
- 機能デバイスオブジェクト WDK カーネル
- FDO WDK カーネル
- 物理デバイスオブジェクト WDK カーネル
- PDOs WDK カーネル
- デバイスオブジェクト WDK カーネル、種類
- DOs WDK カーネルをフィルター処理する
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420689ea8a01b49329babe95cf1f4ecec34ea7ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836097"
---
# <a name="types-of-wdm-device-objects"></a>WDM デバイス オブジェクトの種類





WDM デバイスオブジェクトには、次の3種類があります。

1.  物理デバイスオブジェクト (PDO) –バス[ドライバー](bus-drivers.md)に対するバス上のデバイスを表します。

2.  機能デバイスオブジェクト (FDO) –[関数ドライバー](function-drivers.md)に対するデバイスを表します。

3.  フィルターデバイスオブジェクト (フィルター DO) –[フィルタードライバー](filter-drivers.md)に対するデバイスを表します。

3種類のデバイスオブジェクトはすべて種類の[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)ですが、使用方法が異なり、デバイスの拡張子は異なる場合があります。

ドライバーは、デバイスオブジェクト ([**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)) を作成し、デバイススタックにアタッチすることによって、デバイスの i/o を処理するドライバーのスタックにそれ自体を追加します ([**Ioattachdevicetodevicestack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack))。 **Ioattachdevicetodevicestack**は、デバイススタックの現在の最上位を特定し、新しいデバイスオブジェクトをデバイススタックの一番上に接続します。

 

 




