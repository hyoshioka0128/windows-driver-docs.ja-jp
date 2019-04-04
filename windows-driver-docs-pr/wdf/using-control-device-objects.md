---
title: 制御デバイス オブジェクトの使用
description: 制御デバイス オブジェクトの使用
ms.assetid: 6367954f-6916-46df-a5a0-e80f045b69e5
keywords:
- デバイス オブジェクト WDK KMDF を制御します。
- デバイス オブジェクト WDK KMDF
- フレームワークは、WDK KMDF、デバイスのコントロール オブジェクトをオブジェクトします。
- 従来のハードウェア デバイス WDK KMDF
- ソフトウェア専用の仮想デバイス WDK KMDF
- システム シャット ダウンの通知 WDK KMDF
- WDK KMDF シャット ダウンの通知
- WDK KMDF の通知
- WDK KMDF の名前
- WDK KMDF、デバイス オブジェクトを名前します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccdd70f979d6822baeb0acb643ec2022a77dc03c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574496"
---
# <a name="using-control-device-objects"></a>制御デバイス オブジェクトの使用


A*制御デバイス オブジェクト*プラグ アンド プレイ (PnP) や電源管理操作をサポートしないフレームワーク デバイス オブジェクトです。 ドライバーは、デバイス オブジェクトのコントロールを使用して、ソフトウェアのみの仮想デバイスを表すまたは*レガシ ハードウェア デバイス*(つまり、デバイスを提供しない PnP や電源管理機能)。

また通常コントロール デバイス オブジェクトを作成するドライバーでは、デバイス オブジェクトのシンボリック リンクを作成します。 アプリケーションは Microsoft Win32 などの API 要素にシンボリック リンクの名前を渡すことによって制御デバイス オブジェクトを I/O 要求を送信することができます[ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数。

フレームワークにコントロールのデバイス オブジェクトをアタッチできません、[デバイス スタック](wdm-concepts-for-kmdf-drivers.md#device-stacks)します。 そのため、アプリケーションは、コントロールのデバイス オブジェクトに、I/O 要求を送信するときに、I/O マネージャーは、オブジェクトを作成した、コントロール デバイスの代わりに、スタックの上部にあるドライバーをドライバーに直接要求を提供します。 (ただし、追加のドライバーを呼び出すことができます[ **IoAttachDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548294)コントロール デバイス オブジェクトの上のデバイス オブジェクトをアタッチします。 この場合、追加のドライバー最初に受け取ります I/O 要求。)

### <a name="uses-of-control-device-objects"></a>デバイス オブジェクトをコントロールの使用

デバイスの制御の 2 つの一般的な用途は次のとおりです。

1.  PnP デバイスの場合、ドライバーは、一連のアプリケーションを使用するためのカスタムの I/O 制御コードをサポートしている場合のフィルター ドライバー。

    アプリケーションが、ドライバー スタックの先頭に、カスタムの I/O 制御コードを送信しようとしています場合 (のシンボリック リンク名などを使用して、[デバイス インターフェイス](using-device-interfaces.md))、場合、ドライバー、フィルター ドライバーの上の I/O 要求が失敗するドライバー。カスタムの I/O 制御コードを認識できませんでした。 この問題を回避するには、フィルター ドライバーは、制御デバイス オブジェクトを作成できます。 アプリケーションでは、フィルター ドライバーに直接 I/O 制御コードを送信するのに制御デバイス オブジェクトのシンボリック リンクの名前を使用できます。

    (問題を回避するために、フィルター ドライバーのより良い方法は、バス ドライバーとして機能するので注意して[列挙](enumerating-the-devices-on-a-bus.md)raw モードで動作する子デバイス。 つまり、フィルター ドライバーがサポートする各デバイス ドライバーは、関数のドライバーを必要としないオブジェクト (PDO) の物理デバイスを作成できます。 ドライバー呼び出し[ **WdfPdoInitAssignRawDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548802)と[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)これらのデバイスとアプリケーションの各によって識別できますデバイス名カスタム I/O 制御コードを送信するとき。)

2.  PnP がサポートされていないデバイス用のドライバーです。

    このようなドライバーは、このようなデバイスのデバイス オブジェクトがデバイス スタックに存在していない、PnP 機能を提供しないためコントロール デバイス オブジェクトを使用する必要があります。 非 PnP デバイスのサポートの詳細については、[非 PnP ドライバーとカーネル モード ドライバー フレームワークを使用して](using-kernel-mode-driver-framework-with-non-pnp-drivers.md)を参照してください。

### <a name="creating-a-control-device-object"></a>コントロールのデバイス オブジェクトを作成します。

コントロールのデバイス オブジェクトを作成するには、ドライバーが必要です。

1.  呼び出す[ **WdfControlDeviceInitAllocate** ](https://msdn.microsoft.com/library/windows/hardware/ff545841)を取得する、 [ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)構造体。

2.  オブジェクトの初期化メソッドを呼び出し、WDFDEVICE を初期化するために、必要に応じて\_INIT 構造体。 ドライバーは、次の初期化メソッドのみを呼び出すことができます。
    -   [**WdfControlDeviceInitSetShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff545847)
    -   [**WdfDeviceInitAssignName**](https://msdn.microsoft.com/library/windows/hardware/ff546029)
    -   [**WdfDeviceInitAssignSDDLString**](https://msdn.microsoft.com/library/windows/hardware/ff546035)
    -   [**WdfDeviceInitAssignWdmIrpPreprocessCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546043)
    -   [**WdfDeviceInitSetCharacteristics**](https://msdn.microsoft.com/library/windows/hardware/ff546074)
    -   [**WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)
    -   [**WdfDeviceInitSetExclusive**](https://msdn.microsoft.com/library/windows/hardware/ff546097)
    -   [**WdfDeviceInitSetFileObjectConfig**](https://msdn.microsoft.com/library/windows/hardware/ff546107)
    -   [**WdfDeviceInitSetIoInCallerContextCallback**](https://msdn.microsoft.com/library/windows/hardware/ff546119)
    -   [**WdfDeviceInitSetIoType**](https://msdn.microsoft.com/library/windows/hardware/ff546128)
    -   [**WdfDeviceInitSetRequestAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff546786)

3.  呼び出す[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)、WDFDEVICE の内容を使用する\_framework デバイス オブジェクトを作成する構造体を初期化します。

4.  次の初期化の操作を行います。
    -   [既定の I/O キューを作成する](creating-i-o-queues.md)のいずれかが必要な場合は、デバイス。
    -   呼び出す[ **WdfDeviceConfigureRequestDispatching**](https://msdn.microsoft.com/library/windows/hardware/ff545920)必要な場合、します。
    -   呼び出す[ **WdfDeviceCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff545939)コントロール デバイスへのアクセスを使用するアプリケーションをシンボリック リンク名を作成します。

5.  呼び出す[ **WdfControlFinishInitializing**](https://msdn.microsoft.com/library/windows/hardware/ff545854)します。

### <a name="rules-for-using-control-device-objects"></a>デバイス オブジェクトをコントロールの使用に関する規則

デバイス オブジェクトにコントロールを作成するドライバーは、次の規則に従う必要があります。

-   ドライバーできません制御デバイス オブジェクトのハンドル メソッドに渡すフレームワークを[列挙子デバイス](enumerating-the-devices-on-a-bus.md)します。

-   ドライバーが制御デバイス オブジェクトのハンドルをサポートするフレームワーク メソッドに渡すことはできません[デバイス インターフェイス](using-device-interfaces.md)します。

-   フレームワークでは、キューをすることはできませんが、ドライバーが I/O キューを作成して、キューの要求ハンドラーの登録を[電源管理対象](using-power-managed-i-o-queues.md)します。

-   ドライバーを作成できます[ファイル オブジェクト](framework-file-objects.md)デバイス オブジェクトを制御します。

### <a name="naming-a-control-device-object"></a>コントロールのデバイス オブジェクトの名前を付ける

コントロールのすべてのデバイス オブジェクトを指定する必要があります。 通常、ドライバーを呼び出す[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)デバイス名を割り当てし、呼び出す[ **WdfDeviceCreateSymbolicLink** ](https://msdn.microsoft.com/library/windows/hardware/ff545939)オブジェクトへのアクセスを使用するアプリケーションをシンボリック リンク名を作成します。

ドライバーが要求されていない場合[ **WdfDeviceInitAssignName** ](https://msdn.microsoft.com/library/windows/hardware/ff546029)デバイス名を割り当てるには、フレームワークに自動的が生成されますが制御デバイスの名前をドライバーを呼び出すことはできません[ **WdfDeviceCreateSymbolicLink**](https://msdn.microsoft.com/library/windows/hardware/ff545939)します。

ドライバーを呼び出すことができます[ **WdfDeviceInitSetDeviceClass** ](https://msdn.microsoft.com/library/windows/hardware/ff546084)を指定する、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)制御デバイスです。 デバイス セットアップ クラスは、デバイス セットアップ クラスに属しているについて管理者が指定した情報を含むレジストリのセクションを識別します。 呼び出し元の詳細については[ **WdfDeviceInitSetDeviceClass**](https://msdn.microsoft.com/library/windows/hardware/ff546084)を参照してください[Framework ベースのドライバーでのデバイス アクセスの制御](controlling-device-access-in-kmdf-drivers.md)します。

### <a name="receiving-notification-of-system-shutdown"></a>システムのシャット ダウンの通知を受け取る

デバイス オブジェクトのコントロールをサポートしていない PnP ため、ドライバーは、デバイスの電源の状態が変更されたときに、ドライバーに通知するコールバック関数を登録できません。 ただし、ドライバーを呼び出すことができます[ **WdfControlDeviceInitSetShutdownNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff545847)を登録する、 [ *EvtDeviceShutdownNotification* ](https://msdn.microsoft.com/library/windows/hardware/ff540911)コールバック関数。 このコールバック関数は、システムがその能力が失われると、ドライバーを通知します。

### <a name="deleting-a-control-device-object"></a>コントロールのデバイス オブジェクトを削除します。

一部のドライバーは、次のように、ドライバーがアンロードする前に、コントロールのデバイス オブジェクトを削除する必要があります。

-   かどうか (これは PnP または電源の管理をサポートしない) デバイス オブジェクト、コントロールを作成するには、ドライバーとドライバーが最終的に呼び出す必要があります、ドライバーは、PnP、電源管理をサポートするデバイス オブジェクト フレームワークを作成することも場合、 [ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734) IRQL = パッシブ\_レベル コントロールのデバイス オブジェクトを削除します。

    ドライバーでは、両方の種類のデバイス オブジェクトを作成する場合、オペレーティング システムは、ドライバーの管理のデバイス オブジェクトが削除されるまでには、ドライバーをアンロードできません。

    ただし、フレームワークがその他のデバイス オブジェクトを削除した後、ドライバーはまでコントロール デバイス オブジェクトを削除しない必要があります。 フレームワークがその他のデバイス オブジェクトを削除する場合を判断するには、ドライバーが提供する必要があります[ *EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)それらのオブジェクトに対して機能します。

-   ドライバーがコントロール デバイス オブジェクトを作成しますが、オブジェクトを作成しません framework デバイスを PnP サポートし、電源管理、ドライバーがコントロールのデバイス オブジェクトを削除します。

    ドライバーの後に、フレームワークがコントロールのデバイス オブジェクトを削除するこの場合、 [ *EvtDriverUnload* ](https://msdn.microsoft.com/library/windows/hardware/ff541694)コールバック関数を返します。

 

 





