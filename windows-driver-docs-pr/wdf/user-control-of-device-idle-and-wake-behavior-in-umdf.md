---
title: デバイスのユーザーによる制御がアイドル状態し、復帰の UMDF での動作
description: デバイスのユーザーによる制御がアイドル状態し、復帰の UMDF での動作
ms.assetid: 9341c412-dd0a-4e80-a164-250e24004082
keywords:
- 電源管理 WDK UMDF、アイドル状態の電源切断
- 電源管理 WDK UMDF、ウェイク アップ
- WDK UMDF アイドル状態の電源機能
- アイドル状態の電源機能 WDK UMDF、ユーザー コントロール
- ウェイク アップ機能 WDK UMDF
- ウェイク アップ機能 WDK UMDF、ユーザー コントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80ac6ca9101131ed31599c38ef425ffa5e3928f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539118"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>デバイスのユーザーによる制御がアイドル状態し、復帰の UMDF での動作


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスを電源オフまたはウェイク アップ機能のアイドル状態にある場合を有効にするか、これらの機能を無効にするユーザーを許可するかどうかを決定できます。

UMDF ドライバーを使用できる、 [ **IWDFDevice2::AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920)レジストリへのアクセスを持つユーザーが有効にするか、デバイスのアイドル状態の電源機能を無効にするかを指定します。

ドライバーを使用できます、 [ **IWDFDevice2::AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)レジストリへのアクセスを持つユーザーが有効にするか、デバイスのウェイク アップ機能を無効にするかを指定します。

両方のこれらのメソッド、ドライバー、機能を有効にできるように、機能を無効にするまたはユーザー機能を制御できるように。

-   ドライバーを呼び出すと、 **AssignS0IdleSettings**メソッド、そのユーザーに付与できますデバイスのアイドル状態の機能の制御を設定して、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**と設定、*有効*パラメーターを**WdfTrue**または**WdfUseDefault**します。

-   ドライバーを呼び出すと、 **AssignSxWakeSettings**メソッド、そのユーザーに付与できますデバイスのウェイク アップ機能の制御を設定して、 *UserControlOfWakeSettings*パラメーターを**WakeAllowUserControl**と設定、*有効*パラメーターを**WdfTrue**または**WdfUseDefault**します。

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、デバイス マネージャーの表示を有効にするか、アイドル状態を無効にして機能を wake ユーザーようにするプロパティ シート ページの形式でのユーザー インターフェイスを提供します。 (フレームワークを変更します**IdleInWorkingState**と**WakeFromSleepState**レジストリの値。 ドライバーとそのインストール ファイルする必要がありますいない読み取りまたはこれらの値を変更します。)

デバイスの設定を変更した場合、フレームワークは必要に応じて、新しい設定を一致するように、デバイスの電源の状態を更新します。 たとえば場合は、ユーザーは、デバイスは低電力状態で既にはアイドル状態だったために、デバイスのアイドル状態の電源機能を無効に、フレームワークは稼働状態にデバイスを返します。

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、既定でこれらの設定を有効。 にします。 いくつかのドライバー開発者は、最初にそれらを変更するユーザーを許可する前に、設定を無効にする可能性があります。

そのため、バージョン 1.9 以降のフレームワークがという名前の 2 つのドライバー定義可能なレジストリ値を提供**WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**に格納されていますが、デバイスの**デバイス パラメーター\\WDF**デバイスの下のサブキー[ハードウェア キー](https://msdn.microsoft.com/library/windows/hardware/ff561381)します。 値は、REG\_「0」、DWORD に型指定された機能を示すは無効になり、機能を示す「1」を有効にします。

ドライバーの INF ファイルが使用できる、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320)を作成し、設定、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**レジストリの値。 たとえば、により、デバイスのアイドル状態の電源機能、ドライバーがドライバーの INF ファイルを設定できる場合は、デバイスがインストールされている場合は、機能を無効にする必要があります、 **WdfDefaultIdleInWorkingState** 「0」にします。

フレームワークを調べ、 **WdfDefaultIdleInWorkingState**レジストリ値、ドライバーを設定する場合にのみ、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**と*有効*パラメーターを**WdfTrue**または**WdfUseDefault**ドライバーを呼び出すと、 [ **IWDFDevice2:。AssignS0IdleSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556920)メソッド。

フレームワークを調べ、 **WdfDefaultWakeFromSleepState**レジストリ値は、ドライバーを設定する場合にのみ、 *UserControlOfWakeSettings*パラメーターを**IWakeAllowUserControl**と*有効*パラメーターを**WdfTrue**または**WdfUseDefault**ドライバーを呼び出すと、 [ **IWDFDevice2:。AssignSxWakeSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff556923)メソッド。

 

 





