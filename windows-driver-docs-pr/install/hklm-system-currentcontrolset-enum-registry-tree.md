---
title: HKLM\SYSTEM\CurrentControlSet\Enum レジストリツリー
description: HKLM\SYSTEM\CurrentControlSet\Enum レジストリツリーには、システム上のデバイスに関する情報が含まれています。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce6539b96c857b9cdee39f061834c10fd6a6cfad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837493"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\Enum レジストリツリー





**列挙**ツリーはオペレーティングシステムコンポーネントで使用するために予約されており、そのレイアウトは変更される可能性があります。 ドライバーとユーザーモードの[デバイスインストールコンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))では、このツリーから情報を抽出するために、 [**Iogetdeviceproperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty)や[**SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)などのシステム指定の関数を使用する必要があります。 *ドライバーと Windows アプリケーションは、列挙ツリーに直接アクセスすることはできません* *。*

 

 





