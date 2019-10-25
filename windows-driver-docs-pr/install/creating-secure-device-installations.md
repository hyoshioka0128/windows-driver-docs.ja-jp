---
title: セキュリティで保護されたデバイスのインストールの作成
description: セキュリティで保護されたデバイスのインストールの作成
ms.assetid: e92488c4-1383-4493-b229-61c646546c82
keywords:
- デバイスのセットアップ WDK デバイスのインストール、セキュリティ
- デバイスのインストール WDK、セキュリティ
- デバイスのインストール WDK、セキュリティ
- セキュリティ WDK デバイスのインストール
- セキュリティ記述子の WDK デバイスのインストール
- INF ファイル WDK デバイスのインストール
- セキュリティ設定のテスト WDK デバイスのインストール
- レジストリ WDK デバイスのインストール
- WMI セキュリティ WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad84714187d0b0dce14f2c23f8b1243e317f10c2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828916"
---
# <a name="creating-secure-device-installations"></a>セキュリティで保護されたデバイスのインストールの作成





[ドライバーパッケージ](driver-packages.md)を作成するときは、デバイスのインストールが常に安全な方法で実行されるようにする必要があります。 セキュリティで保護されたデバイスのインストールとは、次のようなものです。

-   デバイスとそのデバイスインターフェイスクラスへのアクセスを制限します。

-   デバイス用に作成されたドライバーサービスへのアクセスを制限します。

-   ドライバーファイルの変更または削除を防止します。

-   デバイスのレジストリエントリへのアクセスを制限します。

-   デバイスの WMI クラスへのアクセスを制限します。

-   Setupapi.log 関数を正しく使用します

デバイスのインストールセキュリティは、*セキュリティ記述子*によって制御されます。 セキュリティ記述子を指定するためのプライマリメディアは INF ファイルです。 システムには既定のセキュリティ記述子が用意されており、ほとんどの場合、これらの記述子をオーバーライドする必要はありません。

### <a name="security-settings-for-devices-and-interfaces"></a>デバイスとインターフェイスのセキュリティ設定

システムによって提供されるすべての[デバイスセットアップクラス](https://docs.microsoft.com/previous-versions/ff553419(v=vs.85))の既定のセキュリティ記述子が提供されます。 一般に、これらの記述子により、システム管理者とユーザーの読み取り/書き込み/実行アクセスのフルアクセスが可能になります。 (デバイスへのアクセスを制御するセキュリティ記述子も、デバイスの[デバイスインターフェイスクラス](device-interface-classes.md)(存在する場合) へのアクセスを制御します。

WDM ドライバーの INF ファイルでは、システムの既定の設定を上書きするセキュリティ設定 (クラスごとまたはデバイスごと) を指定できます。 新しいデバイスセットアップクラスを作成するベンダーは、クラスのセキュリティ記述子を指定する必要があります。 一般に、デバイス固有のセキュリティ記述子を指定する必要はありません。 同じクラスに属するデバイスの種類によってユーザーの種類が大きく異なる場合は、デバイス固有のセキュリティ記述子を指定すると便利な場合があります。

WDM デバイスセットアップクラスに属するすべてのデバイスのセキュリティ記述子を指定するには、クラスインストーラーの INF ファイルの inf [**ClassInstall32 セクション**](inf-classinstall32-section.md)内で[**inf AddReg ディレクティブ**](inf-addreg-directive.md)を使用します。 **AddReg**ディレクティブは、 **(devicetype**および**Security**レジストリエントリの値を設定する*レジストリセクション*をポイントする必要があります。 これらのレジストリ値は、指定されたデバイスの種類のすべてのデバイスのセキュリティ記述子を指定します。

WDM デバイスセットアップクラスに属する1つのデバイスのセキュリティ記述子を指定するには、デバイスの INF ファイルの inf [**DDInstall. HW セクション**](inf-ddinstall-hw-section.md)内で[**inf AddReg ディレクティブ**](inf-addreg-directive.md)を使用します。 **AddReg**ディレクティブは、 **(devicetype**および**Security**レジストリエントリの値を設定する*レジストリセクション*をポイントする必要があります。 これらのレジストリ値は、関連する[**INF モデルセクション**](inf-models-section.md)で指定された[ハードウェア id](hardware-ids.md)または[互換性 id](compatible-ids.md)と一致するすべてのデバイスのセキュリティ記述子を指定します。

既定では、デバイスを表すデバイスオブジェクトを開く要求に対して、デバイスのセキュリティ記述子セットが適用されます (たとえば、NT デバイス名が*デバイス\\DeviceName\\* デバイスを開く要求など)。

ただし、既定では、デバイスのセキュリティ記述子セットはデバイスの名前空間内のオブジェクトを開く要求に適用されません。デバイスの名前空間には、デバイスの名前が *\\device\\DeviceName という形式のすべてのオブジェクトが含まれてい @no</3_ ObjectName*。 デバイスの名前空間内のオブジェクトに対して同じセキュリティ設定を適用するには、デバイスの FILE_DEVICE_SECURE_OPEN デバイスの特性フラグを設定します。 セキュリティで保護されたデバイスアクセスの詳細については、「[デバイスの名前空間へのアクセスの制御 (Windows ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/kernel/controlling-device-namespace-access)」を参照してください。 FILE_DEVICE_SECURE_OPEN デバイスの特性フラグを設定する方法の詳細については、「[デバイスの特性の指定 (Windows ドライバー)](https://docs.microsoft.com/windows-hardware/drivers/kernel/specifying-device-characteristics)」を参照してください。

PnP マネージャーは、ドライバーの[**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンを呼び出した後、デバイスオブジェクトのセキュリティ値を設定します。 一部の WDM ドライバーでは、 [**Iocreateデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure)を呼び出すことによって、物理デバイスオブジェクト (PDO) を作成するときに、デバイス固有のセキュリティ記述子を指定できます。 詳細については、「[デバイスオブジェクトのセキュリティ保護](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)」を参照してください。

### <a name="security-settings-for-driver-files"></a>ドライバーファイルのセキュリティ設定

[**INF CopyFiles ディレクティブ**](inf-copyfiles-directive.md)を使用してファイルをコピーする場合は、*ファイルリストセクション*を指定することができます。**セキュリティ**セクション。 このセクションでは、 **CopyFiles**ディレクティブによってコピーされるすべてのファイルのセキュリティ記述子を指定します。 ただし、インストール先が *% SystemRoot%* のシステムサブディレクトリの1つである場合、ベンダーはドライバーファイルのセキュリティ記述子を指定する必要はありません。 (これらのサブディレクトリの詳細については、「 [Dirids の使用](using-dirids.md)」を参照してください)。これらのサブディレクトリの既定のセキュリティ記述子がシステムによって提供され、既定の記述子をオーバーライドすることはできません。

### <a name="security-settings-for-driver-services"></a>ドライバーサービスのセキュリティ設定

ドライバーの INF ファイルの*service-install セクション*(「 [**Inf addservice ディレクティブ**](inf-addservice-directive.md)」を参照) では、**セキュリティ**エントリを含めることができます。 このエントリは、デバイスに関連付けられているドライバーサービスの開始、停止、構成などの操作を実行するために必要なアクセス許可を指定します。 ただし、システムはドライバーサービスの既定のセキュリティ記述子を提供します。この既定の記述子は通常、オーバーライドする必要はありません。

### <a name="security-settings-for-device-and-driver-registry-entries"></a>デバイスとドライバーのレジストリエントリのセキュリティ設定

Inf [**AddReg ディレクティブ**](inf-addreg-directive.md)を使用して inf ファイルでレジストリエントリを指定する場合は、*レジストリの追加セクション*を含めることができます。各*追加レジストリセクション*の**セキュリティ**セクション。 *レジストリの追加-セクション*。**Security**セクション: 関連する*レジストリセクション*セクションで作成された、作成されたレジストリエントリへのアクセス許可を指定します。 システムは、 **Hkr**相対ルートの下に作成されたすべてのレジストリエントリに対して、既定のセキュリティ記述子を提供します。 そのため、相対ルートの下にレジストリエントリを作成するときに、セキュリティ記述子を指定する必要はありません。

### <a name="security-settings-for-wmi-classes"></a>WMI クラスのセキュリティ設定

システムは、WMI クラスを識別する Guid に既定のセキュリティ記述子を割り当てます。 Windows XP 以前のバージョンのオペレーティングシステムでは、WMI Guid の既定のセキュリティ記述子により、すべてのユーザーにフルアクセスが許可されます。 Windows Server 2003 以降では、既定のセキュリティ記述子により、管理者のみがアクセスできるようになります。

ドライバーが WMI クラスを定義し、これらのクラスに対してシステムの既定のセキュリティ記述子を使用しない場合は、デバイスの INF ファイル内で[**Inf DDInstall. WMI セクション**](inf-ddinstall-wmi-section.md)を使用してセキュリティ記述子を指定できます。

### <a name="using-setupapi-functions-correctly"></a>Setupapi.log 関数を正しく使用する

[ドライバーパッケージ](driver-packages.md)に、setupapi.log 関数を呼び出すインストーラー、共同インストーラー、またはその他のインストールアプリケーションが含まれている場合は、 [setupapi.log を使用するためのガイドライン](guidelines-for-using-setupapi.md)に従う必要があります。

### <a href="" id="testing-installation-security-settings-"></a>インストールのセキュリティ設定をテストする

[Setupapi.log ログ](setupapi-logging--windows-server-2003--windows-xp--and-windows-2000-.md)を使用して、デバイスのインストールに関連付けられているセキュリティ設定が正しく指定されていることを確認します。 ログ記録レベルを verbose (0x0000FFFF) に設定してから、さまざまなインストールシナリオを試してください。

このようなシナリオには、ユーザーアカウントとシステム管理者アカウントの両方からの初期インストールと reinstallations の両方が含まれている必要があります。 ソフトウェアをインストールする前にデバイスに接続してみてください。また、その逆もできます。

インストールが成功した場合は、ログを表示して、エラーが発生していないことを確認します。 インストールが失敗した場合は、ログを確認してエラーの原因を特定します。

また、インストールが完了したら、次の操作を実行できます。

-   レジストリエントリに割り当てられているセキュリティ設定を表示するには、レジストリエディターを使用します。

-   **マイコンピューター**を使用して、ファイルに割り当てられているセキュリティ設定を表示します。

 

 





