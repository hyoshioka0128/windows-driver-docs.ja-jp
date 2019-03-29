---
title: SCSI ミニポート ドライバーのレジストリ エントリ
description: SCSI ミニポート ドライバーのレジストリ エントリ
ms.assetid: bff5c004-7115-4436-b233-9d1d89643b23
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、レジストリ エントリ
- レジストリ WDK SCSI
- TimeoutValue
- TotalSenseDataBytes
- MaximumSGList
- BusType
- CreateInitiatorLU
- 擬似 Lun WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3029c27c35aa3f8f09e7df6951acc413f3dda16a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580773"
---
# <a name="registry-entries-for-scsi-miniport-drivers"></a>SCSI ミニポート ドライバーのレジストリ エントリ


## <span id="ddk_registry_entries_for_scsi_miniport_drivers_kg"></span><span id="DDK_REGISTRY_ENTRIES_FOR_SCSI_MINIPORT_DRIVERS_KG"></span>


次のレジストリ エントリを使用すると、ポート ドライバー/SCSI ミニポート ドライバーのペアの動作を構成できます。 PnpInterface レジストリ エントリをすべてプラグ アンド プレイ (PnP) デバイスに必要な詳細については、次を参照してください。[プラグ アンド プレイ SCSI ミニポート ドライバーのレジストリ エントリ](registry-entries-for-plug-and-play-scsi-miniport-drivers.md)します。

-   **TimeoutValue**
    -   所在地:HKLM\\システム\\CurrentControlSet\\サービス\\ディスク\\TimeoutValue
    -   値:1-255 秒
    -   意味:ディスクのクラス ドライバーによって開始された、SRB 要求がタイムアウトするまでの秒の単位の時間です。このレジストリ値が設定されていない場合は、10 秒の既定値が使用されます。 クラスのドライバーによって開始された要求のタイムアウト値は、クラス ドライバーによって異なります。

        **注**  そのタイムアウトを優先的に受け入れられるミニポートが値を設定する場合。 タイムアウトの選択ロジックは次のとおりです。
        -   ミニポート (HKLM... でタイムアウト値を設定する場合、Windows 8 以降 \\サービスの\\&lt;ミニポート&gt;\\パラメーター\\IoTimeoutValue)、この値は記憶域クラス ドライバーで受け入れられます。
        -   それ以外の場合、ディスク グローバル タイムアウト レジストリ (このキー) が設定されている場合、この値は記憶域クラス ドライバーで受け入れられます。
        -   それ以外の場合、10 秒の既定値は、記憶域クラス ドライバーによって使用されます。

         

    -   オペレーティング システムのバージョン:この機能は、Windows オペレーティング システムのすべてのバージョンで使用できます。

<!-- -->

-   **TotalSenseDataBytes**
    -   所在地:HKLM\\システム\\CurrentControlSet\\Enum\\&lt;Bus&gt; \\ &lt; DeviceID&gt;\\&lt;デバイス&gt;\\DeviceParameters\\ScsiPort\\TotalSenseDataBytes
    -   値:18 と SCSI ポート 255 までの間 Storport は常に、255 を使用します。
    -   意味:この値が設定の指定、バッファーのバイト サイズ SCSI ポート ドライバーはセンス データの要求を割り当てます。 値が設定されていない場合、SCSI ポートは、18 の既定のサイズを使用します。 Storport ドライバーは、255 を常に許可します。 警告: フィルター ドライバー クラス ドライバーとポートのドライバーの間に挿入する必要がありますこの値を尊重およびセンス データ バッファーのサイズを管理しようとします。
    -   オペレーティング システムのバージョン:この機能は、Windows 2000 Server および以降のオペレーティング システムで使用できます。
-   **MaximumSGList**
    -   所在地:HKLM\\システム\\CurrentControlSet\\サービス\\&lt;ServiceName&gt;\\パラメーター\\デバイス\\MaximumSGList、場所&lt;ServiceName&gt; = ミニポート ドライバー名で指定された、 **AddServices** INF ファイルでディレクティブ。
    -   値:16 ~ 255 の範囲です。
    -   意味:アダプターでサポートされているスキャッター/ギャザー リストの要素の数を示します。
    -   オペレーティング システムのバージョン:この機能は、Windows NT 4.0 SP4 および以降のオペレーティング システムで使用できます。
-   **BusType**
    -   所在地:HKLM\\システム\\CurrentControlSet\\サービス\\&lt;ServiceName&gt;\\パラメーター\\バスの種類、場所&lt;ServiceName&gt; = ミニポート ドライバー名で指定された、 **AddServices** INF ファイルでディレクティブ。
    -   値:同じ[**ストレージ\_BUS\_型**](https://msdn.microsoft.com/library/windows/hardware/ff566356)列挙子。
    -   意味:アダプターが接続されているバスの種類を示します。
    -   オペレーティング システムのバージョン:この機能は、Windows 2000 以降のオペレーティング システムで使用できます。
-   **CreateInitiatorLU**
    -   所在地:&lt;ServiceName&gt;\\パラメーター\\デバイス\\CreateInitiatorLU、場所&lt;ServiceName&gt; = ミニポート ドライバー名で指定された、 **AddServices**INF ファイルでディレクティブ。
    -   値:0 または 1。
    -   意味:1 の値がより高度なドライバーは、あるアダプターを実際のハードウェア デバイスが接続されていないか、接続されたデバイスが表示されていない場合でもに、ポート ドライバーの特定の要求を送信できるようにするポート ドライバーは、"開始側論理ユニットを作成"を示しますシステム。 デバイスの操作パラメーターの設定は、システムに表示される前に、そのファームウェアを更新するために必要な場合があります。 Windows Server 2003 では、前に、ポート、ポート ドライバーでは、そのデバイス スタックで少なくとも 1 つの論理ユニットが必要があるしない限り、デバイスのファームウェアを更新するドライバーに指示することでした。 一部のベンダーが、アダプターのスタックが、このセットアップとディスクの管理の問題を作成する、いわゆる"擬似 Lun"を追加することでこの問題を解決しようとして、このようなソリューションは、構成マネージャーがユーザーに要求が発生することがあります、存在しないデバイスのドライバーです。 「開始側の論理ユニット」の新しい機能は、これらの解決策の手法を使用する必要は不要になったです。 設定して**CreateInitiatorLU**をレジストリに 1 には、Ioctl を送信できます。 また WMI 要求ポート ドライバーに接続されているオペレーティング システムに表示されているデバイスがあるかどうか。 「開始側の論理ユニット」機能の使用をもう 1 つと通信するファイバー チャネル アダプターを持つ関数を純粋な管理と接続されているデバイスがありません。
    -   オペレーティング システムのバージョン:この機能は、Windows Server 2003 および以降のオペレーティング システムで使用できます。 このレジストリ値の値には、SCSI ポート ミニポート ドライバーの機能のみに影響します。 Storport ミニポート ドライバーは、アダプターに接続されているデバイスがない場合でも常に、アダプター オブジェクトへのアクセスを許可します。

 

 




