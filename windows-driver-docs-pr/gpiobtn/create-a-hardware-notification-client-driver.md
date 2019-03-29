---
title: ハードウェア通知クライアント ドライバーの作成
description: ここでは、Microsoft によって提供される、KMDF クラスの拡張機能を利用したハードウェア通知クライアント ドライバーの開発のための一般的なガイダンスを示します。
ms.assetid: 348950d3-fb80-4800-a606-290d473aa412
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ef6f9d7653241245c1c462bb008cfc2a766bef36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581995"
---
# <a name="create-a-hardware-notification-client-driver"></a>ハードウェア通知クライアント ドライバーの作成


ここでは、Microsoft によって提供される、KMDF クラスの拡張機能を利用したハードウェア通知クライアント ドライバーの開発のための一般的なガイダンスを示します。

1.  Mshwnclxstub.lib にリンクし、ヘッダー hwn.h と hwnclx.h を含む、クライアント ドライバーの実装用のファイルを作成します。

2.  必要な KMDF とハードウェア notification クラスの拡張機能コールバック関数のインスタンスを定義します。 具体的には、実装し、次のコード例に示すように、これらのコールバック関数を登録する必要があります。

    ```cpp
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD HwnClientEvtDeviceAdd;
    HWN_CLIENT_INITIALIZE_DEVICE HwnClientInitializeDevice;
    HWN_CLIENT_UNINITIALIZE_DEVICE HwnClientUnInitializeDevice;
    HWN_CLIENT_QUERY_DEVICE_INFORMATION HwnClientQueryDeviceInformation;
    HWN_CLIENT_START_DEVICE HwnClientStartDevice;
    HWN_CLIENT_STOP_DEVICE HwnClientStopDevice;
    HWN_CLIENT_SET_STATE HwnClientSetState;
    HWN_CLIENT_GET_STATE HwnClientGetState;
    ```

3.  実装、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチンでは、クライアント ドライバーのエントリ ポイントと初期化を担当します。 ハードウェア通知クライアント ドライバーでは、この関数を次の処理する必要があります。

    -   呼び出す[ **WDF\_ドライバー\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff551302)ドライバーの初期化に[ **WDF\_ドライバー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551300)構造体。

    -   呼び出す[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)クライアント ドライバーのフレームワーク ドライバー オブジェクトを作成します。

    -   内容を定義する、 [ **HWN\_クライアント\_登録\_パケット**](https://msdn.microsoft.com/library/windows/hardware/mt843560)クラスの拡張機能で使用するためのコールバック関数のポインターを含むです。 必要なコールバック関数の詳細については、次を参照してください。[ハードウェア通知参照](https://msdn.microsoft.com/library/windows/hardware/dn789336)します。

    -   呼び出す[HwNRegisterClient](https://msdn.microsoft.com/library/windows/hardware/mt843550)クライアント ドライバーをクラス拡張を登録します。

4.  実装、 [ *EVT\_WDF\_ドライバー\_デバイス\_追加*](https://msdn.microsoft.com/library/windows/hardware/ff541693)デバイスの初期化の操作を実行する責任を負います関数PnP マネージャーは、デバイスの存在を報告するとします。 ハードウェア通知クライアント ドライバーでは、この関数を次の処理する必要があります。

    -   呼び出す[ **HwNProcessAddDevicePreDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/mt843549)デバイスをさまざまな状態に移行する、KMDF に必要なデバイスを準備する/リリースし、開始/終了コールバックを提供します。

    -   呼び出す[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926) framework デバイス オブジェクトを作成します。

    -   呼び出す[ **HwNProcessAddDevicePostDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/mt843548) I/O キューを作成します。

5.  定義された実装[ **HWN\_クライアント\_初期化\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/mt843553)ハードウェアの通知を準備するクラスの拡張機能によって呼び出される関数使用するためのコント ローラー。

6.  定義された実装[ **HWN\_クライアント\_非\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/mt827292)ハードウェアの初期化解除にクラスの拡張機能によって呼び出される関数通知コント ローラー。

7.  定義された実装[ **HWN\_クライアント\_クエリ\_デバイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/mt843554)関数、クラスの拡張機能によって呼び出されます。 この関数は、通知のハードウェア コンポーネントの属性を取得する責任を負います。

8.  定義された実装[ **HWN\_クライアント\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/mt843557)クラスの拡張機能によって呼び出される関数。 この関数は、ハードウェアの通知コント ローラーを起動するため、クライアント ドライバー用の ACPI リソースの割り当てを担当します。

9.  定義された実装[ **HWN\_クライアント\_停止\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/mt843558)クラスの拡張機能によって呼び出される関数。 この関数はハードウェア通知コント ローラーを停止して、クライアント ドライバーによって使用される ACPI リソースを解放します。

10. 定義された実装[ **HWN\_クライアント\_設定\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt843556)クラスの拡張機能によって呼び出されます。 この関数は、ハードウェア通知コンポーネントの状態を設定します。

11. 定義された実装[ **HWN\_クライアント\_取得\_状態**](https://msdn.microsoft.com/library/windows/hardware/mt843552)クラスの拡張機能によって呼び出されます。 この関数は、通知のハードウェア コンポーネントの現在の値を取得します。 入力バッファーが null の場合、つまり、ユーザーが特定のハードウェアの通知の状態を指定しなかった場合、この関数はすべてのハードウェア通知コンポーネントの状態情報を返します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[ハードウェア通知](hardware-notifications-support.md)

[ハードウェア通知リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn789336)



