---
title: デバイスとドライバーのレジストリ ツリー
description: デバイスとドライバーのレジストリ ツリー
ms.assetid: 74dc1889-26a9-47ba-8c8d-3cd6ed95cb68
keywords:
- ハードウェアキー WDK デバイスのインストール
- レジストリ WDK デバイスのインストール
- ソフトウェアキー WDK デバイスのインストール
- デバイスのインストール WDK、レジストリ
- デバイスのインストール WDK、レジストリ
- デバイスのセットアップ WDK デバイスのインストール、レジストリ
- デバイスのデバッグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30d64107d1e52dfe83a917dc914e34003357357e
ms.sourcegitcommit: e480dcfea893ef6c85b2dfb5827f51b740466262
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "71278371"
---
# <a name="registry-trees-for-devices-and-drivers"></a>デバイスとドライバーのレジストリ ツリー





レジストリ内の次のツリーは、ドライバーの作成者にとって特に重要です ( **HKLM**は**HKEY_LOCAL_MACHINE**を表します)。

-   [HKLM\\SYSTEM\\CurrentControlSet\\Services レジストリツリー](hklm-system-currentcontrolset-services-registry-tree.md)

-   [HKLM\\システム\\CurrentControlSet\\Control レジストリツリー](hklm-system-currentcontrolset-control-registry-tree.md)

-   [HKLM\\システム\\CurrentControlSet\\Enum レジストリツリー](hklm-system-currentcontrolset-enum-registry-tree.md)

-   [HKLM\\SYSTEM\\CurrentControlSet\\のハードウェアレジストリツリー](hklm-system-currentcontrolset-hardwareprofiles-registry-tree.md)

WDF (KMDF または UMDF) ドライバーからのレジストリキーへのアクセスの詳細については、「[ドライバーのレジストリキーの概要](../wdf/introduction-to-registry-keys-for-drivers.md)」を参照してください。

WDM ドライバーからのレジストリキーへのアクセスの詳細については、「[プラグアンドプレイレジストリルーチン](../kernel/plug-and-play-registry-routines.md)」を参照してください。
 

 

 





