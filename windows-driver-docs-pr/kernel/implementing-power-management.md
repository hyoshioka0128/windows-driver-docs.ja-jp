---
title: Windows ドライバーの電源管理
description: オンであり、必要なときに使用できますが、低電力モードで動作し、使用されていないときは、不要なシステム アクティビティ生成しないように、カーネル モード ドライバーでは、ハードウェア デバイスを管理する必要があります。
ms.assetid: ed422428-8a87-4a2d-830d-e156ef949b13
keywords:
- 電源管理の WDK カーネル
- カーネル モード ドライバー WDK、電源管理
- エネルギー WDK 電源管理
- スタートアップの電源管理の WDK カーネル
- シャット ダウンの電源管理の WDK カーネル
- デバイスの電源管理の WDK カーネル
- WDK カーネルの電源を復元します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec7e98caba00db18d17045e9f7c6bed8ece5065a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531826"
---
# <a name="power-management-for-windows-drivers"></a>Windows ドライバーの電源管理


オンであり、必要なときに使用できますが、低電力モードで動作し、使用されていないときは、不要なシステム アクティビティ生成しないように、カーネル モード ドライバーでは、ハードウェア デバイスを管理する必要があります。 [*電源マネージャー* ](power-manager.md)は Windows カーネル コンポーネントのハードウェア プラットフォームでデバイスの電源の状態を調整するためです。




電源マネージャーを準備する低電力モード、およびドライバーを入力するようにデバイスから通知を受け取る電源マネージャー オンにすると自分のデバイスが戻るときにドライバーを指示します。 ドライバーが電源マネージャーに、電源機能を報告する責任を負います。 ドライバーでは、自分のデバイスがアイドル状態 (と低電力モードに切り替えることができます) を検出またはこのような検出の電源マネージャーで証明書利用者のオプションがあります。

## <a name="in-this-section"></a>このセクションの内容


-   [電源管理の概要](introduction-to-power-management.md)
-   [カーネル モードの電源管理のコンポーネント](kernel-mode-power-management-components.md)
-   [ドライバーの電源管理の責任](power-management-responsibilities-for-drivers.md)
-   [電源 Irp を処理するための規則](rules-for-handling-power-irps.md)
-   [個々 のデバイスの電源を管理します。](managing-power-for-individual-devices.md)
-   [システム電源の状態の処理の要求](handling-system-power-state-requests.md)
-   [電源管理フレームワークの概要](overview-of-the-power-management-framework.md)
-   [プラットフォーム拡張機能プラグイン (Pep)](platform-extension-plug-ins--peps-.md)
-   [ウェイク アップ機能を備えたデバイスのサポート](supporting-devices-that-have-wake-up-capabilities.md)
-   [システム起動時のパフォーマンスの向上](improving-system-startup-performance.md)
-   [デバイス レベルの温度管理](device-level-thermal-management.md)

 

 




