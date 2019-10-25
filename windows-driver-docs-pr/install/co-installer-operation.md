---
title: 共同インストーラー操作
description: 共同インストーラー操作
ms.assetid: a7f52125-b435-4963-85dc-712700ba9fe9
keywords:
- WDK デバイスのインストールとその動作の共同インストーラー
- 共同インストーラー WDK デバイスのインストール、例
- SetupDiCallClassInstaller
- クラス共同インストーラー WDK
- 差分 request 共同インストーラーの例 WDK
- デバイス固有の共同インストーラーの WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad7fba0e2ade733f3d696c08029150e8fe91e799
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840656"
---
# <a name="co-installer-operation"></a>共同インストーラー操作





共同インストーラーは、次の図に示すように、Setupapi.log によって呼び出されます。

![共同インストーラーがデバイスのインストールに参加するしくみを示す図](images/coinsts.png)

Unshaded ボックスは、システムによって提供される[デバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))用にオペレーティングシステムによって提供されるコンポーネントを表します。 網掛けされたボックスは、指定できるコンポーネントを表します。 カスタムデバイスセットアップクラスを作成する場合は、クラスインストーラーを指定することもできます。 ただし、ほとんどすべてのデバイスがシステムによって提供されるいずれかのデバイスセットアップクラスに関連付けられるため、新しいデバイスセットアップクラスを作成する必要はほとんどありません。 Windows コンポーネントの詳細については、「[デバイスのインストールの概要](overview-of-device-and-driver-installation.md)」を参照してください。

共同インストーラーは、特定のデバイス (*デバイス固有の共同インストーラー*) またはデバイスセットアップクラス (*クラス共同インストーラー*) 用に提供できます。 Setupapi.log は、共同インストーラーが登録されているデバイスをインストールするときにのみ、デバイス固有の共同インストーラーを呼び出します。 オペレーティングシステムとベンダーは、デバイスに対して、0個以上のデバイス固有の共同インストーラーを登録できます。 は、共同インストーラーが登録されているデバイスセットアップクラスのデバイスをインストールするときに、クラスの共同インストーラーを呼び出します。 オペレーティングシステムとベンダーは、デバイスセットアップクラスの1つまたは複数のクラスの共同インストーラーを登録できます。 また、クラスの共同インストーラーは、1つまたは複数のセットアップクラスに登録できます。

Windows および[カスタムデバイスインストールアプリケーション](writing-a-device-installation-application.md)では、[デバイスインストール関数コード](https://docs.microsoft.com/previous-versions/ff541307(v=vs.85))(差分コード) を使用して[**setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)を呼び出すことによって、デバイスをインストールします。

GUI モードセットアップ中に、オペレーティングシステムは差分コードを使用して[**Setupdicallclassinstaller**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicallclassinstaller)を呼び出し、システムに存在する非 PnP デバイスを検出します。 IHV は、通常、IHV がリリースする非 PnP デバイスに対してこのアクションを実行するための共同インストーラーを提供します。

差分の要求ごとに、 **Setupdicallclassinstaller**は、デバイスのセットアップクラスに登録されているすべてのクラスの共同インストーラー、特定のデバイスに登録されているデバイスの共同インストーラー、デバイスのシステムによって提供されるクラスインストーラーを呼び出します。セットアップクラス (存在する場合)。

カスタムデバイスインストールアプリケーションでは、共同インストーラーまたはクラスインストーラーを直接呼び出すのではなく、 **Setupdicallclassinstaller**を呼び出す必要があります。 この関数は、登録されているすべての共同インストーラーが適切に呼び出されることを保証します。

クラスの共同インストーラーは通常、デバイスのインストールの前に登録され、デバイス固有の共同インストーラーはデバイスのインストールの一部として登録されます。 このため、クラスの共同インストーラーは、通常、開発時に共同インストーラーの一覧に追加され、デバイスのインストール中にすべての差分要求に対して呼び出されます。

デバイスの[**DIF_REGISTER_COINSTALLERS**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-register-coinstallers)要求が完了した後 (または[**Setupdiregistercodeviceinstallers**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiregistercodeviceinstallers)が呼び出された後)、オペレーティングシステムによって、デバイス固有の共同インストーラーが共同インストーラーの一覧に追加されます。 デバイス固有の共同インストーラーは、次の差分要求には参加しません。

[**DIF_ALLOW_INSTALL**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-allow-install)

[**DIF_INSTALLDEVICEFILES**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevicefiles)

[**DIF_SELECTBESTCOMPATDRV**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-selectbestcompatdrv)

次の差分要求に応答できるのは、クラスの共同インストーラー (デバイス固有の共同インストーラーではない) だけです。

[**DIF_DETECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-detect)

[**DIF_FIRSTTIMESETUP**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-firsttimesetup)

[**DIF_NEWDEVICEWIZARD_PRESELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preselect)

[**DIF_NEWDEVICEWIZARD_SELECT**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-select)

[**DIF_NEWDEVICEWIZARD_PREANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-preanalyze)

[**DIF_NEWDEVICEWIZARD_POSTANALYZE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-newdevicewizard-postanalyze)

デバイスの共同インストーラーは、これらのコンテキストでは適切ではありません。特定のデバイスがまだ識別されていないか、インストールの初期段階であるか、デバイスの共同インストーラーがまだ登録されていないことが原因です。

次の図は、デバイス固有の共同インストーラーが登録された後に、 **Setupdicallclassinstaller**が共同インストーラーとクラスインストーラーを呼び出す順序を示しています。

![差分要求の処理と後処理用の共同インストーラーの呼び出しの図](images/callco.png)

前の図に示されている例では、このデバイスのセットアップクラスに2つのクラスの共同インストーラーが登録されており、デバイス固有の共同インストーラーが1つデバイスに登録されています。 次の手順は、前の図の丸で囲んだ数字に対応しています。

1.  **Setupdicallclassinstaller**は、最初のクラスの共同インストーラーを呼び出し、処理中のインストール要求 (この例では[**DIF_INSTALLDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/install/dif-installdevice)) を示す差分コードを指定します。 共同インストーラーには、インストール要求に参加するオプションがあります。 この例では、最初に登録されたクラスの共同インストーラーによって NO_ERROR が返されます。

2.  さらに、 **Setupdicallclassinstaller**は、追加の登録済みクラスの共同インストーラーを呼び出します。 この例では、2番目のクラスの共同インストーラーによって ERROR_DI_POSTPROCESSING_REQUIRED が返されます。これにより、後で後処理用に共同インストーラーを呼び出すように要求します。

3.  **Setupdicallclassinstaller**は、登録されているデバイス固有の共同インストーラーを呼び出します。

4.  登録されているすべての共同インストーラーが呼び出されると、 **Setupdicallclassinstaller**は、システムが提供するクラスインストーラーを呼び出します (デバイスのセットアップクラスがある場合)。 この例では、クラスインストーラーは ERROR_DI_DO_DEFAULT を返します。これは、クラスインストーラーの通常の戻り値です。

5.  **Setupdicallclassinstaller**は、インストール要求の既定のハンドラー (存在する場合) を呼び出します。 DIF_INSTALLDEVICE には、Setupapi.log の一部である[**Setupdiinstalldevice**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiinstalldevice)という既定のハンドラーがあります。

6.  **Setupdicallclassinstaller**は、後処理を要求したすべての共同インストーラーを呼び出します。 この例では、2番目のクラスの共同インストーラーが後処理を要求しました。

共同インストーラーの後処理は、ドライバーの[**Iocompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンに似ていますが、1つのエントリポイントで共同インストーラーが2回呼び出される点が異なります。 **Setupdicallclassinstaller**が後処理のために共同インストーラーを呼び出すと、*後処理*が**TRUE**に設定され、 *installresult*が*コンテキスト*パラメーターの適切な値に設定されます。 この例では、 *Context*です。既定のハンドラーが正常に実行されたため、 *Installresult*は NO_ERROR です。

後処理の場合、 **Setupdicallclassinstaller**は、逆の順序で共同インストーラーを呼び出します。 前の図のすべての共同インストーラーで ERROR_DI_POSTPROCESSING_REQUIRED が返された場合、 **Setupdicallclassinstaller**は最初に Device_Coinstaller_1 を呼び出し、次に Class_Coinstaller_2 を渡してから、Class_Coinstaller_ を呼び出します。1. クラスインストーラーは、後処理を要求しません。共同インストーラーのみを実行します。

前の共同インストーラーでインストール要求が失敗した場合でも、後処理を要求する共同インストーラーが呼び出されます。

 

 





