---
title: 無線管理のサポート
description: ユーザーが、Windows 8 ラップトップ、ノートブック、または tablet PC 設定で [ワイヤレス] オプションをオンまたはオフ、接続しているワイヤレス デバイスを有効にできます。
ms.assetid: AA7AB429-30C5-4C10-AA85-41ED9EAEE69A
keywords:
- 無線管理 API
- 無線管理 API、例
- 無線管理、例
- GPS 無線管理
- GPS 無線管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cd840a2c99a3518d4ea32c58e133bb011515bfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363619"
---
# <a name="supporting-radio-management"></a>無線管理のサポート

> [!IMPORTANT] 
> このドキュメントと Windows 8.1 の地理的位置情報ドライバー サンプルが非推奨とされました。

ユーザーが、Windows 8 ラップトップ、ノートブック、または tablet PC 設定で [ワイヤレス] オプションをオンまたはオフ、接続しているワイヤレス デバイスを有効にできます。 これらのワイヤレス デバイスには、Wi-fi アンテナまたは GPS デバイスを含めることができます。 PC の設定と特定のワイヤレス デバイスの間、内部リンケージを持ちますが、[ラジオ管理 API](https://docs.microsoft.com/previous-versions/windows/hardware/radio/hh406615(v=vs.85))と特定のデバイスの対応するラジオ管理 DLL。

ラジオの管理 API は、Windows Driver Kit の一部として出荷されます/Win32 COM インターフェイスのセットです。 これらのインターフェイスにはメソッドが含まれています。

-   無線デバイスの現在の状態を取得します。
-   無線デバイスに通知イベントをサポートします。
-   (表示名) などのデバイス プロパティを取得します。

これらのインターフェイスは、アプリケーション開発者ではなく、Oem および Ihv のみを対象としています。

## <a name="the-radio-management-dynamic-link-library-dll"></a>無線管理ダイナミック リンク ライブラリ (DLL)


無線デバイスの場合、GPS のようなデバイス ドライバーを作成する場合、ドライバーは、追加ダイナミック リンク ライブラリ (DLL、ラジオの管理 API でインターフェイスをサポートする) を含める必要があります。 この DLL の要件を理解するために、Microsoft では、地理的位置情報ドライバー サンプルの一部としてサンプルの Microsoft Visual Studio プロジェクトとソース コードが付属しています。 このサンプル プロジェクト SampleRM.vcxproj はセンサー地理位置情報ドライバー サンプルが見つかりません。\\C++\\ドライバーのサンプルの RadioManagerGPS フォルダー。 C++ ソース ファイルの 7 つ、6 つの C++ ヘッダー ファイル、モジュール定義ファイル、リソース ファイル、2 つの IDL ファイル、レジストリ ファイル (DLL)、登録をおよび、インストール スクリプトが含まれています。

次の表は、ラジオの管理 API のメソッドとサンプルの DLL 内の対応するメソッドを示します。

|                                                     |                                                       |
|-----------------------------------------------------|-------------------------------------------------------|
| ラジオ Manager API                                   | ラジオ Manager DLL                                     |
| IMediaRadioManager::GetRadioInstances               | CSampleRadioManager::GetRadioInstances                |
| IMediaRadioManager::OnSystemRadioStateChange        | CSampleRadioManager::OnSystemRadioStateChange         |
| IRadioInstance::GetFriendlyName                     | CSampleRadioInstance::GetFriendlyName                 |
| IRadioInstance::GetInstanceSignature                | CSampleRadioInstance::GetInstanceSignature            |
| IRadioInstance::GetRadioManagerSignature            | CSampleRadioInstance::GetRadioManagerSignature        |
| IRadioInstance::GetRadioState                       | CSampleRadioInstance::GetRadioState                   |
| IRadioState::IsAssociatingDevice                    | CSampleRadioInstance::IsAssociatingDevice             |
| IRadioState::IsMultiComm                            | CSampleRadioInstance::IsMultiComm                     |
| IRadioState::SetRadioState                          | CSampleRadioInstance::SetRadioState                   |
| IRadioInstanceCollection::GetAt                     | CRadioInstanceCollection::GetAt                       |
| IRadioInstanceCollection::GetCount                  | CRadioInstanceCollection::GetCount                    |
| IMediaRadioManagerNotifySink::OnInstanceAdd         | CSampleRadioManager::\_FireEventOnInstanceAdd         |
| IMediaRadioManagerNotifySink::OnInstanceRadioChange | CSampleRadioManager::\_FireEventOnInstanceRadioChange |
| IMediaRadioManagerNotifySink::OnInstanceRemove      | CSampleRadioManager::\_FireEventOnInstanceRemove      |

 

## <a name="communicating-with-the-device-driver"></a>デバイス ドライバーとの通信


無線管理 DLL を取得または無線管理 API からオプションの状態を設定する要求を受け取ったときに、対応するデバイス ドライバーを IOCTL としてその要求を転送します。 DLL を呼び出すことによって Ioctl の送信、 [DeviceIoControl]( https://go.microsoft.com/fwlink/p/?linkid=256462)関数。 特定の Ioctl ラジオの管理に関連するには。

-   IOCTL\_GPS\_ラジオ\_管理\_取得\_ラジオ\_状態
-   IOCTL\_GPS\_ラジオ\_管理\_取得\_前\_ラジオ\_状態
-   IOCTL\_GPS\_ラジオ\_管理\_設定\_ラジオ\_状態
-   IOCTL\_GPS\_ラジオ\_管理\_設定\_前\_ラジオ\_状態

サンプルの無線管理の場合、DLL、 **CSensorCommuncation::GetRadioStateHelper**と**CSensorCommunication::SetRadioStateHelper**メソッド転送 Ioctl ようサンプル地理的位置情報ドライバー。

## <a name="driver-support-for-radio-management"></a>無線管理のドライバー サポート


無線管理 DLL、だけでなく、DLL からドライバーに送信される 4 つのラジオ管理 Ioctl を処理するために、デバイス ドライバーを変更する必要があります。 これらの Ioctl は、する必要がありますの現在のオプションの状態を取得またはという、デバイスの無線をオンまたはオフにデバイス ドライバーを通知します。

デバイス ドライバーを最初に受信して、IOCTL での処理、 **CMyQueue::OnDeviceIoControl**メソッド。 このメソッドは、次の 4 つのラジオ管理 Ioctl のいずれかを識別する場合にその IOCTL を転送、 **CMyDevice::ProcessIoControlRadioManagement**メソッドをさらに処理します。 このメソッドは、さらに IOCTL に転送**CSensorManager::ProcessIoControlRadioManagement**します。 オプションの状態の設定または取得への呼び出しによってこの最後のメソッド内で、 **CSensorDDI**クラス。

**CSensorDDI**クラスには、オプションの状態を取得する 1 つのメソッドが含まれています (**CSensorDDI::OnGetRadioState**) とオプションの状態を設定する 1 つのメソッド (**CSEnsorDDI::OnSetRadioState**). これは、ハードウェアをエミュレートするサンプルのデバイス ドライバーの IOCTL の最終処理が発生します。 場合は、実際のデバイス ドライバー、 **CSensorDDI::OnGetRadioState**メソッドは、デバイスのファームウェアからオプションの状態を要求し、 **CSensorDDI::OnSetRadioState**メソッドは、発行、状態を設定するファームウェアを要求します。

## <a name="debugging-the-radio-management-dll"></a>無線管理 DLL のデバッグ


Visual Studio で無線管理 DLL をデバッグするには、次の手順を完了します。

1.  1. Visual Studio を開き、選択**SampleRM.vcsproj** C++ で\\RadioManagerGPS フォルダー。
2.  2. 選択**デバッグ/プロセスにアタッチ**します。 表示される選択可能なプロセスの一覧で、**プロセスにアタッチ**ダイアログ ボックスで、dllhost.exe 選択します。

Dllhost.exe の複数のインスタンスが実行されている場合は、無線管理 DLL に関連付けられているプロセスを決定するために削除のプロセスでそれぞれを選択する必要がありますに注意してください。 適切なプロセスにアタッチした後は、Visual Studio でブレークポイントを設定し、デバッグを開始できます。

 

 




