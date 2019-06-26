---
title: 共同インストーラーの操作
description: 共同インストーラーの操作
ms.assetid: a7f52125-b435-4963-85dc-712700ba9fe9
keywords:
- 共同インストーラー WDK デバイス インストールでは、そのしくみ
- 共同インストーラー WDK デバイス インストールの例
- SetupDiCallClassInstaller
- 共同インストーラー WDK クラスします。
- 差分要求共同インストーラー例 WDK
- デバイスに固有の共同インストーラー WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f36cc41ac0c8b30ab0b28e85434b1457a06c7c06
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375330"
---
# <a name="co-installer-operation"></a>共同インストーラーの操作





共同インストーラーは、次の図に示すように、SetupAPI、によって呼び出されます。

![デバイスのインストールでの共同インストーラーの参加方法を示す図](images/coinsts.png)

影なしのボックスでのオペレーティング システムを提供するコンポーネントを表し、[システム提供のデバイス セットアップ クラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))します。 影付きのボックスは、提供できるコンポーネントを表します。 カスタムのデバイス セットアップ クラスを作成する場合は、クラスのインストーラーも指定できます。 ただし、ほとんどの場合必要、新しいデバイス セットアップ クラスを作成するため、ほぼすべてのデバイス、システム提供のデバイス セットアップ クラスのいずれかと関連付けることができます。 Windows コンポーネントの詳細については、次を参照してください。[デバイス インストールの概要](overview-of-device-and-driver-installation.md)します。

特定のデバイスの共同インストーラーを指定することができます (*デバイスに固有の共同インストーラー*) またはデバイス セットアップ クラス (*クラス共同インストーラー*)。 共同インストーラーで登録されたデバイスをインストールする場合のみ、SetupAPI はデバイスに固有の共同インストーラーを呼び出します。 オペレーティング システムおよびベンダーは、デバイスの 0 個以上のデバイス固有共同インストーラーを登録できます。 SetupAPI は、共同インストーラーで登録されたデバイス セットアップ クラスの任意のデバイスをインストールするときに、クラスの共同インストーラーを呼び出します。 オペレーティング システムおよびベンダーは、デバイス セットアップ クラスの 1 つまたは複数のクラス共同インストーラーを登録できます。 さらに、クラスの共同インストーラーは、1 つまたは複数のセットアップ クラスを登録できます。

Windows と[カスタム デバイスのインストール アプリケーション](writing-a-device-installation-application.md)デバイスを呼び出すことによってインストール[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)で[デバイスのインストールコードを関数](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))(差分コード)。

フル インストール モードのセットアップ中に、オペレーティング システムを呼び出す[ **SetupDiCallClassInstaller** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller) DIF コード、システムに存在する非 PnP デバイスを検出するとします。 IHV は通常、IHV を解放する非 PnP デバイスに対してこの操作を実行する共同インストーラーを提供します。

差分の要求ごとに、 **SetupDiCallClassInstaller**呼び出し、デバイスのセットアップ クラス、特定のデバイスの登録、デバイスの共同インストーラーおよびによって提供されるクラスのインストーラー クラスの co-installer が登録されている、システム、デバイスのセットアップのクラスのいずれかを使用する必要がある場合です。

カスタムのデバイスのインストール アプリケーションを呼び出す必要があります**SetupDiCallClassInstaller**共同インストーラーまたはクラスのインストーラーを直接呼び出すのではなく。 この関数により、登録されているすべての共同インストーラーが適切と呼ばれます。

クラスの共同インストーラーは通常、デバイスのインストール前に登録し、デバイスに固有の共同インストーラーは、デバイスのインストールの一部として登録されます。 Co-installer をクラスでは、したがって通常リストに追加されます、共同インストーラーが最初に構築されるときされ、デバイスのインストール中に差分のすべての要求の呼び出されます。

オペレーティング システムでは、デバイスに固有の共同インストーラーを後に共同インストーラー リストに追加、 [ **DIF_REGISTER_COINSTALLERS** ](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers)デバイスの要求が完了した (または[ **SetupDiRegisterCoDeviceInstallers** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)が呼び出されました)。 デバイスに固有の共同インストーラーは、次の差分要求に参加していません。

[**DIF_ALLOW_INSTALL**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-allow-install)

[**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)

[**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)

クラス共同インストーラーのみ (、デバイス固有共同インストーラーではなく) は、次の差分要求に応答できます。

[**DIF_DETECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-detect)

[**DIF_FIRSTTIMESETUP**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-firsttimesetup)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preselect)

[**DIF_NEWDEVICEWIZARD_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-select)

[**DIF_NEWDEVICEWIZARD_PREANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preanalyze)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-postanalyze)

これらのコンテキストで適切なデバイスの共同インストーラーは、いずれかの特定のデバイスが識別されていないため、またはインストール、またはデバイスの共同インストーラーの早い段階でまだ登録されていません。

次の図は、これで順序を示します**SetupDiCallClassInstaller**デバイスに固有の co-installer が登録した後は共同インストーラーとクラスのインストーラーを呼び出します。

![差分の co-installer を呼び出すことの図の要求を処理し、処理後](images/callco.png)

例では、上記の図に示すようにでは、このデバイスのセットアップ クラスの 2 つのクラスの共同インストーラーが登録されているし、1 つのデバイスに固有の共同インストーラーは、デバイスの登録します。 次の手順は、前の図の丸の番号に対応しています。

1.  **SetupDiCallClassInstaller**処理されているインストールの要求を示す差分コードを指定する、ファースト クラスの共同インストーラーを呼び出します ([**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)、この例では)。 共同インストーラーには、インストールの要求に参加しているのオプションがあります。 この例では、最初の登録済みのクラスの共同インストーラーは NO_ERROR を返します。

2.  **SetupDiCallClassInstaller**、追加の登録済みクラスの co-installer を呼び出します。 この例では、2 番目のクラスの共同インストーラーは、ERROR_DI_POSTPROCESSING_REQUIRED 共同インストーラーが、処理後の後で呼び出されることを要求を返します。

3.  **SetupDiCallClassInstaller** co-installer を特定のデバイスが登録されているいずれかの呼び出し。

4.  登録されているすべての共同インストーラーが呼び出された**SetupDiCallClassInstaller**デバイスのセットアップ クラスに 1 つを使用する必要がある場合、システムが指定したクラスのインストーラーを呼び出します。 この例では、クラスのインストーラーは、クラスのインストーラーの一般的な戻り値である ERROR_DI_DO_DEFAULT で返します。

5.  **SetupDiCallClassInstaller**いずれかを使用する必要がある場合、インストール要求は、既定のハンドラーを呼び出します。 DIF_INSTALLDEVICE が既定のハンドラーで[ **SetupDiInstallDevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)SetupAPI の一部です。

6.  **SetupDiCallClassInstaller**その要求の処理後に、共同インストーラーを呼び出します。 この例では、2 番目のクラスの共同インストーラーは、処理後を要求します。

処理後の共同インストーラーがドライバーに似ています。 [ **IoCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチン、共同インストーラーは、1 つのエントリ ポイントで、2 回目と呼ばれる点が異なります。 ときに**SetupDiCallClassInstaller**設定処理後の共同インストーラーを呼び出して、*後処理*に**TRUE**と*InstallResult*の適切な値に、*コンテキスト*パラメーター。 この例で*コンテキスト*.*InstallResult* NO_ERROR は、既定のハンドラーが正常に実行されるためです。

処理後の**SetupDiCallClassInstaller** co-installer を逆の順序で呼び出します。 ERROR_DI_POSTPROCESSING_REQUIRED、前の図のすべての共同インストーラーを返した場合**SetupDiCallClassInstaller** 、処理後の最初 Device_Coinstaller_1 を呼び出すと、Class_Coinstaller_2 続くとClass_Coinstaller_1 します。 クラスのインストーラーは後処理; を要求しません。共同インストーラーのみの操作を行います。

前の共同インストーラーには、インストールの要求が失敗した場合でも、処理後の要求を共同インストーラーが呼び出されます。

 

 





