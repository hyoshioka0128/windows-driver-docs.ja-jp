---
title: HKLM\SYSTEM\CurrentControlSet\Enum レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\Enum レジストリツリーには、システム上のデバイスに関する情報が含まれています。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 554502e440a88e3cb0915daa4ee8771a7bb4e43c
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278367"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\Enum レジストリツリー





**列挙**ツリーはオペレーティングシステムコンポーネントで使用するために予約されており、そのレイアウトは変更される可能性があります。 ドライバーとユーザーモードの[デバイスインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))では、このツリーから情報を抽出するために、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)や[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)などのシステム指定の関数を使用する必要があります。 *ドライバーと Windows アプリケーションがにアクセスできない****列挙型****ツリーを直接。*

 

 





