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
ms.openlocfilehash: dd391383a26d1bb5ff79264aa6785fc70fd497e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843107"
---
# <a name="user-control-of-device-idle-and-wake-behavior-in-umdf"></a>UMDF でのデバイスのアイドル動作とウェイク動作のユーザーによる制御


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

デバイスにアイドル状態の電源またはウェイクアップ機能がある場合は、ユーザーがこれらの機能を有効または無効にできるようにするかどうかを決定できます。

UMDF ベースのドライバーでは、 [**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッドを使用して、レジストリアクセスを持つユーザーがデバイスのアイドル状態の電源をオンまたはオフにできるかどうかを指定できます。

ドライバーは、 [**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッドを使用して、レジストリアクセスを持つユーザーがデバイスのウェイクアップ機能を有効または無効にできるかどうかを指定できます。

どちらの方法でも、ドライバーは機能を有効にしたり、機能を無効にしたり、ユーザーが機能を制御したりできるようにします。

-   ドライバーが**AssignS0IdleSettings**メソッドを呼び出すと、 *UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**に設定し、*有効*に設定することによって、デバイスのアイドル状態をユーザーが制御できるようになります。パラメーターを**Wdftrue**または**Wdfusedefault に設定**します。

-   ドライバーが**AssignSxWakeSettings**メソッドを呼び出すと、 *UserControlOfWakeSettings*パラメーターを**WakeAllowUserControl**に設定し、*有効*に設定することにより、デバイスの wake 機能をユーザーが制御できるようになります。パラメーターを**Wdftrue**または**Wdfusedefault に設定**します。

ユーザーがドライバーでアイドル状態とウェイク設定を変更できるようになった場合、フレームワークには、ユーザーがアイドルおよびウェイク機能を有効または無効にできるようにデバイスマネージャー表示されるプロパティシートページの形式でユーザーインターフェイスが用意されています。 (フレームワークによって、レジストリ値**IdleInWorkingState**と**WakeFromSleepState**が変更されます。 ドライバーとそのインストールファイルは、これらの値の読み取りや変更を行うことはできません)。

ユーザーがデバイスの設定を変更すると、必要に応じて、フレームワークによって、新しい設定と一致するようにデバイスの電源状態が更新されます。 たとえば、ユーザーがデバイスのアイドル状態になっているときに、デバイスがアイドル状態になっているときに、デバイスのアイドル状態になっている機能を無効にすると、フレームワークはそのデバイスを動作状態に戻します。

ユーザーがドライバーでアイドル設定とウェイク設定を変更できるようにすると、フレームワークは既定でこれらの設定を有効にします。 一部のドライバーの作成者は、設定を変更できるようにする前に、最初に設定を無効にすることができます。

したがって、バージョン1.9 以降のフレームワークでは、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**という2つのドライバーで定義可能なレジストリ値が提供されています。これらは、デバイスのデバイスパラメーターに格納されてい **\\WDF**サブキーは、デバイスの[ハードウェアキー](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)の下にあります。 値は、"0" を使用して、機能が無効になっていることを示す "0" と、機能が有効になっていることを示す "1" が指定されている場合\_は、"0"

ドライバーの INF ファイルでは、 [**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、 **WdfDefaultIdleInWorkingState**と**WdfDefaultWakeFromSleepState**のレジストリ値を作成および設定できます。 たとえば、ドライバーによってデバイスのアイドル電力が有効になっているが、デバイスのインストール時に機能を無効にする必要がある場合、ドライバーの INF ファイルは**WdfDefaultIdleInWorkingState**を "0" に設定できます。

このフレームワークは、ドライバーが*UserControlOfIdleSettings*パラメーターを**IdleAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue** **に設定した場合にのみ、WdfDefaultIdleInWorkingState レジストリ値を調べます。WdfUseDefault** (ドライバーが[**IWDFDevice2:: AssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)メソッドを呼び出す場合)。

このフレームワークは、ドライバーが*UserControlOfWakeSettings*パラメーターを**IWakeAllowUserControl**に設定し、 *Enabled*パラメーターを**wdftrue**に設定した場合にのみ、 **WdfDefaultWakeFromSleepState**レジストリ値を検査します。**Wdfusedefault** (ドライバーが[**IWDFDevice2:: AssignSxWakeSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assignsxwakesettings)メソッドを呼び出す場合)。

 

 





