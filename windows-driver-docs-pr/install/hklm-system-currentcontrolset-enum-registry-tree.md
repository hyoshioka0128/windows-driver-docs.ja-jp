---
title: HKLM\SYSTEM\CurrentControlSet\Enum レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\Enum レジストリ ツリーには、システム上のデバイスに関する情報が含まれています。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b247b445248e624a98f7377b95a5a26d95a19f54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386411"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\レジストリ ツリーで列挙型





**HKLM\\システム\\CurrentControlSet\\Enum**レジストリ ツリーには、システム上のデバイスに関する情報が含まれています。 PnP マネージャー名の形式でデバイスごとに、サブキーを作成する**HKLM\\システム\\CurrentControlSet\\Enum\\** <em>列挙子</em> **\\** <em>deviceID</em>します。 これらの各キー、サブキーをシステム上に存在する各デバイス インスタンスには。 このサブキーは、デバイスの説明、ハードウェア Id、互換性 Id、およびリソース要件などの情報を持っています。

**Enum**ツリーは、オペレーティング システムのコンポーネントで使用するため予約されており、レイアウトが変更される可能性が。 ドライバーとユーザー モード[デバイス インストール コンポーネント](https://docs.microsoft.com/previous-versions/ff541277(v=vs.85))など、システムが提供する機能を使用する必要があります[ **IoGetDeviceProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdeviceproperty)と[ **SetupDiGetDeviceRegistryProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya)、このツリーから情報を抽出します。 *ドライバーと Windows のアプリケーションにアクセスする必要がありますいない、* ***Enum*** *直接ツリーします。* 表示することができます、 **Enum**ドライバーをデバッグするときに、レジストリ エディターを使用して直接ツリー。

 

 





