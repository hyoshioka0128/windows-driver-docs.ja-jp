---
title: デバイスのアイドル動作とウェイク動作のユーザーによる制御
description: デバイスのアイドル動作とウェイク動作のユーザーによる制御
ms.assetid: 776fcf82-2235-489a-8d46-3ad230da3402
keywords:
- システムウェイクアップ WDK KMDF
- 電源管理 WDK KMDF、ウェイクアップ機能
- ウェイクアップ機能 WDK KMDF
- スリープ電源管理 WDK KMDF
- 低電力状態 WDK KMDF
- 電源管理 WDK KMDF、アイドル電力ダウン
- アイドル状態の電源ダウン WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e1d3ab76ce09e6c92c211a00a1355af6dec2f06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843105"
---
# <a name="user-control-of-device-idle-and-wake-behavior"></a>デバイスのアイドル動作とウェイク動作のユーザーによる制御


デバイスにアイドル状態の電源またはウェイクアップ機能がある場合は、ユーザーがこれらの機能を有効または無効にできるようにするかどうかを決定できます。

ドライバーは、 [**WDF\_デバイス\_電源\_ポリシー\_アイドル\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)構造のメンバーを使用して、レジストリアクセス権を持つユーザーがデバイスのアイドル状態の電源をオンまたはオフにできるかどうかを指定できます。

ドライバーは、 [**WDF\_デバイス\_電源\_ポリシー\_wake\_SETTINGS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_wake_settings)構造体のメンバーを使用して、レジストリアクセス権を持つユーザーがデバイスのウェイクアップ機能を有効または無効にできるかどうかを指定できます。

これらの構造体の両方で、ドライバーが機能を有効にしたり、機能を無効にしたり、ユーザーが機能を制御したりできるようにします。 ユーザーが制御できるようにするには、適切な設定の構造で、 **UserControlOfIdleSettings**または**UserControlOfWakeSettings**メンバーをそれぞれ**IdleAllowUserControl**または**WakeAllowUserControl**に設定します。**有効な**メンバーを**wdftrue**または**wdfusedefault に設定**します。

ユーザーがドライバーでアイドル状態とウェイク設定を変更できるようになった場合、フレームワークには、ユーザーがアイドルおよびウェイク機能を有効または無効にできるようにデバイスマネージャー表示されるプロパティシートページの形式でユーザーインターフェイスが用意されています。 (フレームワークによって、レジストリ値**IdleInWorkingState**と**WakeFromSleepState**が変更されます。 ドライバーとそのインストールファイルは、これらの値の読み取りや変更を行う*ことはできません*)。

ユーザーがデバイスの設定を変更すると、必要に応じて、フレームワークによって、新しい設定と一致するようにデバイスの電源状態が更新されます。 たとえば、ユーザーがデバイスのアイドル状態になっているときに、デバイスがアイドル状態になっているときに、デバイスのアイドル状態になっている機能を無効にすると、フレームワークはそのデバイスを動作状態に戻します。

ユーザーがドライバーでアイドル設定とウェイク設定を変更できるようにすると、フレームワークは既定でこれらの設定を有効にします。 一部のドライバーの作成者は、設定を変更できるようにする前に、最初に設定を無効にすることができます。

したがって、バージョン1.9 以降の KMDF の場合、フレームワークには、デバイスのデバイスに格納されている**WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**という2つのドライバー定義可能なレジストリ値が用意されています。 **パラメーター\\WDF**サブキーは、デバイスのハードウェアキーの下にあります。 値は、"0" を使用して、機能が無効になっていることを示す "0" と、機能が有効になっていることを示す "1" が指定されている場合\_は、"0"

ドライバーの INF ファイルでは、 [**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**のレジストリ値を作成および設定できます。 たとえば、ドライバーによってデバイスのアイドル電力が有効になっているが、デバイスのインストール時に機能を無効にする必要がある場合、ドライバーの INF ファイルは**WdfDefaultIdleInWorkingState**を "0" に設定できます。

このフレームワークは、ドライバーが**UserControlOfIdleSettings**または**UserControlOfWakeSettings**メンバーをに設定している場合にのみ、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**のレジストリ値を**調べます。** 適切な設定構造で、IdleAllowUserControl または**WakeAllowUserControl**、それぞれ、**有効な**メンバーを**Wdftrue**または**wdfusedefault**に設定します。

 

 





