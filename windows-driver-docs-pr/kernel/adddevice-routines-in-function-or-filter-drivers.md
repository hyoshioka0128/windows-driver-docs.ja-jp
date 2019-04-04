---
title: 関数またはフィルター ドライバーで AddDevice ルーチン
description: 関数またはフィルター ドライバーで AddDevice ルーチン
ms.assetid: 0a095c17-2295-46df-9908-f306f7fe9f67
keywords:
- 関数のドライバー WDK カーネル
- フィルター ドライバー WDK カーネル
- AddDevice ルーチンの WDK カーネル、関数のドライバー
- AddDevice ルーチンの WDK カーネル、フィルター ドライバー
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e81268fadb1224f7c747c621b5643bb3daba98a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536314"
---
# <a name="adddevice-routines-in-function-or-filter-drivers"></a>関数またはフィルター ドライバーで AddDevice ルーチン





[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)関数またはフィルター ドライバーのルーチンは、次の手順を実行する必要があります。

1.  呼び出す[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)機能を作成または追加されているデバイスのデバイス オブジェクト (FDO またはフィルター操作を実行) をフィルター処理します。

    指定しない、 *DeviceName*デバイス オブジェクトのため、そのため、PnP マネージャーのセキュリティをバイパスします。 ユーザー モード コンポーネントは、デバイスへのシンボリック リンクを必要とする場合は、デバイスを登録インターフェイス (次の手順を参照してください)。 カーネル モード コンポーネントは、レガシ デバイス名を必要とする場合は、ドライバーは、デバイス オブジェクトを名前する必要がありますが、名前付けは推奨されません。

    ファイルを含める\_デバイス\_SECURE\_で開いて、 *DeviceCharacteristics*パラメーター。 このような特性は、I/O マネージャーなどの関連するオープンと末尾の名前でファイルを開く、開いているすべての要求のデバイス オブジェクトに対するセキュリティ チェックを実行するよう指示します。

2.  \[省略可能な\]デバイスに 1 つまたは複数のシンボリック リンクを作成します。

    呼び出す[ **IoRegisterDeviceInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff549506)デバイスの機能を登録し、そのアプリケーションまたはシステムにシンボリック リンクを作成するコンポーネントが、デバイスを開くに使用できます。 呼び出して、インターフェイスを有効にする必要があります、ドライバー [ **IoSetDeviceInterfaceState** ](https://msdn.microsoft.com/library/windows/hardware/ff549700)処理すると、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 詳細については、[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)を参照してください。

3.  デバイスの拡張機能には、デバイスの PDO へのポインターを格納します。

    PnP マネージャーとして PDO へのポインターを提供する、 *PhysicalDeviceObject*パラメーターを*AddDevice*します。 ドライバーの PDO ポインターからルーチンの呼び出しでのなど使用[ **IoGetDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff549203)します。

4.  フラグで PnP デバイスの状態を追跡するために、デバイスの拡張機能など、デバイスは一時停止、削除すると定義突然削除します。

    たとえば、デバイスが一時停止状態の間に受信 Irp を保持することを示す 1 つのフラグを定義します。 ドライバーがまだない場合、メカニズム キュー Irp の Irp で保持するためのキューを作成します。 参照してください[キューおよびデキュー Irp](queuing-and-dequeuing-irps.md)詳細についてはします。

    割り当てることも、 **IO\_削除\_ロック**デバイス拡張機能と呼び出しで構造[ **IoInitializeRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549324)これを初期化するには構造体。 詳細については、[ロックを使用して削除](using-remove-locks.md)を参照してください。

5.  設定\_バッファーに格納された\_IO または\_直接\_I/O マネージャーで、デバイス スタックに送信される I/O 要求を使用するバッファーの種類を指定するデバイス オブジェクトの IO フラグ ビットです。 高度なドライバーまたはこのメンバーと同じ値をスタックでは、次の下位ドライバーとしてを除く可能性がある最上位レベルのドライバーです。 詳細については、[デバイス オブジェクトを初期化して](initializing-a-device-object.md)を参照してください。

6.  設定\_POWER\_突入または\_POWER\_電源管理、必要に応じてページング可能なフラグ。 ページング可能なドライバーをする必要があります設定\_POWER\_ページング可能なフラグ。 デバイス オブジェクトのフラグは、デバイスの PDO を作成するときに通常、バス ドライバーによって設定されます。 ただしより高度なドライバーは、これらのフラグでの値を変更する必要があります、 *AddDevice*ルーチン、FDO を作成または操作フィルターを適用したとき。 参照してください[電源管理のためのデバイス オブジェクトのフラグの設定](setting-device-object-flags-for-power-management.md)詳細についてはします。

7.  作成/イベント、スピン ロック、またはその他のオブジェクトなど、このデバイスを管理するドライバーを使用してその他のソフトウェア リソースを初期化します。 (への応答、I/O ポートなどのハードウェア リソースは、後で構成されている、 [ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求します)。

    *AddDevice* IRQL でシステム スレッド コンテキストで実行されるルーチン = パッシブ\_レベルでメモリが割り当てられた[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)使用初期化中にのみできますページ プールからの長さにドライバーがシステムのページング ファイルを保持するデバイスを制御しません。 このようなメモリの割り当てを解放する必要があります[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)する前に*AddDevice*コントロールを返します。

8.  デバイス オブジェクト、デバイス スタックをアタッチ ([**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300))。

    デバイスの PDO へのポインターを指定、*台*パラメーター。

    によって返されたポインターを格納**IoAttachDeviceToDeviceStack**します。 デバイスの次の下位のドライバーのデバイス オブジェクトを指すポインターが必要なパラメーターを[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336)と[ **PoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff559654)デバイス スタック Irp を渡すときにします。

9.  オフにします\_デバイス\_FDO またはフィルターの初期化フラグは、次のようなステートメントを使用しないでください。

    ```cpp
    FunctionalDeviceObject->Flags &= ~DO_DEVICE_INITIALIZING;
    ```

10. デバイスの PnP Irp の処理 (など[ **IRP\_MN\_クエリ\_リソース\_要件**](https://msdn.microsoft.com/library/windows/hardware/ff551715)と**IRP\_MN\_開始\_デバイス**)。

ドライバーを受信するまで、デバイスの制御を開始する必要がありますされません、 **IRP\_MN\_開始\_デバイス**PnP マネージャーによって、デバイスに割り当てられたハードウェア リソースの一覧を格納しています。

 

 




