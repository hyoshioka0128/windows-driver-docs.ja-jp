---
title: KMDF ドライバーでのデバイス アクセスの制御
description: KMDF ドライバーでのデバイス アクセスの制御
ms.assetid: 62bbc69f-0754-4d37-a476-dd2ac3d70de6
keywords:
- デバイスへのアクセス制御の WDK KMDF
- WDK のデバイス オブジェクトの名前
- デバイス オブジェクト WDK KMDF
- framework オブジェクト WDK KMDF、デバイスのアクセス制御
- セキュリティ記述子 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 837ddaddbdec442a48dac7cc7a71267d9603b317
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382876"
---
# <a name="controlling-device-access-in-kmdf-drivers"></a>KMDF ドライバーでのデバイス アクセスの制御


ドライバーは、コンピューターのデバイスやファイルを不適切にアクセスできないようにする必要があります。 デバイスとファイルを不正アクセスを防ぐため、次の操作をする必要があります。

-   必要な場合にのみ、デバイス オブジェクトの名前を付けます。

-   デバイス オブジェクトとインターフェイスのセキュリティ記述子を提供します。

### <a href="" id="naming-device-objects-only-when-necessary"></a> 必要な場合にのみ、デバイス オブジェクトの名前付け

ほとんどの Windows Driver Model (WDM) ドライバーのようなフレームワーク ベースのドライバー通常名前を指定しません、デバイス オブジェクト。 アプリケーションは、各追加のデバイス オブジェクトの名前は、アプリケーションがデバイスへのアクセスに使用できる追加のパスを表すため、デバイスのオブジェクト名を指定することで、デバイスにアクセスできます。

未承認のアクセスを防ぐため、デバイスに、デバイス オブジェクトは名前と、各ドライバーでのセキュリティ記述子を指定できます。 ただし、ファイル名をオペレーティング システム、ドライバーを提供します (を参照してください[ **WdfFileObjectGetFileName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)) アプリケーションを使用するデバイス オブジェクトの名前は含まれません。 そのため、ドライバーのスタックのいくつかのドライバーがそれらのデバイス オブジェクトの名前を指定する場合、ドライバーは、アプリケーションがデバイスを開くために使用するオブジェクト名を特定できません。 結果として、アプリケーションは、ドライバーが必要ですがより緩いセキュリティ記述子を使用してデバイスを開く可能性があります。

物理デバイス オブジェクト (Pdo) 名が必要です。 通常、フレームワークに基づくバス ドライバーは、(既定) フレームワークに指示オペレーティング システムの名前を生成するために、PDO の名前を指定しません。

その一方で、framework ベースのドライバー割り当てることができます、デバイス名デバイス オブジェクトを呼び出すことによって[ **WdfDeviceInitAssignName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)します。 ドライバーは、その場合にのみ、ドライバーは特定のデバイス名、または、ドライバーで以前のドライバー スタックにあるアーキテクチャが属している場合を必要とする古いアプリケーションをサポートする必要があります。 (FDO) の機能のデバイス オブジェクト、デバイス オブジェクトのフィルター (フィルター操作を行います)、または PDO 名前必要があります。オブジェクトの名前。

Fdo と DOs のフィルターの名前を付けではなく WDM ドライバーやフレームワーク ベースのドライバーは、アプリケーションにアクセスできるデバイスのインターフェイスを提供する必要があります。 オペレーティング システムは、デバイスの PDO およびドライバー パッケージの INF ファイルを指定するレジストリ エントリから、デバイス インターフェイスのセキュリティ記述子を取得します。 バス ドライバーは、ドライバーのデバイスが関数のドライバーがない、raw モードで動作している場合、PDO のデバイスのインターフェイスを提供できます。

一部のドライバーを呼び出す必要があります[ **WdfDeviceCreateSymbolicLink** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)デバイスのシンボリック リンクの名前を作成します。 たとえば、ドライバーを作成、 [MS-DOS デバイス名](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-ms-dos-device-names)場合アプリケーションは、MS-DOS デバイス名を参照してください。 ドライバーを作成する場合は、名前のない FDO またはフィルターにシンボリック リンクの名前は、フレームワークは、PDO の名前のシンボリック リンクの名前を関連付けます。 (デバイスの制御に関連付けられていない、PDO のためには、ドライバーは、デバイスの名前のないコントロールのシンボリック リンクの名前を作成できません。)

### <a href="" id="providing-security-descriptors-for-device-objects-and-interfaces"></a> デバイス オブジェクトとインターフェイスのセキュリティ記述子を提供します。

すべてのデバイスの名前付きオブジェクトには、セキュリティ記述子が必要です。 オペレーティング システムでは、デバイス オブジェクトのセキュリティ記述子を使用して、デバイスとそのデバイス インターフェイスへのアクセスを許可するユーザーの種類を決定します。 セキュリティ記述子でデバイス オブジェクトを割り当てることができます。

-   デバイス オブジェクトの既定のセキュリティ記述子を提供するオペレーティング システム (を参照してください[デバイスへのアクセスを制御する](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access))。

-   既定のセキュリティ記述子を提供すると、フレームワーク (SDDL を使用して\_DEVOBJ\_SYS\_すべて\_ADM\_すべての値) には、ドライバーを呼び出す場合[ **WdfDeviceInitAssignName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)デバイス オブジェクトに名前を割り当てる (を参照してください[デバイス オブジェクトの SDDL](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects))。

-   フレームワークの既定のセキュリティ記述子を呼び出すことによってオーバーライドできるドライバー [ **WdfDeviceInitAssignSDDLString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)します。

既定では、オペレーティング システムもドライバーを提供するデバイス インターフェイスへのアクセス権を確認するのにデバイス PDO のセキュリティ記述子を使用します。

ドライバー パッケージとデバイスのセキュリティ記述子を指定する INF ファイルを提供できます、 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)内、 [ **INF DDInstall.HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section).

INF ファイルでのセキュリティ記述子の指定に関する詳細については、次を参照してください。[セキュリティで保護されたデバイスのインストールを作成する](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)します。

かどうか、ドライバーは、raw モードで動作するデバイスの Pdo を作成するドライバーを指定する必要があります、[デバイス セットアップ クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)呼び出し時に[ **WdfPdoInitAssignRawDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)します。 さらに、ドライバーは、デバイスの制御を作成する場合は、呼び出すことができます[ **WdfDeviceInitSetDeviceClass** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)デバイス セットアップ クラスを指定します。 どちらのこのような場合、システム管理者は、デバイスのセキュリティ記述子を格納するのに、指定したセットアップ クラスのレジストリ キーを使用できます。

オペレーティング システムがデバイスを使用するセキュリティ記述子を決定する方法については、次を参照してください。[デバイスへのアクセスを制御する](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access)します。

常に、ファイルを設定、フレームワークは、デバイス オブジェクトを作成するとき\_デバイス\_SECURE\_オープン オペレーティング システムは、任意の名前にアクセスするアプリケーションを許可する前に、デバイスのセキュリティ記述子を確認するためのフラグデバイスの名前空間。 ファイルの詳細については\_デバイス\_SECURE\_フラグとデバイスの名前空間を開きを参照してください[デバイス Namespace のアクセスを制御する](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)します。

 

 





