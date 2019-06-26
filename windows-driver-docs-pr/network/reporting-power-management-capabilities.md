---
title: 電源管理機能のレポート
description: 電源管理機能のレポート
ms.assetid: cfacd885-e18a-44a5-939d-88e62b573ace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80a8f681cb84843ca7343fb637ab8f1f1c65a521
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373247"
---
# <a name="reporting-power-management-capabilities"></a>電源管理機能のレポート





サポート NDIS 6.20 が動作し、以降のバージョンの NDIS ミニポート ドライバーでは、初期化中に、ハードウェアの電源管理機能を報告します。 NDIS は、NDIS プロトコル ドライバーをバインド操作中に関連する現在の機能を報告します。 ただし、NDIS は、プロトコル ドライバーからいくつかの機能を非表示にすることができます。 たとえば、NDIS は、ユーザーは、電源管理機能の一部またはすべて無効にします。 ときに、さまざまな機能を報告する可能性があります。

プロトコル ドライバーに NDIS を報告する現在の電源管理機能できないが必ずしもに NDIS ミニポート ドライバーが報告されたハードウェアの機能と同じに注意してください。

NDIS 6.1 または以前のミニポート ドライバーは、NDIS 6.20 プロトコル ドライバーにバインドする場合、NDIS は、NDIS 6.20 プロトコル ドライバーでサポートされている形式に電源管理機能を変換します。 NDIS は、NDIS 6.20 が動作のミニポート ドライバーは、NDIS 6.1 と前の上位のドライバーでサポートされている形式にレポートを電源管理機能にも変換します。

ミニポート ドライバーを報告するハードウェアの機能を有効になっているまたは INF ファイルの設定で無効になっていることができます。 電源管理 INF ファイルの設定の詳細については、次を参照してください。[電源管理のための標準化された INF キーワード](standardized-inf-keywords-for-power-management.md)します。

ミニポートの初期化中に、ミニポート ドライバーを初期化します、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)基になるの電源管理機能を含む構造体ハードウェア。 ミニポート ドライバーのセット、 **PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体を指す、 **NDIS\_PM\_機能**構造体。

[ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体には、次の情報が含まれています。

**フラグ**  
NDIS 6.20 が動作のこのメンバーは、NDIS の予約されています。

NDIS 6.30 以降では、次のフラグが定義されます。

<a href="" id="ndis-pm-wake-packet-indication-supported"></a>NDIS\_PM\_WAKE\_パケット\_INDICATION\_サポートされています。  
このフラグが設定されている場合、ネットワーク アダプターは、アダプターが、ウェイク アップのイベントを生成する原因となった受信パケットを保存できます。

この電源管理機能の詳細については、次を参照してください。 [NDIS Wake 理由状態インジケーター](ndis-wake-reason-status-indications.md)します。

<a href="" id="ndis-pm-selective-suspend-supported"></a>NDIS\_PM\_セレクティブ\_SUSPEND\_サポートされています。  
このフラグが設定されている場合、選択的 NDIS の中断のミニポート ドライバーではネットワーク アダプターを使用します。

この電源管理機能の詳細については、次を参照してください。 [NDIS セレクティブ サスペンド](ndis-selective-suspend.md)します。

<a href="" id="supportedwolpacketpatterns"></a>**SupportedWoLPacketPatterns**  
ネットワーク アダプターをサポートする wake on LAN (WOL) パケットのパターンを指定するフラグが含まれています。 たとえば、ネットワーク アダプターでは、ビットマップ、WOL マジック パケットの場合、または EAP over LAN (EAPOL) 要求の識別子のメッセージを受信すると、ウェイク アップ イベントを生成できます。 現在のオペレーティング システムでサポートされているパターンの完全な一覧を参照してください、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)リファレンス ページです。

<a href="" id="numtotalwolpatterns"></a>**NumTotalWoLPatterns**  
A **ULONG**ネットワーク アダプターをサポートする WOL パターンの合計数を表す値です。 これは、「サポートされている WOL ビットマップ パターンの数」と「サポートされている、WOL プロトコル パターンの数」の合計

たとえばには、ドライバーは、8 の柔軟なビットマップ パターン、(事前設定されたフィルターの場合) を使用して IPv4 TCP SYN およびマジック パケットをサポートする場合は、NumTotalWoLPatterns で 9 を報告するは。 (8 ビットマップ + 1 の IPv4 TCP SYN = 9)

**注**  WOL パターンの合計数は、マジック パケットとウェイク アップのパターンが含まれません。

 

WOL プロトコル パターンの詳細については、次を参照してください。 [ **NDIS\_PM\_WOL\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)します。

<a href="" id="maxwolpatternsize"></a>**MaxWoLPatternSize**  
パターンと比較できるバイトの最大数が含まれています。

<a href="" id="maxwolpatternoffset"></a>**MaxWoLPatternOffset**  
MAC ヘッダーの先頭から開始されるパケット検査できるバイト数が含まれています。

<a href="" id="maxwolpacketsavebuffer"></a>**MaxWoLPacketSaveBuffer**  
ミニポート ドライバーは、バッファーに保存でき、ドライバー スタックを示す WOL プロトコル パターンのバイト数が含まれています。

<a href="" id="supportedprotocoloffloads"></a>**SupportedProtocolOffloads**  
ネットワーク アダプターでサポートされる機能、電源管理プロトコルの負荷を軽減するかを指定するフラグが含まれています。 ミニポート ドライバーでは、低電力プロトコルのネットワーク アダプターの機能をオフロードするレポートにこれらのフラグを使用します。 たとえば、ネットワーク アダプターでは、IPv4 ARP オフロード、IPv6 近隣要請 (NS) または IEEE 802.11 堅牢なセキュリティで保護されたネットワーク (RSN) 4 ウェイと 2 ウェイ ハンドシェイクをサポートできます。 現在のオペレーティング システムでサポートされているプロトコルのオフロードの完全な一覧を参照してください、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)リファレンス ページです。

<a href="" id="numarpoffloadipv4addresses"></a>**NumArpOffloadIPv4Addresses**  
ARP オフロードの IPv4 アドレスの数が含まれています。

<a href="" id="numnsoffloadipv6addresses"></a>**NumNSOffloadIPv6Addresses**  
ネットワークの要請 (NS) オフロード、ネットワーク アダプターをサポートする IPv6 要求の数が含まれています。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
ネットワーク アダプターがの受信時にウェイク アップのイベントを信号最低のデバイスの電源状態を指定します、*マジック パケット*します。 (A*マジック パケット*は受信側のネットワーク アダプターのイーサネット アドレスの 16 個の連続したコピーを含むパケットです)。

<a href="" id="minpatternwakeup"></a>**MinPatternWakeUp**  
ネットワーク アダプターがプロトコル ドライバーで指定されたパターンを含むネットワーク フレームの受信時にウェイク アップのイベントを信号最低のデバイスの電源状態を指定します。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
ネットワーク アダプターが、リンクの変更 (メディアを接続または切断) がある場合は、ウェイク アップのイベントを信号最低のデバイスの電源状態を指定します。

<a href="" id="supportedwakeupevents"></a>**SupportedWakeUpEvents**  
ネットワーク アダプターをサポートするメディアに依存しないウェイク アップのイベントを指定します。 これらのイベントは、メディアの種類に固有ではありません。 たとえば、これらのウェイク アップ イベントには、リンクの変更イベントが含まれます。

<a href="" id="mediaspecificwakeupevents"></a>**MediaSpecificWakeUpEvents**  
ネットワーク アダプターをサポートするメディア固有のウェイク アップのイベントを指定します。 たとえば、これらのイベントが含まれる次。

-   アクセス ポイント (AP) と 802.11 ネットワーク アダプターの関連付けを解除します。

-   モバイル ブロード バンド (MB) のネットワーク アダプターでは、MB サービスへの登録状態の変更を検出します。

プロトコルを低電力状態のネットワーク アダプターのオフロードをサポートするには、プロトコルの同じ低電力状態をサポートする必要があります、ミニポート ドライバーの負荷を軽減するパターン一致 WOL イベント; のサポートします。つまり、値で指定されている、 **MinPatternWakeUp**または**MinMagicPacketWakeUp**メンバー。

NDIS を初期化します、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)基になるネットワーク アダプターの現在使用できる電源管理機能を含む構造体を渡しますバインド操作中にプロトコル ドライバーを後続のプロトコルです。 NDIS セット、 **PowerManagementCapabilitiesEx**のメンバー、 [ **NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters) NDISを指す構造体\_PM\_機能の構造体。

使用できるドライバーが重なって、 [OID\_PM\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-hardware-capabilities)をネットワーク アダプターのハードウェアの電源管理機能を取得する OID クエリ。 NDIS は、ミニポート ドライバーに代わってこの OID 要求を処理します。 NDIS ミニポート ドライバーが、OID をサポートする必要はありません\_PM\_ハードウェア\_機能 OID 要求。

使用できるドライバーが重なって、 [OID\_PM\_現在\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-current-capabilities)ネットワーク アダプターの現在使用できる電源管理機能を照会する OID。 NDIS は、ミニポート ドライバーに代わってこの OID 要求を処理します。 NDIS ミニポート ドライバーが、OID をサポートする必要はありません\_PM\_現在\_機能 OID 要求。

 

 





