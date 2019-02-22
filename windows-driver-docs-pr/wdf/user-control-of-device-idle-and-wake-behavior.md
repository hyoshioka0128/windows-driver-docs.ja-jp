---
title: デバイスがアイドル状態とスリープ解除の動作のユーザーによる制御
description: デバイスがアイドル状態とスリープ解除の動作のユーザーによる制御
ms.assetid: 776fcf82-2235-489a-8d46-3ad230da3402
keywords:
- システム ウェイク アップ WDK KMDF
- 電源管理 WDK KMDF、ウェイク アップ機能
- ウェイク アップ機能 WDK KMDF
- 電源管理 WDK KMDF をスリープ状態します。
- 低電力状態 WDK KMDF
- 電源管理 WDK KMDF、アイドル状態の電源切断
- アイドル状態の電源切断 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 297fb89ccc37a7d2fc34f9bf40e7026941410085
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552900"
---
# <a name="user-control-of-device-idle-and-wake-behavior"></a>デバイスがアイドル状態とスリープ解除の動作のユーザーによる制御


デバイスを電源オフまたはウェイク アップ機能のアイドル状態にある場合を有効にするか、これらの機能を無効にするユーザーを許可するかどうかを決定できます。

ドライバーがのメンバーを使用できる、 [ **WDF\_デバイス\_POWER\_ポリシー\_IDLE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551270)構造体を指定するかどうかレジストリのアクセス権を持つユーザーでは、有効にしたり、デバイスのアイドル状態の電源機能を無効にすることができます。

ドライバーがのメンバーを使用できる、 [ **WDF\_デバイス\_POWER\_ポリシー\_WAKE\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff551277)構造体を指定するかどうかレジストリのアクセス権を持つユーザーでは、有効にしたり、デバイスのウェイク アップ機能を無効にすることができます。

両方これらの構造体のドライバー、機能を有効にできるように、機能を無効にするまたはユーザー機能を制御できるようにします。 ユーザーが制御できる、適切な設定で、ドライバー構造体を設定、 **UserControlOfIdleSettings**または**UserControlOfWakeSettings**メンバー **IdleAllowUserControl**または**WakeAllowUserControl**をそれぞれ、**有効**メンバー **WdfTrue**または**WdfUseDefault**,.

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、デバイス マネージャーの表示を有効にするか、アイドル状態を無効にして機能を wake ユーザーようにするプロパティ シート ページの形式でのユーザー インターフェイスを提供します。 (フレームワークを変更します**IdleInWorkingState**と**WakeFromSleepState**レジストリの値。 ドライバーとそのインストール ファイルにする必要があります*いない*読み取り、またはこれらの値を変更します)。

デバイスの設定を変更した場合、フレームワークは必要に応じて、新しい設定を一致するように、デバイスの電源の状態を更新します。 たとえば場合は、ユーザーは、デバイスは低電力状態で既にはアイドル状態だったために、デバイスのアイドル状態の電源機能を無効に、フレームワークは稼働状態にデバイスを返します。

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、既定でこれらの設定を有効。 にします。 いくつかのドライバー開発者は、最初にそれらを変更するユーザーを許可する前に、設定を無効にする可能性があります。

そのため、バージョン 1.9 および KMDF の以降のバージョンでは、フレームワークは、という名前の 2 つのドライバー定義可能なレジストリ値**WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**、デバイスの保存されている**デバイス パラメーター\\WDF**デバイスのハードウェア キーの下のサブキー。 値は、REG\_「0」、DWORD に型指定された機能を示すは無効になり、機能を示す「1」を有効にします。

ドライバーの INF ファイルが使用できる、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)を作成し、設定、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**レジストリの値。 たとえば、により、デバイスのアイドル状態の電源機能、ドライバーがドライバーの INF ファイルを設定できる場合は、デバイスがインストールされている場合は、機能を無効にする必要があります、 **WdfDefaultIdleInWorkingState** 「0」にします。

フレームワークを調べ、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**レジストリ値は、ドライバーが設定されている場合にのみ、 **UserControlOfIdleSettings**または**UserControlOfWakeSettings**メンバー **IdleAllowUserControl**または**WakeAllowUserControl**、それぞれ、および、 **有効**メンバー **WdfTrue**または**WdfUseDefault**、適切な設定の構造体。

 

 





