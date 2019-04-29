---
title: UEFI バッテリ充電プロトコル
description: UEFI バッテリ充電プロトコル
ms.assetid: 5e9ef620-2ca1-4579-a715-19eec8933d57
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dbc2d4e762a55196407854999932cd51370abb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337418"
---
# <a name="uefi-battery-charging-protocol"></a>UEFI バッテリ充電プロトコル


**注**  このセクションの一部の情報は、Windows 10 Mobile と特定のプロセッサ アーキテクチャにのみ適用可能性があります。

 

UEFI のバッテリ充電プロトコルは、UEFI のバッテリ充電ドライバーとの通信に Microsoft UEFI バッテリの充電中のアプリケーションによって使用されます。 UEFI のバッテリ充電ドライバーは、デバイスで Microsoft UEFI バッテリの充電中のアプリケーションを使用する場合、このプロトコルを実装する必要があります。

**重要な**  UEFI バッテリのドライバーを充電する必要があります、このプロトコルを実装していません、デバイスは、カスタム UEFI バッテリが充電、Microsoft が提供するアプリケーションではなくアプリケーションを使用している場合。 Windows ブート マネージャーでは、ドライバーは、このプロトコルを実装している場合は、アプリケーションを課金 Microsoft UEFI バッテリを読み込みます。

 

Microsoft UEFI バッテリが充電アプリケーションの詳細については、次を参照してください。[ブート環境でバッテリが充電中](battery-charging-in-the-boot-environment.md)します。

## <a name="protocol-interface"></a>プロトコル インターフェイス


-   [EFI\_バッテリ\_充電中\_プロトコル](efi-battery-charging-protocol.md)

-   [EFI\_バッテリ\_充電中\_プロトコル。GetBatteryInformation](efi-battery-charging-protocolgetbatteryinformation.md)

-   [EFI\_バッテリ\_充電中\_プロトコル。GetBatteryStatus](efi-battery-charging-protocolgetbatterystatus.md)

-   [EFI\_バッテリ\_充電中\_プロトコル。ChargeBattery](efi-battery-charging-protocolchargebattery.md)

Windows ブート フローでは、メインの OS を読み込むことができます、前に特定のレベルに課金するバッテリが必要です。 UEFI 仕様バージョン 2.3 では、標準のバッテリが充電プロトコルがありません。

### <a name="sequence-diagram"></a>シーケンス図

![uefi バッテリの充電シーケンス図](images/uefibatterychargingsequencediagram.png)

 

 




