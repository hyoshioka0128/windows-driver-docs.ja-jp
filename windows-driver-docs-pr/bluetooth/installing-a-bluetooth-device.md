---
title: Bluetooth デバイスのインストール
description: Bluetooth デバイスのインストール
ms.assetid: 2bf2b2df-260c-42a5-9ee9-6db91f304036
keywords:
- Bluetooth WDK、bluetooth ドライバーのインストール
- クライアント側プロファイルドライバー WDK Bluetooth
- サーバー側プロファイルドライバー WDK Bluetooth
- INF ファイル WDK Bluetooth
ms.date: 05/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 2921c56b2f33c7ffe29fc3cb9ad9f3fb2211fffb
ms.sourcegitcommit: 5b4742d8983f6a194416fd6bc7ec837a12822565
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84211981"
---
# <a name="installing-a-bluetooth-device"></a>Bluetooth デバイスのインストール

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 Bluetooth デバイスのインストールの問題が発生しているお客様の場合は[、「Windows での bluetooth デバイスのペアリング](https://support.microsoft.com/help/15290/windows-connect-bluetooth-device)」を参照してください。

Bluetooth プロファイルドライバーには、次の2種類のインストールがあります。

- リモートデバイスがサービスをアドバタイズし、コンピューターから接続するリモートデバイスの**クライアント側インストール**。 例としては、マウスデバイス、キーボード、プリンターなどがあります。

- コンピューターがサービスとリモートデバイスをアドバタイズする**サーバー側のインストール**は、これらのサービスを使用するためにコンピューターに接続できます。 たとえば、ベンダーはサーバー側のインストールを作成して、PDA がコンピューターに接続されているプリンターに印刷できるようにすることができます。

この2つのインストールの種類には、異なるインストール手順が必要です。

## <a name="installing-a-client-side-profile-driver"></a>クライアント側プロファイルドライバーのインストール

Bluetooth 対応デバイスを使用するユーザーは、そのデバイスをコンピューターの範囲内に移動し、次のクライアント側プロファイルドライバーのインストールシーケンスを使用して、コンピューターからリモートデバイスへの接続を開始します。

1. **コントロールパネル**の [Bluetooth デバイス] を起動して、コンピューターの範囲内にあるすべてのデバイスを検索します。

2. ペアリングするデバイスを選択します。

3. デバイスをローカルラジオとペアリング (または bond) します。 これには、PIN の交換が必要になる場合と、含まれない場合があります。

4. ローカルラジオは、リモートデバイスでサポートされているサービスを識別するために SDP の問い合わせを発行します。

5. **新しいハードウェアの検出ウィザード**では、ローカルハードディスクドライブ、または Windows Update で適切なドライバーが検索されます。

6. **新しいハードウェアの検出ウィザード**でデバイスの適切なドライバーが検出されなかった場合は、プロファイルドライバーのデバイスセットアップ情報ファイル (INF ファイル) を含むプロファイルドライバーのインストールメディアを挿入するように求められます。

## <a name="installing-a-server-side-profile-driver"></a>サーバー側プロファイルドライバーのインストール

Bluetooth ドライバースタックは、Bluetooth SIG で定義されているサービス Guid に加えて、カスタム Guid (つまり、Bluetooth SIG で定義されていない Guid) もサポートしています。

> [!NOTE]
> Microsoft Windows SDK に用意されている**guidgen.exe**ツールを使用して、カスタム guid を作成できます。

リモート Bluetooth デバイスで使用できるコンピューター機能を公開するには、ユーザーモードインストールアプリケーションを作成する必要があります。

インストールアプリケーションは、Bluetooth ドライバースタックと通信して、公開する機能のサービス GUID を作成する必要があります。 ベンダーは、アプリケーションとデバイスのインストール INF ファイルにサービス GUID を指定します。

インストールアプリケーションでは、ユーザーモード API [BluetoothSetLocalServiceInfo](https://docs.microsoft.com/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothsetlocalserviceinfo)を呼び出す必要があります。 アプリケーションでこの API を呼び出すには、アプリケーションに "SE \_ LOAD \_ DRIVER NAME" セキュリティ特権が必要 \_ です。 この特権を取得する方法を次のコード例に示します。 この例では、エラー処理を示していないことに**注意**してください。

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

## <a name="profile-driver-inf-file"></a>プロファイルドライバーの INF ファイル

プロファイルドライバーの INF ファイルには、クライアント側インストール用の Bluetooth デバイスに関する情報が含まれています。 サーバー側のインストールの場合、INF ファイルは、インストールアプリケーションによって作成されたサービス GUID に対応するデバイス ID を指定します。 すべての Bluetooth デバイスは、 **bluetooth**クラスのメンバーです。 Bluetooth クラスインストーラー (*Bthci .dll*) は、プロファイルドライバーのインストールに役立ちます。

INF ファイルの作成と配布、およびドライバーのインストールの詳細については、「 [Inf ファイル](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)および inf ファイルの作成」[セクションと「ディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。

### <a name="plug-and-play-ids"></a>プラグアンドプレイ Id

Bluetooth ドライバースタックは、次のテンプレートに従ってハードウェア Id を生成します。

- BTHENUM \\ { *ServiceGUID*} \_ VID& *nnnnnnnn*

- BTHENUM \\ { *ServiceGUID*} \_ VID& *nnnnnnnn* \_ PID& *nnnn*

- BTHENUM \\ { *ServiceGUID*} \_ localmfg& *nnnn*

Bluetooth ドライバースタックは、次のテンプレートに従って、互換性のある Id を生成します。

- BTHENUM \\ { *ServiceGUID*}

*ServiceGUID*は、Bluetooth 仕様で定義されているように、128ビット guid に拡張された16ビット guid です。 たとえば、{000011240000-10008-8000-00805F9B34FB} は、HID デバイスに対応しています。

- *VID&* の後の8桁は、ベンダー ID コードに対応しています。

- *PID&* の4桁の数字は、製品 ID コードに対応しています。

- *Localmfg&* の次の4桁は、ローカル Bluetooth ラジオの製造元に対応しています。

- VID/PID タグと LOCALMFG タグは互いに独立しています。

最も一般的なデバイス ID は、単独で*ServiceGUID*です。 例:

BTHENUM \\ {000011240000-10008-8000-00805F9b34fb}

Bluetooth ドライバースタックは、リモートデバイスと INF ファイルの両方でプラグアンドプレイ Id を使用して、リモートデバイスの特定のリリースでのみ実行されるように、プロファイルドライバーとソフトウェアを読み込むように制限できます。 Bluetooth ドライバースタックは、デバイスが SDP を使用して検出できるプラグアンドプレイ ID を発行する場合にのみ、VID と PID のペアを生成することに**注意**してください。 例:

BTHENUM \\ {000011240000-10008-8000-00805F9b34fb} \_ VID& *nnnnnnnn* \_ PID& *nnnn*

Bluetooth ドライバースタックは、特定のローカル Bluetooth ラジオでのみ実行されるプロファイルドライバーとソフトウェアを読み込むように制限できます。これを行うには、INF ファイルのデバイス ID に LOCALMFG タグを指定します。 例:

BTHENUM \\ {000011240000-10008-8000-00805F9b34fb} \_ localmfg& *nnnn*
