---
title: Bluetooth デバイスのインストール
description: Bluetooth デバイスのインストール
ms.assetid: 2bf2b2df-260c-42a5-9ee9-6db91f304036
keywords:
- Bluetooth の WDK をインストール
- クライアント側のプロファイル ドライバー WDK Bluetooth
- サーバー側のプロファイル ドライバー WDK Bluetooth
- INF ファイル WDK Bluetooth
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 212adebec6cd3e04f98c905d70da82bb39109cbe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328197"
---
# <a name="installing-a-bluetooth-device"></a>Bluetooth デバイスのインストール


Bluetooth プロファイル ドライバーのインストールの 2 つの種類があります。

1.  クライアント側のインストール

2.  サーバー側のインストール

クライアント側のインストールは、リモート デバイス、リモート デバイスがそのサービスをアドバタイズして、そのコンピューターを接続します。 例: マウス デバイス、キーボード、およびプリンターです。

サーバー側のインストールは、コンピューターがサービスやリモート デバイスをそれらのサービスを使用するコンピューターに接続できるをアドバタイズします。 たとえば、仕入先は、PDA、コンピューターに接続されたプリンターに印刷を有効にするサーバー側のインストールを作成できました。

これらの 2 つのインストールの種類には、別のインストール手順が必要です。

### <a name="span-idinstallingaclientsideprofiledriverspanspan-idinstallingaclientsideprofiledriverspaninstalling-a-client-side-profile-driver"></a><span id="installing_a_client_side_profile_driver"></span><span id="INSTALLING_A_CLIENT_SIDE_PROFILE_DRIVER"></span>**クライアント側のプロファイルのドライバーをインストールします。**

ユーザーは、Bluetooth 対応デバイスを使用する場合、ユーザーが、コンピューターの範囲内にデバイスを更新した後、コンピューターからリモート デバイスへの接続を開始する必要があります。 プロファイルのクライアント側ドライバーのインストールのインストールの順序を次に示します。

**クライアント側のプロファイルのドライバーをインストールするには**

1.  Bluetooth デバイスを起動**コントロール パネルの** コンピューターの範囲内のすべてのデバイスを検索します。

2.  ペアにするデバイスを選択します。

3.  ローカルの無線を使用してデバイスをペアリング (またはサマンサ)。 これは、暗証番号 (pin) exchange しないことがあります。

4.  ローカルのオプションは、リモート デバイスでサポートされているサービスを識別するために、SDP の照会を発行します。

5.  **新しいハードウェアの検出ウィザード**や Windows Update で、ローカルのハード ディスク ドライブ上の適切なドライバーを検索します。

6.  場合、**新しいハードウェアの検出ウィザード**適切なドライバーを見つけることができませんが、デバイスのユーザー プロファイルのドライバーのデバイスのセットアップ情報ファイル (INF ファイル) を含むプロファイル ドライバーのインストール メディアを挿入するように求められます。

### <a name="span-idinstallingaserversideprofiledriverspanspan-idinstallingaserversideprofiledriverspaninstalling-a-server-side-profile-driver"></a><span id="installing_a_server_side_profile_driver"></span><span id="INSTALLING_A_SERVER_SIDE_PROFILE_DRIVER"></span>**サーバー側のプロファイルのドライバーをインストールします。**

Bluetooth ドライバー スタックは、カスタム Guid (Bluetooth SIG で定義されていない Guid) と同様に、Bluetooth SIG で定義されているサービスの Guid をサポートします。

**注**  を使用することができます、 *Guidgen.exe*カスタム Guid を作成する Microsoft Windows SDK で提供されるツールです。

 

リモートの Bluetooth デバイスを使用するコンピューターの機能を公開するには、ユーザー モードのインストール アプリケーションを記述する必要があります。

インストール アプリケーションは、サービスを公開する機能の GUID を作成する Bluetooth ドライバー スタックと通信する必要があります。 ベンダーは、アプリケーションで、そのデバイスのインストールの INF ファイルで、サービスの GUID を指定します。

インストール アプリケーションは、ユーザー モード API を呼び出す必要があります**BluetoothSetLocalServiceInfo**します。 ただし、アプリケーションでは、この API を呼び出すことができます、前に、アプリケーションが必要、SE\_ロード\_ドライバー\_セキュリティ特権の名前。 次のコード例では、この特権を取得する方法を示します。 なお、例は、エラー処理を示していません。

```cpp
HANDLE procToken;
LUID luid;
TOKEN_PRIVILEGES tp;

OpenProcessToken(GetCurrentProcess(), TOKEN_ADJUST_PRIVILEGES | TOKEN_QUERY, &procToken);

LookupPrivilegeValue(NULL, SE_LOAD_DRIVER_NAME, &luid);

Tp.PrivilegeCount = 1;
Tp.privileges[0].Luid = luid;
Tp.Privileges[0].Attributes = SE_PRIVILEGE_ENABLED;

AdjustTokenPrivileges(procToken, FALSE, &tp, sizeof(TOKEN_PRIVILEGES), (PTOKEN_PRIVILEGES) NULL, (PDWORD)NULL)
```

### <a name="span-idprofiledriverinffilespanspan-idprofiledriverinffilespanprofile-driver-inf-file"></a><span id="profile_driver_inf_file"></span><span id="PROFILE_DRIVER_INF_FILE"></span>**プロファイルのドライバーの INF ファイル**

プロファイル ドライバーの INF ファイルには、インストールのクライアント側の Bluetooth デバイスに関する情報が含まれています。 サーバー側インストールでは、INF ファイルには、サービスのインストール アプリケーションで作成された GUID に対応するデバイス ID を指定します。 Bluetooth デバイスのすべてのメンバーである、 **Bluetooth**クラス。 Bluetooth クラスのインストーラー ( *Bthci.dll*) プロファイルのドライバーのインストールに役立ちます。

作成と INF ファイルを配布するドライバーのインストールの詳細については、次を参照してください。 [INF ファイルを作成する](https://msdn.microsoft.com/library/windows/hardware/ff549520)と[INF ファイルのセクションとディレクティブ](https://msdn.microsoft.com/library/windows/hardware/ff547433)します。

### <a name="span-idplugandplayidsspanspan-idplugandplayidsspanplug-and-play-ids"></a><span id="plug_and_play_ids"></span><span id="PLUG_AND_PLAY_IDS"></span>**プラグ アンド プレイ Id**

Bluetooth ドライバー スタックでは、次のテンプレートに従ってハードウェア Id が生成されます。

-   BTHENUM\\{ *ServiceGUID*}\_VID & *nnnnnnnn*

-   BTHENUM\\{ *ServiceGUID*}\_VID & *nnnnnnnn*\_PID & *nnnn*

-   BTHENUM\\{ *ServiceGUID*}\_LOCALMFG & *nnnn*

Bluetooth ドライバー スタックには、次のテンプレートに従って互換性 Id が生成されます。

-   BTHENUM\\{ *ServiceGUID*}

*ServiceGUID*は 16 ビットの GUID に展開は、128 ビットの GUID では、Bluetooth の仕様で定義されています。 たとえば、{00001124-0000-1000-8000-00805F9B34FB} は、HID デバイスに対応します。

次の 8 桁*VID &* 仕入先 ID コードに対応しています。

次の 4 桁*PID &* 製品 ID コードに対応しています。

次の 4 桁*LOCALMFG &* ローカル Bluetooth 無線の製造元に対応しています。

VID/PID と LOCALMFG タグは、相互依存しません。

ID が最も一般的なデバイス、 *ServiceGUID*自体。 次に、例を示します。

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}

プロファイルのドライバーとリモート デバイスと INF ファイルの両方でプラグ アンド プレイ Id を使用してリモート デバイスの特定のリリースでのみ実行するソフトウェアを読み込むには Bluetooth ドライバー スタックを制限することができます。 デバイスは、SDP を使用して、スタックを検出するプラグ アンド プレイ ID を発行した場合のみ、Bluetooth ドライバー スタックは VID/PID ペアを生成します。 注意してください。 次に、例を示します。

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}\_VID& *nnnnnnnn*\_PID& *nnnn*

プロファイルのドライバーと、デバイス ID、INF ファイルに含まれる LOCALMFG タグを指定することによって、特定のローカル Bluetooth 無線でのみ実行するソフトウェアを読み込むには Bluetooth ドライバー スタックを制限することができます。 次に、例を示します。

BTHENUM\\{00001124-0000-1000-8000-00805F9B34FB}\_LOCALMFG& *nnnn*

 

 





