---
title: Windows Update を使用したデバイス ファームウェアの更新
description: このトピックでは、Windows の更新 (WU) サービスを使用して、デバイスのファームウェアを更新する方法について説明します。
ms.assetid: 778c5ab5-572f-43b9-8e9a-9dd608de17a9
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: c620882d02e54124c187ac5aae690be6067929d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384785"
---
# <a name="updating-device-firmware-using-windows-update"></a>Windows Update を使用したデバイス ファームウェアの更新

このトピックでは、Windows の更新 (WU) サービスを使用してシャーシ内、またはリムーバブル デバイスのファームウェアを更新する方法について説明します。  システム ファームウェアの更新方法の詳細については、次を参照してください。 [Windows の UEFI ファームウェアを更新するプラットフォーム](../bringup/windows-uefi-firmware-update-platform.md)します。

これを行うには、デバイス ドライバー、ファームウェアのペイロードを含むとして実装されている更新メカニズムを提供します。  デバイス ベンダーから提供されたドライバーを使用する場合は、ファームウェアの更新ロジックとペイロードを関数の既存のドライバーに追加するか、別のファームウェア更新プログラムのドライバー パッケージを提供するオプションがあります。  デバイスは、Microsoft 提供のドライバーを使用している場合は、個別のファームウェア更新プログラムのドライバー パッケージを提供する必要があります。  どちらの場合も、ファームウェアの更新プログラムのドライバー パッケージは universal 必要があります。  ユニバーサル ドライバーに関する詳細については、次を参照してください。[ユニバーサル Windows ドライバーの概要](../develop/getting-started-with-universal-drivers.md)します。  バイナリのドライバーを使用して[KMDF](../wdf/index.md)、 [UMDF 2](../wdf/getting-started-with-umdf-version-2.md)または[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)します。 

ドライバーがファームウェアの更新は WU には、ソフトウェアを実行できません、ため、プラグ アンド プレイ (PnP) のインストールにファームウェアを配信する必要があります。

## <a name="firmware-update-driver-actions"></a>ファームウェア更新ドライバー アクション

通常、ファームウェア ドライバーの更新では、軽量のデバイス ドライバーには、次です。

* デバイスの開始時またはドライバーの[ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

    1. アタッチされているデバイスを識別します。
    2. ドライバーがデバイスのバージョンより新しいファームウェアのバージョンを持っているかどうかを決定します。
    3. ファームウェアの更新が必要な場合は、更新プログラムをスケジュールする、イベント タイマーを設定します。
    4. それ以外の場合、ドライバーがもう一度開始されるまで、何も作成を行いません。

* システム時に。

    1. 更新プログラムがキューに置かれた場合、一連の条件が満たされるまで待ちます。
    2. 条件が満たされたときに、デバイスのファームウェアの更新プログラムを実行します。

## <a name="firmware-update-driver-contents"></a>ファームウェア更新のドライバー コンテンツ

通常、ファームウェアの更新プログラムのドライバー パッケージは、次があります。

* [ユニバーサル ドライバーの INF](using-a-universal-inf-file.md)
* ドライバー カタログ
* 関数のドライバー (.sys または .dll)
* ファームウェア更新プログラム バイナリのペイロード

個別のドライバーの送信としては、ファームウェア更新プログラム パッケージを送信します。

## <a name="adding-firmware-update-logic-to-a-vendor-supplied-driver"></a>ベンダーから提供されたドライバーにファームウェアの更新ロジックを追加します。

関数の既存のドライバーは、次の図に示すように、ファームウェアの更新メカニズムを実装できます。

![Windows の更新を使用して、関数の既存のドライバーを経由してファームウェア更新を配布するには](images/single-devnode.png)

または、関数のドライバーとファームウェアのドライバーの更新を個別に更新する場合は、ファームウェア ドライバーの更新をインストールする 2 番目のデバイス ノードを作成します。  次の図は、1 つのデバイスは別のデバイスの 2 つのノードを保持できます。

![Windows の更新を使用して、別のデバイス ノードを使用してファームウェア更新を配布するには](images/two-devnodes.png)

この場合、関数およびファームウェア デバイス ノードでは、個別に対象にするために別のハードウェア Id が必要です。

2 つ目のデバイス ノードを作成するいくつかの方法はあります。  特定のデバイスの種類には、USB などの 1 つの物理デバイスで 2 番目のデバイス ノードを公開する機能があります。  この機能を使用して、WU をターゲット設定可能なデバイス ノードを作成でき、ファームウェアの更新ドライバーをインストールできます。  ただし、多数のデバイスの種類には複数のデバイス ノードを列挙するために 1 つの物理デバイスはできません。

ここでは、拡張機能を指定する INF を使用して、 [AddComponent](../install/inf-addcomponent-directive.md) Windows Update によってターゲットとなるし、ドライバーのファームウェア更新をインストールするデバイス ノードを作成するディレクティブ。  INF ファイルから次のスニペットは、これを実行する方法を示しています。

```cpp
[Manufacturer]
%Contoso%=Standard,NTamd64
[Standard.NTamd64]
%DeviceName%=Device_Install, PCI\DEVICE_ID
[Device_Install.Components]
AddComponent=ComponentName,,AddComponentSection
[AddComponentSection]
ComponentIDs = ComponentDeviceId
```

上記の INF サンプルでは、`ComponentIDs = ComponentDeviceId`子デバイスがハードウェア ID を持つことを示します`SWC\ComponentDeviceId`します。  インストールすると、この INF は、次のデバイスの階層を作成します。

![親デバイス、プライマリ デバイス、AddComponent デバイス](images/component-device-hierarchy.png)

将来のファームウェアの更新プログラム、INF、ファームウェアのペイロードを格納しているバイナリ ファイルを更新します。

## <a name="adding-firmware-update-logic-to-a-microsoft-supplied-driver"></a>Microsoft 提供のドライバーにファームウェアの更新ロジックを追加します。

Microsoft 提供のドライバーを使用するデバイスのファームウェアを更新するには、必要があります、2 つ目のデバイス ノードを作成する上記のようです。

## <a name="best-practices"></a>ベスト プラクティス

* ファームウェアの更新ドライバーの INF で、指定[DIRID 13](using-dirids.md) PnP、DriverStore 内のドライバー パッケージ内のファイルのままにします。

    ```cpp
    [Firmware_AddReg]
    ; Store location of firmware payload
    HKR,,FirmwareFilename,,"%13%\firmware_payload.bin"
    ```

    PnP に解決、デバイスをインストールするときのこの場所をします。  ドライバーは、ペイロードの場所を特定するには、このレジストリ キーを開きます。

* ファームウェア ドライバーを更新するには、次の INF エントリを指定する必要があります。

    ```cpp
    Class=Firmware
    ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
    ```

* 別のデバイス ノードを見つけるには、ファームウェア ドライバーが、一致のデバイスのすべてのノードの列挙ではなく自体を基準とした、デバイス ツリーを説明する必要があります。  ユーザー、デバイスの複数のインスタンスに接続しているし、ファームウェア ドライバーが関連付けられているデバイスのみを更新する必要があります。  通常、検索するデバイス ノードは、親またはファームウェア ドライバーがインストールされているデバイス ノードの兄弟です。 たとえば、上記 2 つのデバイス ノードの図、ファームウェア ドライバーの更新が関数ドライバーを検索する兄弟デバイスを探すことができます。  すぐに上記の図では、ファームウェア ドライバーが通信するために必要ながプライマリ デバイスを検索する親デバイスを検索できます。

* ドライバーは、デバイスが、場合によっては複数の異なるファームウェア バージョンで、システム上の複数のインスタンスに堅牢な必要があります。  たとえば、ある可能性があります接続および数回; 更新されたデバイスの 1 つのインスタンスこれは、古いファームウェア バージョンがいくつかの新しいデバイスを接続し、可能性があります。  つまり、(現在のバージョン) などの状態は、グローバルの場所ではないと、デバイスに対してで格納する必要があります。

* (EXE または例では、共同インストーラー) ファームウェアを更新する既存のメソッドがある場合ほとんど UMDF ドライバー内で更新プログラムのコードを再利用することができます。
