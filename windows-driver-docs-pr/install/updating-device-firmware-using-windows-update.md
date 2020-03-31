---
title: Windows Update を使用したデバイス ファームウェアの更新
description: このトピックでは、Windows Update (WU) サービスを使用してデバイスのファームウェアを更新する方法について説明します。
ms.assetid: 778c5ab5-572f-43b9-8e9a-9dd608de17a9
ms.date: 08/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e9a680809c2c62e7f9fecd5a101eea915443bd8
ms.sourcegitcommit: 078e2dfac6c18f65ff923d1e55bff4a23e02a824
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80400472"
---
# <a name="updating-device-firmware-using-windows-update"></a>Windows Update を使用したデバイス ファームウェアの更新

このトピックでは、Windows Update (WU) サービスを使用して、リムーバブルデバイスまたはシャーシ内のデバイスのファームウェアを更新する方法について説明します。  システムファームウェアの更新の詳細については、「 [WINDOWS UEFI ファームウェア更新プラットフォーム](../bringup/windows-uefi-firmware-update-platform.md)」を参照してください。

これを行うには、ファームウェアペイロードを含む、デバイスドライバーとして実装されている更新機構を提供します。  デバイスでベンダーから提供されたドライバーを使用している場合は、既存の関数ドライバーにファームウェア更新ロジックとペイロードを追加するか、別のファームウェア更新ドライバーパッケージを提供するかを選択できます。  デバイスで Microsoft が提供するドライバーを使用している場合は、個別のファームウェア更新ドライバーパッケージを提供する必要があります。  どちらの場合も、ファームウェア更新ドライバーパッケージはユニバーサルである必要があります。  ユニバーサルドライバーの詳細については、「[ユニバーサル Windows ドライバーでのはじめに](../develop/getting-started-with-universal-drivers.md)」を参照してください。  ドライバーバイナリでは、 [Kmdf](../wdf/index.md)、 [UMDF 2](../wdf/getting-started-with-umdf-version-2.md) 、または[Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)を使用できます。 

WU はソフトウェアを実行できないため、ファームウェア更新ドライバーは、インストールのためにファームウェアをプラグアンドプレイ (PnP) に渡す必要があります。

## <a name="firmware-update-driver-actions"></a>ファームウェア更新ドライバーのアクション

通常、ファームウェア更新ドライバーは、次のような軽量なデバイスドライバーです。

* デバイスの起動時、またはドライバーの[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数では、次のようになります。

    1. デバイスが接続されているデバイスを特定します。
    2. ドライバーのファームウェアのバージョンが、デバイスハードウェアで現在フラッシュされているファームウェアのバージョンよりも新しいものであるかどうかを確認します。
    3. ファームウェアの更新が必要な場合は、イベントタイマーを設定して更新をスケジュールします。
    4. それ以外の場合は、ドライバーが再起動されるまで何も行いません。

* システムランタイム:

    1. 更新プログラムがキューに登録されている場合は、一連の条件が満たされるのを待ちます。
    2. 条件が満たされたら、デバイスでファームウェアの更新を実行します。

## <a name="firmware-update-driver-contents"></a>ファームウェア更新ドライバーの内容

通常、ファームウェア更新ドライバーパッケージには、次のものが含まれます。

* [ユニバーサルドライバー INF](using-a-universal-inf-file.md)
* ドライバー カタログ
* 関数ドライバー (.sys または .dll)
* ファームウェア更新ペイロードバイナリ

ファームウェア更新パッケージを個別のドライバー送信として送信します。

## <a name="adding-firmware-update-logic-to-a-vendor-supplied-driver"></a>ベンダー提供のドライバーにファームウェア更新ロジックを追加する

次の図に示すように、既存の関数ドライバーはファームウェアの更新メカニズムを実装できます。

![Windows Update を使用した既存の関数ドライバーを使用したファームウェアの更新の配布](images/single-devnode.png)

または、ファンクションドライバとファームウェア更新ドライバを個別に更新する場合は、ファームウェアの更新ドライバをインストールする2つ目のデバイスノードを作成します。  次の図は、1つのデバイスが2つの異なるデバイスノードを持つことができる方法を示しています。

![Windows Update を使用して別のデバイスノードを使用してファームウェアの更新を配布する](images/two-devnodes.png)

この場合、独立したターゲットにするには、関数とファームウェアのデバイスノードのハードウェア Id が異なる必要があります。

2つ目のデバイスノードを作成するには、いくつかの方法があります。  デバイスの種類によっては、USB などの1つの物理デバイス上で2番目のデバイスノードを公開する機能があります。  この機能を使用して、WU によってデバイスノード不要を作成し、ファームウェア更新ドライバーをインストールすることができます。  ただし、デバイスの種類によっては、1台の物理デバイスで複数のデバイスノードを列挙することはできません。

この場合は、 [Addcomponent](../install/inf-addcomponent-directive.md)ディレクティブを指定する拡張機能の INF を使用して、Windows Update の対象となる可能性のあるデバイスノードを作成し、そのノードにファームウェア更新ドライバーをインストールします。  INF ファイルの次のスニペットは、その方法を示しています。

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

上記の INF サンプルでは、`ComponentIDs = ComponentDeviceId` は、子デバイスのハードウェア ID が `SWC\ComponentDeviceId`であることを示しています。  この INF をインストールすると、次のデバイス階層が作成されます。

![親デバイス、プライマリデバイス、AddComponent デバイス](images/component-device-hierarchy.png)

将来のファームウェア更新の場合は、ファームウェアペイロードを含む INF ファイルとバイナリファイルを更新します。

## <a name="adding-firmware-update-logic-to-a-microsoft-supplied-driver"></a>Microsoft 提供のドライバーにファームウェア更新ロジックを追加する

Microsoft 提供のドライバーを使用するデバイスのファームウェアを更新するには、上記のように、2つ目のデバイスノードを作成する必要があります。

## <a name="best-practices"></a>ベスト プラクティス

* ファームウェア更新ドライバーの INF で[Dirid 13](using-dirids.md)を指定すると、PnP はドライバーパッケージ内のファイルを driverstore に残します。

    ```cpp
    [Firmware_AddReg]
    ; Store location of firmware payload
    HKR,,FirmwareFilename,,"%13%\firmware_payload.bin"
    ```

    PnP は、デバイスをインストールするときにこの場所を解決します。  ドライバーはこのレジストリキーを開いて、ペイロードの場所を特定できます。

* ファームウェア更新ドライバーでは、次の INF エントリを指定する必要があります。

    ```cpp
    Class=Firmware
    ClassGuid={f2e7dd72-6468-4e36-b6f1-6488f42c1b52}
    ```

* 別のデバイスノードを見つけるには、ファームウェアドライバーは、すべてのデバイスノードが一致しているかを列挙するのではなく、それ自体を基準にしてデバイスツリーをウォークする必要があります。  ユーザーはデバイスの複数のインスタンスに接続している可能性があり、ファームウェアドライバーは、関連付けられているデバイスのみを更新する必要があります。  通常、検索するデバイスノードは、ファームウェアドライバーがインストールされているデバイスノードの親または兄弟です。 たとえば、上の図で2つのデバイスノードがある場合、ファームウェア更新ドライバーは、関数ドライバーを検索する兄弟デバイスを探すことができます。  上の図では、ファームウェアドライバーが、通信する必要があるプライマリデバイスを見つけるために親デバイスを探すことができます。

* ドライバーは、システム上にあるデバイスの複数のインスタンスに対して堅牢である必要があります。複数の異なるファームウェアバージョンがある可能性もあります。  たとえば、デバイスの1つのインスタンスが複数回接続されて更新されている場合があります。新しいデバイスが接続されている場合は、いくつかのファームウェアバージョンが古いことがあります。  つまり、状態 (現在のバージョンなど) は、グローバルな場所ではなく、デバイスに対して保存する必要があります。

* ファームウェア (EXE または共同インストーラーなど) を更新するための既存のメソッドがある場合は、ほとんどの場合、UMDF ドライバー内で更新コードを再利用できます。
