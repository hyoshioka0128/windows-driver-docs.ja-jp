---
title: 関数のドライバーのデバイス オブジェクトの作成
description: 関数のドライバーのデバイス オブジェクトの作成
ms.assetid: 3b988f6d-c50e-412d-85cb-031746535ff4
keywords:
- PnP WDK KMDF、関数のドライバー
- プラグ アンド プレイ WDK KMDF、関数のドライバー
- 電源管理 WDK KMDF、関数のドライバー
- 機能ドライバー WDK KMDF
- WDK KMDF の機能のデバイス オブジェクト
- Fdo WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 821f0af74fe62250a0b1ac2bab94b102ad827ae1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552714"
---
# <a name="creating-device-objects-in-a-function-driver"></a>関数のドライバーのデバイス オブジェクトの作成


各[関数ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff546516)システム上に存在する、サポートされているデバイスの各フレームワーク デバイス オブジェクトを作成します。 関数のドライバーによっては、これらのデバイス オブジェクトが作成された、ため、機能のデバイス オブジェクト (Fdo) は呼び出されます。 各 FDO は function ドライバーのデバイスを表したものです。

関数ドライバー フレームワークのデバイス オブジェクトを作成する必要がありますたびに、フレームワーク、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数。 フレームワークは、システムでサポートされているデバイスのいずれかが存在するドライバーに通知するには、このコールバック関数を呼び出します。

ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数へのポインターを受け取る、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。 ドライバーのセットを呼び出すことができます[framework デバイス オブジェクトの初期化メソッド](https://msdn.microsoft.com/library/windows/hardware/dn265631#device-init-methods)、WDFDEVICE で情報を格納する\_INIT 構造体。 さらに、ドライバーの関数を呼び出すことができます[framework FDO 初期化メソッド](https://msdn.microsoft.com/library/windows/hardware/dn265631#fdo-init-methods)します。

Function ドライバー framework デバイス オブジェクトを作成すると、通常は、次の手順が含まれています。

-   PnP、パワー、および電源ポリシーのコールバック関数を登録しています。

    ほとんどの関数のドライバー呼び出し[ **WdfDeviceInitSetPnpPowerEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546135) PnP と電力のコールバック関数を登録します。 これらのコールバック関数の詳細については、[PnP をサポートしていると関数のドライバーでの電源管理](supporting-pnp-and-power-management-in-function-drivers.md)を参照してください。

    デバイスは、低電力アイドル状態をサポートしていますまたは、ウェイク アップ機能を備えて、場合、関数のドライバーもは[ **WdfDeviceInitSetPowerPolicyEventCallbacks** ](https://msdn.microsoft.com/library/windows/hardware/ff546774)電源ポリシーのコールバックを登録するには。関数。 これらのコールバック関数の詳細については、[電源ポリシー所有権](power-policy-ownership.md)を参照してください。

-   ドライバー固有のコールバック関数の関数を登録しています。

    一部の関数のドライバー呼び出し[ **WdfFdoInitSetEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff547268)場合、それらのデバイスで必要なシステムのハードウェア リソースを指定するときに参加する必要があります。 ハードウェア リソースの詳細については、[Framework ベースのドライバーのハードウェア リソース](hardware-resources-for-kmdf-drivers.md)を参照してください。

-   ファイルのイベントのコールバック関数を登録しています。

    ドライバーを呼び出す必要があります、ドライバーは、アプリケーションを開くか、デバイス上のファイルを閉じたときに応答する必要がある場合、 [ **WdfDeviceInitSetFileObjectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff546107) framework ファイル オブジェクトのコールバック関数を登録するには. 詳細については、[Framework ファイル オブジェクトを使用する](framework-file-objects.md)を参照してください。

-   I/O 要求の属性を設定します。

    ドライバーを呼び出すことができる場合、ドライバーはフレームワークのキュー オブジェクトからの I/O 要求を受信、 [ **WdfDeviceInitSetRequestAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff546786)フレームワークがデバイスを割り当てることのコンテキストのメモリを設定するには要求オブジェクト。 詳細については、[要求オブジェクトのコンテキストを使用して](using-request-object-context.md)を参照してください。

-   デバイスの特性を設定します。

    通常、関数ドライバーは、一部のデバイスの特性を指定する次のメソッドを呼び出します。

    -   [**WdfDeviceInitSetDeviceType**](https://msdn.microsoft.com/library/windows/hardware/ff546090)ドライバーがサポートするハードウェアの種類を識別します。
    -   [**WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)をドライバーがアプリケーションからの I/O 要求を処理する場合は、データのバッファーにアクセスするためのメソッドを識別します。
    -   [**WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)デバイスは読み取り専用またはリムーバブル メディアをサポートしているかどうかなど、デバイスの特性を設定します。
    -   [**WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)デバイスは、一度に 1 つのアプリケーションでの排他アクセスを必要とする場合、します。
    -   [**WdfDeviceInitSetPowerInrush**](https://msdn.microsoft.com/library/windows/hardware/ff546142)低電力状態からの作業 (D0) 状態に遷移するとき、デバイスに、突入電流が必要な場合、します。
    -   [**WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766)または[ **WdfDeviceInitSetPowerNotPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546147)システムは、ドライバーはページング可能なデータにアクセスする必要があるかどうかを示すために、スリープ状態と動作 (S0) 状態の遷移中です。
    -   [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)デバイス オブジェクトに名前を割り当てます。
    -   [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)セキュリティ記述子をデバイス オブジェクトに割り当てます。
    -   [**WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)デバイスのセットアップ クラスを識別します。
-   デバイスのプロパティを取得します。

    場合があります関数ドライバーでは、デバイスのバスのドライバーやその他の下位のドライバーが設定されているデバイスのプロパティに関する情報を取得する必要があります。 ドライバーを呼び出すことができます[ **WdfFdoInitQueryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff547254)または[ **WdfFdoInitAllocAndQueryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff547239)この情報を取得します。 Windows 8.1 以降を対象とする新しいドライバーが呼び出せる[ **WdfFdoInitQueryPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265613)と[ **WdfFdoInitAllocAndQueryPropertyEx** ](https://msdn.microsoft.com/library/windows/hardware/dn265612).

-   デバイスのレジストリ キーへのアクセス。

    関数のドライバーによっては、デバイスまたは別のドライバー、ユーザー、またはインストール パッケージが配置されている場合、レジストリのドライバーに関する情報を取得する必要があります。 ドライバーが呼び出せる[ **WdfFdoInitOpenRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff547249)デバイスまたはドライバーのレジストリ キーを開きます。 詳細については、[Framework ベースのドライバーのレジストリを使用して](https://msdn.microsoft.com/library/windows/hardware/ff545562)を参照してください。

-   動的な列挙を使用する既定の子リスト構成を作成します。

    かどうか、バスの機能のドライバーを記述して、ドライバーは、バスに接続されている子デバイスの動的な列挙を実行している場合、ドライバーを呼び出す必要があります[ **WdfFdoInitSetDefaultChildListConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff547258). 詳細については、[バス上のデバイスを列挙する](enumerating-the-devices-on-a-bus.md)を参照してください。

-   デバイス オブジェクトを作成します。

    デバイス オブジェクトを作成する最後の手順を呼び出すことです。 [ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。

 

 





