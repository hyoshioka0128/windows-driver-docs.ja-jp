---
title: 無線管理のサポート
description: ユーザーが Windows 8 のラップトップ、ノートブック、またはタブレットで [PC 設定] の [ワイヤレス] オプションを選択すると、接続されているワイヤレスデバイスのオンとオフを切り替えることができます。
ms.assetid: AA7AB429-30C5-4C10-AA85-41ED9EAEE69A
keywords:
- ラジオ管理 API
- radio management API、例
- 無線管理、例
- GPS ラジオの管理
- ラジオ管理、GPS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69304e9e86afc1cf3dfc62a69866d127ef4f0338
ms.sourcegitcommit: 5273e44c5c6c1c87952d74e95e5473c32a916d10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84122689"
---
# <a name="supporting-radio-management"></a>無線管理のサポート

> [!IMPORTANT]
> Windows 8.1 のこのドキュメントと位置情報ドライバーのサンプルは、非推奨とされました。

ユーザーが Windows 8 のラップトップ、ノートブック、またはタブレットで [PC 設定] の [ワイヤレス] オプションを選択すると、接続されているワイヤレスデバイスのオンとオフを切り替えることができます。 これらのワイヤレスデバイスには、Wi-fi アンテナまたは GPS デバイスを含めることができます。 PC 設定と特定のワイヤレスデバイスとの内部リンケージは、[ラジオ管理 API](https://docs.microsoft.com/previous-versions/windows/hardware/radio/hh406615(v=vs.85))と、特定のデバイスの対応するラジオ管理 DLL です。

Radio Management API は、Windows Driver Kit の一部として出荷される COM/Win32 インターフェイスのセットです。 これらのインターフェイスには、次のようなメソッドが含まれます。

- ラジオデバイスの現在の状態を取得します。

- ラジオデバイスの通知イベントをサポートする

- デバイスのプロパティ (フレンドリ名など) の取得

これらのインターフェイスは、アプリケーション開発者ではなく、Oem および Ihv 向けにのみ用意されています。

## <a name="the-radio-management-dynamic-link-library-dll"></a>オプション管理のダイナミックリンクライブラリ (DLL)

GPS など、ラジオデバイス用のデバイスドライバーを作成する場合、ドライバーには、ラジオ管理 API のインターフェイスをサポートする追加のダイナミックリンクライブラリ (DLL) を含める必要があります。 この DLL の要件を理解するために、Microsoft は、地理位置情報ドライバーのサンプルの一部として、サンプル Microsoft Visual Studio プロジェクトとソースコードを提供しています。 このサンプルプロジェクト SampleRM は、ドライバーサンプルのセンサー位置情報ドライバーのサンプル \\ C++ \\ RadioManagerGPS フォルダーにあります。 これには、7つの C++ ソースファイル、6つの C++ ヘッダーファイル、モジュール定義ファイル、リソースファイル、2つの IDL ファイル、(DLL を登録するための) レジストリファイル、およびインストールスクリプトが含まれます。

次の表に、ラジオ管理 API のメソッドと、サンプル DLL に含まれる対応するメソッドの一覧を示します。

|                                                     |                                                       |
|-----------------------------------------------------|-------------------------------------------------------|
| Radio Manager API                                   | Radio Manager DLL                                     |
| ImediarGetRadioInstances Omanager::               | CSampleRadioManager::GetRadioInstances                |
| ImediarOnSystemRadioStateChange Omanager::        | CSampleRadioManager::OnSystemRadioStateChange         |
| IRadioInstance:: GetFriendlyName                     | CSampleRadioInstance:: GetFriendlyName                 |
| IRadioInstance::GetInstanceSignature                | CSampleRadioInstance::GetInstanceSignature            |
| IRadioInstance::GetRadioManagerSignature            | CSampleRadioInstance::GetRadioManagerSignature        |
| IRadioInstance::GetRadioState                       | CSampleRadioInstance::GetRadioState                   |
| IRadioState::IsAssociatingDevice                    | CSampleRadioInstance::IsAssociatingDevice             |
| IRadioState::IsMultiComm                            | CSampleRadioInstance::IsMultiComm                     |
| IRadioState::SetRadioState                          | CSampleRadioInstance::SetRadioState                   |
| IRadioInstanceCollection:: GetAt                     | CRadioInstanceCollection:: GetAt                       |
| IRadioInstanceCollection:: GetCount                  | CRadioInstanceCollection:: GetCount                    |
| IMediaRadioManagerNotifySink:: OnInstanceAdd         | CSampleRadioManager:: \_ 焼討 eventoninstanceadd         |
| IMediaRadioManagerNotifySink::OnInstanceRadioChange | CSampleRadioManager:: \_ FireEventOnInstanceRadioChange |
| IMediaRadioManagerNotifySink::OnInstanceRemove      | CSampleRadioManager:: \_ FireEventOnInstanceRemove      |

## <a name="communicating-with-the-device-driver"></a>デバイスドライバーとの通信

ラジオ管理 DLL は、ラジオ管理 API から無線状態を取得または設定する要求を受信すると、その要求を IOCTL として対応するデバイスドライバーに転送します。 DLL は、 [DeviceIoControl](https://docs.microsoft.com/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)関数を呼び出すことによって ioctl を送信します。 ラジオ管理に関連する特定の Ioctl は次のとおりです。

- IOCTL \_ GPS \_ ラジオ \_ 管理 \_ の \_ ラジオ \_ 状態の取得

- IOCTL \_ GPS \_ ラジオ \_ 管理 \_ の \_ 前の \_ ラジオ \_ 状態の取得

- IOCTL \_ GPS \_ ラジオ \_ 管理 \_ セットの \_ 無線 \_ 状態

- IOCTL \_ GPS \_ ラジオ \_ 管理 \_ の \_ 前の \_ ラジオ \_ 状態の設定

サンプルのラジオ管理 DLL の場合、 **Csensorcommunication:: GetRadioStateHelper**メソッドと**Csensorcommunication:: SetRadioStateHelper**メソッドは、サンプルの地理位置情報ドライバーに ioctl を転送します。

## <a name="driver-support-for-radio-management"></a>ドライバーによるラジオ管理のサポート

オプション管理 DLL に加えて、DLL からドライバーに送信される4つのラジオ管理 Ioctl を処理するようにデバイスドライバーを変更する必要もあります。 これらの Ioctl は、現在の無線状態を取得する必要があることをデバイスドライバーに通知します。または、デバイスのラジオをオンまたはオフにします。

デバイスドライバーは、 **CMyQueue:: OnDeviceIoControl**メソッドの IOCTL を最初に受信して処理します。 このメソッドが4つのラジオ管理 Ioctl のいずれかを識別する場合、後続の処理を行うために、その IOCTL を**CMyDevice::P rocessiocontrolradiomanagement**メソッドに転送します。 次に、このメソッドは、IOCTL を**Csensormanager::P rocessiocontrolradiomanagement**に転送します。 この最後のメソッドでは、 **Csensorddi**クラスへの呼び出しによってオプションの状態が設定または取得されます。

**Csensorddi**クラスには、オプションの状態 (**Csensorddi:: OnGetRadioState**) を取得するメソッドと、オプションの状態 (**Csensorddi:: OnSetRadioState**) を設定するメソッドの1つが含まれています。 ここでは、ハードウェアをエミュレートするサンプルデバイスドライバーで、最終的な IOCTL 処理が行われます。 実際のデバイスドライバーの場合、 **Csensorddi:: OnGetRadioState**メソッドはデバイスのファームウェアからオプションの状態を要求し、 **Csensorddi:: OnSetRadioState**メソッドはファームウェアに要求を発行して状態を設定します。

## <a name="debugging-the-radio-management-dll"></a>オプション管理 DLL のデバッグ

次の手順を実行して、Visual Studio でラジオ管理 DLL をデバッグできます。

1. Visual Studio を開き、C++ RadioManagerGPS フォルダーで**SampleRM**を選択します。 \\

1. [**デバッグ]、[プロセスにアタッチ**] の順に選択します。 [**プロセスにアタッチ**] ダイアログボックスに表示される使用可能なプロセスの一覧で、[dllhost.exe] を選択します。

Dllhost.exe のインスタンスが複数実行されている場合は、オプション管理 DLL に関連付けられているプロセスを特定するために、削除プロセスでそれぞれを選択する必要があることに注意してください。 適切なプロセスにアタッチしたら、Visual Studio でブレークポイントを設定し、デバッグを開始できます。
