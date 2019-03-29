---
title: HKLM\SYSTEM\CurrentControlSet\Enum レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\Enum レジストリ ツリーには、システム上のデバイスに関する情報が含まれています。
ms.assetid: 9de3ca54-d23f-4ee6-a638-27e52a60dfdd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bcac6c6badc9813457b69b66db174b8a298d083
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580053"
---
# <a name="hklmsystemcurrentcontrolsetenum-registry-tree"></a>HKLM\\システム\\CurrentControlSet\\レジストリ ツリーで列挙型





**HKLM\\システム\\CurrentControlSet\\Enum**レジストリ ツリーには、システム上のデバイスに関する情報が含まれています。 PnP マネージャー名の形式でデバイスごとに、サブキーを作成する**HKLM\\システム\\CurrentControlSet\\Enum\\**<em>列挙子</em>**\\** <em>deviceID</em>します。 これらの各キー、サブキーをシステム上に存在する各デバイス インスタンスには。 このサブキーは、デバイスの説明、ハードウェア Id、互換性 Id、およびリソース要件などの情報を持っています。

**Enum**ツリーは、オペレーティング システムのコンポーネントで使用するため予約されており、レイアウトが変更される可能性が。 ドライバーとユーザー モード[デバイス インストール コンポーネント](https://msdn.microsoft.com/library/windows/hardware/ff541277)など、システムが提供する機能を使用する必要があります[ **IoGetDeviceProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff549203)と[ **SetupDiGetDeviceRegistryProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551967)、このツリーから情報を抽出します。 *ドライバーと Windows のアプリケーションにアクセスする必要がありますいない、* ***Enum*** *直接ツリーします。* 表示することができます、 **Enum**ドライバーをデバッグするときに、レジストリ エディターを使用して直接ツリー。

 

 





