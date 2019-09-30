---
title: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles レジストリツリーには、システム上のハードウェアプロファイルに関する情報が含まれています。
ms.assetid: 548d7a50-b3b1-4413-8898-9ed13bcbdcfc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f7bdd129ebe1aebba17d1c64af397af9a00921
ms.sourcegitcommit: 667b4be765b2eac6bc586d39abef3393a718b23f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71679690"
---
# <a name="hklmsystemcurrentcontrolsethardwareprofiles-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\のハードウェアレジストリツリー





**HKLM\\system\\CurrentControlSethardwareprofilesレジストリツリーには、システム上のハードウェアプロファイルに関する情報が含まれています。\\** ハードウェアプロファイルは非推奨とされており、ハードウェアプロファイルを基準として状態を保存することはできません。

代わりに、 **PLUGPLAY_REGKEY_CURRENT_HWPROFILE**を使用せずに、 **PLUGPLAY_REGKEY_DEVICE**と**PLUGPLAY_REGKEY_DRIVER**を使用して情報をグローバルに保存します。 詳細については、「 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)」を参照してください。




