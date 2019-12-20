---
title: UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御
description: UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御
ms.assetid: 9341c412-dd0a-4e80-a164-250e24004082
keywords:
- 電源管理 WDK UMDF、アイドル電力ダウン
- 電源管理 WDK UMDF、ウェイクアップ
- アイドル状態の電源ダウン機能 WDK UMDF
- アイドル電力ダウン機能 WDK UMDF、ユーザーコントロール
- ウェイクアップ機能 WDK UMDF
- ウェイクアップ機能 WDK UMDF、ユーザーコントロール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf0810008190c1e8f3efdd449fd4f8665ad6943a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210242"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

デバイスにアイドル状態の電源またはウェイクアップ機能がある場合は、ユーザーがこれらの機能を有効または無効にできるようにするかどうかを決定できます。

UMDF ベースのドライバーでは、 [**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッドを使用して、レジストリアクセスを持つユーザーがデバイスのアイドル状態の電源をオンまたはオフにできるかどうかを指定できます。

ドライバーは、 [**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッドを使用して、レジストリアクセスを持つユーザーがデバイスのウェイクアップ機能を有効または無効にできるかどうかを指定できます。

どちらの方法でも、ドライバーは機能を有効にしたり、機能を無効にしたり、ユーザーが機能を制御したりできるようにします。

-   ドライバーは、 **AssignS0IdleSettings**メソッドを呼び出すと、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue**または**wdfusedefault**に設定することによって、デバイスのアイドル状態をユーザーが制御できるようになります。

-   ドライバーは、 **AssignSxWakeSettings**メソッドを呼び出すと、 *UserControlOfWakeSettings*パラメーターを**WakeAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue**または**wdfusedefault**に設定することによって、デバイスのウェイクアップ機能をユーザーが制御できるようにします。

ユーザーがドライバーでアイドル状態とウェイク設定を変更できるようになった場合、フレームワークには、ユーザーがアイドルおよびウェイク機能を有効または無効にできるようにデバイスマネージャー表示されるプロパティシートページの形式でユーザーインターフェイスが用意されています。 (フレームワークによって、レジストリ値**IdleInWorkingState**と**WakeFromSleepState**が変更されます。 ドライバーとそのインストールファイルは、これらの値の読み取りや変更を行うことはできません)。

ユーザーがデバイスの設定を変更すると、必要に応じて、フレームワークによって、新しい設定と一致するようにデバイスの電源状態が更新されます。 たとえば、ユーザーがデバイスのアイドル状態になっているときに、デバイスがアイドル状態になっているときに、デバイスのアイドル状態になっている機能を無効にすると、フレームワークはそのデバイスを動作状態に戻します。

ユーザーがドライバーでアイドル設定とウェイク設定を変更できるようにすると、フレームワークは既定でこれらの設定を有効にします。 一部のドライバーの作成者は、設定を変更できるようにする前に、最初に設定を無効にすることができます。

したがって、バージョン1.9 以降のフレームワークでは、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**という2つのドライバーで定義可能なレジストリ値が提供されます。これらは、デバイスの[ハードウェアキー](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)の下にあるデバイスの**デバイスパラメーター\\WDF**サブキーに格納されます。 値は、"0" を使用して、機能が無効になっていることを示す "0" と、機能が有効になっていることを示す "1" が指定されている場合\_は、"0"

ドライバーの INF ファイルでは、 [**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**のレジストリ値を作成および設定できます。 たとえば、ドライバーによってデバイスのアイドル電力が有効になっているが、デバイスのインストール時に機能を無効にする必要がある場合、ドライバーの INF ファイルは**WdfDefaultIdleInWorkingState**を "0" に設定できます。

このフレームワークは、ドライバーが[**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッドを呼び出したときに*UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue**または**Wdfusedefault**に設定した場合にのみ、 **WdfDefaultIdleInWorkingState**レジストリ値を調べます。

このフレームワークは、ドライバーが[**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッドを呼び出したときに*UserControlOfWakeSettings*パラメーターを**IWakeAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue**または**Wdfusedefault**に設定した場合にのみ、 **WdfDefaultWakeFromSleepState**レジストリ値を調べます。

 

 





