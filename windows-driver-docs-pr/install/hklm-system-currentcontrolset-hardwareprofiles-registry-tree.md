---
title: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles レジストリ ツリー
description: HKLM\SYSTEM\CurrentControlSet\HardwareProfiles レジストリツリーには、システム上のハードウェアプロファイルに関する情報が含まれています。
ms.assetid: 548d7a50-b3b1-4413-8898-9ed13bcbdcfc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 796544177efe8d764f11f66418d97369cba725fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828810"
---
# <a name="hklmsystemcurrentcontrolsethardwareprofiles-registry-tree"></a>HKLM\\SYSTEM\\CurrentControlSet\\のハードウェアプロファイルレジストリツリー





**HKLM\\system\\CurrentControlSet\\Hardware profiles**レジストリツリーには、システム上のハードウェアプロファイルに関する情報が含まれています。 ハードウェアプロファイルは非推奨とされており、ハードウェアプロファイルを基準として状態を保存することはできません。

代わりに、 **PLUGPLAY_REGKEY_CURRENT_HWPROFILE**を使用せずに、 **PLUGPLAY_REGKEY_DEVICE**と**PLUGPLAY_REGKEY_DRIVER**を使用して情報をグローバルに保存します。 詳細については、「 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)」を参照してください。




