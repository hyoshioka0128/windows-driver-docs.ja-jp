---
title: UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御
description: UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御
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
ms.openlocfilehash: a7afe8c59c505156f942632b254417ed49cfb917
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372297"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスを電源オフまたはウェイク アップ機能のアイドル状態にある場合を有効にするか、これらの機能を無効にするユーザーを許可するかどうかを決定できます。

UMDF ドライバーを使用できる、 [ **IWDFDevice2::AssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)レジストリへのアクセスを持つユーザーが有効にするか、デバイスのアイドル状態の電源機能を無効にするかを指定します。

ドライバーを使用できます、 [ **IWDFDevice2::AssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)レジストリへのアクセスを持つユーザーが有効にするか、デバイスのウェイク アップ機能を無効にするかを指定します。

両方のこれらのメソッド、ドライバー、機能を有効にできるように、機能を無効にするまたはユーザー機能を制御できるように。

-   ドライバーを呼び出すと、 **AssignS0IdleSettings**メソッド、そのユーザーに付与できますデバイスのアイドル状態の機能の制御を設定して、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**と設定、*有効*パラメーターを**WdfTrue**または**WdfUseDefault**します。

-   ドライバーを呼び出すと、 **AssignSxWakeSettings**メソッド、そのユーザーに付与できますデバイスのウェイク アップ機能の制御を設定して、 *UserControlOfWakeSettings*パラメーターを**WakeAllowUserControl**と設定、*有効*パラメーターを**WdfTrue**または**WdfUseDefault**します。

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、デバイス マネージャーの表示を有効にするか、アイドル状態を無効にして機能を wake ユーザーようにするプロパティ シート ページの形式でのユーザー インターフェイスを提供します。 (フレームワークを変更します**IdleInWorkingState**と**WakeFromSleepState**レジストリの値。 ドライバーとそのインストール ファイルする必要がありますいない読み取りまたはこれらの値を変更します。)

デバイスの設定を変更した場合、フレームワークは必要に応じて、新しい設定を一致するように、デバイスの電源の状態を更新します。 たとえば場合は、ユーザーは、デバイスは低電力状態で既にはアイドル状態だったために、デバイスのアイドル状態の電源機能を無効に、フレームワークは稼働状態にデバイスを返します。

ドライバーは、ユーザーがアイドル状態の変更し、復帰の設定を許可している場合、フレームワークは、既定でこれらの設定を有効。 にします。 いくつかのドライバー開発者は、最初にそれらを変更するユーザーを許可する前に、設定を無効にする可能性があります。

そのため、バージョン 1.9 以降のフレームワークがという名前の 2 つのドライバー定義可能なレジストリ値を提供**WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**に格納されていますが、デバイスの**デバイス パラメーター\\WDF**デバイスの下のサブキー[ハードウェア キー](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)します。 値は、REG\_「0」、DWORD に型指定された機能を示すは無効になり、機能を示す「1」を有効にします。

ドライバーの INF ファイルが使用できる、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を作成し、設定、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**レジストリの値。 たとえば、により、デバイスのアイドル状態の電源機能、ドライバーがドライバーの INF ファイルを設定できる場合は、デバイスがインストールされている場合は、機能を無効にする必要があります、 **WdfDefaultIdleInWorkingState** 「0」にします。

フレームワークを調べ、 **WdfDefaultIdleInWorkingState**レジストリ値、ドライバーを設定する場合にのみ、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**と*有効*パラメーターを**WdfTrue**または**WdfUseDefault**ドライバーを呼び出すと、 [ **IWDFDevice2:。AssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッド。

フレームワークを調べ、 **WdfDefaultWakeFromSleepState**レジストリ値は、ドライバーを設定する場合にのみ、 *UserControlOfWakeSettings*パラメーターを**IWakeAllowUserControl**と*有効*パラメーターを**WdfTrue**または**WdfUseDefault**ドライバーを呼び出すと、 [ **IWDFDevice2:。AssignSxWakeSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッド。

 

 





