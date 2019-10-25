---
title: KMDF ドライバーでのデバイス アクセスの制御
description: KMDF ドライバーでのデバイス アクセスの制御
ms.assetid: 62bbc69f-0754-4d37-a476-dd2ac3d70de6
keywords:
- デバイスアクセス制御 (WDK KMDF)
- WDK デバイスオブジェクトの名前
- デバイスオブジェクト WDK KMDF
- フレームワークオブジェクト WDK KMDF、デバイスアクセス制御
- セキュリティ記述子 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f69f7c9b294b7e66b39b67492ed3e3c5ecf2f347
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845623"
---
# <a name="controlling-device-access-in-kmdf-drivers"></a>KMDF ドライバーでのデバイス アクセスの制御


ユーザーがコンピューターのデバイスとファイルに不適切にアクセスするのを防ぐために、ドライバーを使用する必要があります。 デバイスとファイルへの不正アクセスを防ぐには、次のことを行う必要があります。

-   必要な場合にのみ、デバイスオブジェクトに名前を指定します。

-   デバイスオブジェクトとインターフェイスのセキュリティ記述子を指定します。

### <a href="" id="naming-device-objects-only-when-necessary"></a>必要な場合にのみデバイスオブジェクトに名前を付ける

ほとんどの Windows Driver Model (WDM) ドライバーと同様に、フレームワークベースのドライバーは通常、デバイスオブジェクトに名前を指定しません。 アプリケーションはデバイスオブジェクト名を指定することによってデバイスにアクセスできます。そのため、追加の各デバイスオブジェクト名は、アプリケーションがデバイスにアクセスするために使用できる追加のパスを表します。

デバイスへの不正アクセスを防ぐために、各ドライバーは、デバイスオブジェクトに名前を指定するときにセキュリティ記述子を指定できます。 ただし、オペレーティングシステムによってドライバーに提供されるファイル名 (「 [**Wdffileobjectgetfilename**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename)」を参照) には、アプリケーションが使用するデバイスオブジェクト名が含まれていません。 したがって、ドライバーのスタック内の複数のドライバーによってデバイスオブジェクトの名前が指定されている場合、そのデバイスを開くためにアプリケーションが使用したオブジェクト名をドライバーが判断できません。 その結果、アプリケーションは、使用しているドライバーよりも制限の緩いセキュリティ記述子を持つデバイスを開く可能性があります。

物理デバイスオブジェクト (PDOs) には名前が必要です。 通常、フレームワークによって (既定では)、名前を生成するようにオペレーティングシステムに指示するため、フレームワークベースのバスドライバーは PDO の名前を指定しません。

一方、フレームワークベースのドライバーは、 [**Wdfdeviceinitassign name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)を呼び出すことによってデバイスオブジェクトにデバイス名を割り当てることができます。 ドライバーは、特定のデバイス名を必要とする古いアプリケーションをドライバーがサポートしている必要がある場合、またはそのアーキテクチャに必要な古いドライバースタックにドライバーが属している場合にのみ、機能デバイスオブジェクト (FDO)、フィルターデバイスオブジェクト (フィルター処理)、または PDO に名前を指定する必要があります。オブジェクト名。

WDM ドライバーおよびフレームワークベースのドライバーは、FDOs に名前を付けたり、DOs をフィルター処理したりする代わりに、アプリケーションがアクセスできるデバイスインターフェイスを提供する必要があります。 オペレーティングシステムは、デバイスの PDO から、およびドライバーパッケージの INF ファイルによって指定されたレジストリエントリから、デバイスインターフェイスのセキュリティ記述子を取得します。 バスドライバーは、ドライバーのデバイスが raw モードで動作している場合に、関数ドライバーを使用せずに PDO のデバイスインターフェイスを提供できます。

一部のドライバーでは、 [**WdfDeviceCreateSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatesymboliclink)を呼び出して、デバイスのシンボリックリンク名を作成する必要があります。 たとえば、アプリケーションがデバイスの MS-DOS 名を確認する場合、ドライバーは[ms-dos デバイス名](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-ms-dos-device-names)を作成することがあります。 ドライバーによって名前のない FDO またはフィルターのシンボリックリンク名が作成された場合、フレームワークによって、シンボリックリンク名が PDO の名前に関連付けられます。 (コントロールデバイスは PDO に関連付けられていないため、名前のないコントロールデバイスのシンボリックリンク名をドライバーで作成することはできません)。

### <a href="" id="providing-security-descriptors-for-device-objects-and-interfaces"></a>デバイスオブジェクトとインターフェイスのセキュリティ記述子の提供

すべての名前付きデバイスオブジェクトには、セキュリティ記述子が必要です。 オペレーティングシステムは、デバイスオブジェクトのセキュリティ記述子を使用して、デバイスとそのデバイスインターフェイスにアクセスすることが許可されているユーザーの種類を決定します。 セキュリティ記述子は、次の方法でデバイスオブジェクトに割り当てることができます。

-   デバイスオブジェクトの既定のセキュリティ記述子を提供するオペレーティングシステム (「[デバイスアクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access)」を参照)。

-   既定のセキュリティ記述子を提供するフレームワーク。ドライバーが[**Wdfdeviceinitassign name**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignname)を呼び出してデバイスオブジェクトに名前を割り当てる場合 (sddl\_devobj\_SYS\_ALL\_ADM\_すべての値) を使用します (「sddl」を参照してください)。 [デバイスオブジェクトの場合](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects))。

-   ドライバー。 [**Wdfdeviceinit割り当て Sddlstring**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitassignsddlstring)を呼び出すことによって、フレームワークの既定のセキュリティ記述子をオーバーライドできます。

既定では、オペレーティングシステムは、デバイス PDO のセキュリティ記述子も使用して、ドライバーが提供するデバイスインターフェイスへのアクセス権を決定します。

ドライバーパッケージは、inf [**DDInstall. HW セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)内の[**inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を使用して、デバイスのセキュリティ記述子を指定する inf ファイルを提供できます。

INF ファイルでセキュリティ記述子を指定する方法の詳細については、「[セキュリティで保護されたデバイスのインストールの作成](https://docs.microsoft.com/windows-hardware/drivers/install/creating-secure-device-installations)」を参照してください。

ドライバーが raw モードで動作するデバイスに対して PDOs を作成する場合、ドライバーは[**Wdfpdoinit割り当て Rawdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfpdo/nf-wdfpdo-wdfpdoinitassignrawdevice)を呼び出すときに、[デバイスセットアップクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)を指定する必要があります。 また、ドライバーがコントロールデバイスを作成する場合は、 [**Wdfdeviceinitsetdeviceclass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetdeviceclass)を呼び出して、デバイスセットアップクラスを指定できます。 どちらの場合も、システム管理者は、指定されたセットアップクラスのレジストリキーを使用して、デバイスのセキュリティ記述子を格納できます。

デバイスで使用するセキュリティ記述子をオペレーティングシステムがどのように判断するかについては、「[デバイスアクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-access)」を参照してください。

フレームワークは、デバイスオブジェクトを作成するとき、常にファイル\_デバイス\_セキュリティで保護された\_OPEN フラグを設定します。これにより、オペレーティングシステムはデバイスのセキュリティ記述子を確認してから、アプリケーションがデバイス内の任意の名前にアクセスできるようになります。空間. ファイル\_デバイス\_セキュリティで保護された\_オープンフラグとデバイスの名前空間の詳細については、「[デバイスの名前空間へのアクセスの制御](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)」を参照してください。

 

 





