---
title: デバイスとドライバーのレジストリ ツリー
description: デバイスとドライバーのレジストリ ツリー
ms.assetid: 74dc1889-26a9-47ba-8c8d-3cd6ed95cb68
keywords:
- ハードウェア キー WDK デバイスのインストール
- レジストリの WDK デバイスのインストール
- ソフトウェア キー WDK のデバイスのインストール
- デバイスのインストール WDK、レジストリ
- インストールを実行するデバイス WDK、レジストリ
- デバイスのセットアップの WDK デバイスのインストール、レジストリ
- デバイスのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c46bd37a7562cbcd78bda72a402bf3d4880ad46
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553630"
---
# <a name="registry-trees-for-devices-and-drivers"></a>デバイスとドライバーのレジストリ ツリー





レジストリの次のツリーがドライバー開発者にとって特に重要ですが (どこ**HKLM**表します**HKEY_LOCAL_MACHINE**)。

-   [HKLM\\システム\\CurrentControlSet\\サービスのレジストリ ツリー](hklm-system-currentcontrolset-services-registry-tree.md)

-   [HKLM\\システム\\CurrentControlSet\\レジストリ ツリーのコントロール](hklm-system-currentcontrolset-control-registry-tree.md)

-   [HKLM\\システム\\CurrentControlSet\\レジストリ ツリーで列挙型](hklm-system-currentcontrolset-enum-registry-tree.md)

-   [HKLM\\システム\\CurrentControlSet\\HardwareProfiles レジストリ ツリー](hklm-system-currentcontrolset-hardwareprofiles-registry-tree.md)

WDF (KMDF または UMDF) ドライバーからレジストリ キーへのアクセス方法の詳細については、次を参照してください。[ドライバーのレジストリ キーの概要](../wdf/introduction-to-registry-keys-for-drivers.md)します。

**注**  下キー **HKLM\\システム\\CurrentControlSet**システム hive でデータが格納されているため、ドライバーに重要なデータを保持するために、安全な場所は。 (たとえば、複数のコピーを維持する方法) のシステム ハイブを保護するのには追加の予防措置が取得されます。

 

 

 





