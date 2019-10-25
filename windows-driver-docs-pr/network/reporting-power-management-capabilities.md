---
title: 電源管理機能のレポート
description: 電源管理機能のレポート
ms.assetid: cfacd885-e18a-44a5-939d-88e62b573ace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6ec12acb865f4933bcac3dca00039301b56c651
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842040"
---
# <a name="reporting-power-management-capabilities"></a>電源管理機能のレポート





Ndis 6.20 以降のバージョンの NDIS をサポートするミニポートドライバーは、初期化中にハードウェアの電源管理機能を報告します。 NDIS は、バインド操作中に、現在の機能を他の NDIS プロトコルドライバーに報告します。 ただし、NDIS では、一部の機能をプロトコルドライバーから非表示にすることができます。 たとえば、ユーザーが電源管理機能の一部またはすべてを無効にした場合、NDIS は異なる機能を報告する場合があります。

NDIS がプロトコルドライバーに報告する現在の電源管理機能は、ミニポートドライバーが NDIS に報告したハードウェア機能と必ずしも同じではないことに注意してください。

Ndis 6.1 以前のミニポートドライバーが NDIS 6.20 プロトコルドライバーにバインドされている場合、NDIS は、電源管理機能を NDIS 6.20 プロトコルドライバーでサポートされている形式に変換します。 また、ndis は、ndis 6.20 ミニポートドライバーによって報告される電源管理機能を、NDIS 6.1 以前のドライバーでサポートされている形式に変換します。

ミニポートドライバーによって報告されるハードウェア機能は、INF ファイル設定で有効または無効にすることができます。 電源管理の INF ファイル設定の詳細については、「 [Power management の標準化](standardized-inf-keywords-for-power-management.md)された inf キーワード」を参照してください。

ミニポートの初期化中に、ミニポートドライバーは、基盤となるハードウェアの電源管理機能を使用して、 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造を初期化します。 ミニポートドライバーは、ndis **\_PM\_機能**を指すように、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の構造体の**PowerManagementCapabilitiesEx**メンバーを設定します。データ.

[**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造には、次の情報が含まれています。

**示す**  
NDIS 6.20 では、このメンバーは NDIS 用に予約されています。

NDIS 6.30 以降では、次のフラグが定義されています。

<a href="" id="ndis-pm-wake-packet-indication-supported"></a>NDIS\_PM\_WAKE\_パケット\_通知\_サポートされています  
このフラグが設定されている場合、ネットワークアダプターは、アダプターがウェイクアップイベントを生成する原因となった受信パケットを保存できます。

この電源管理機能の詳細については、「 [NDIS Wake Reason Status 兆候](ndis-wake-reason-status-indications.md)」を参照してください。

<a href="" id="ndis-pm-selective-suspend-supported"></a>NDIS\_PM\_選択\_中断\_サポートされています  
このフラグが設定されている場合、ミニポートドライバーは、ネットワークアダプターに対する NDIS のセレクティブサスペンドをサポートします。

この電源管理機能の詳細については、「 [NDIS の選択的中断](ndis-selective-suspend.md)」を参照してください。

<a href="" id="supportedwolpacketpatterns"></a>**SupportedWoLPacketPatterns**  
ネットワークアダプターがサポートする wake on LAN (WOL) パケットパターンを指定するフラグが含まれています。 たとえば、ネットワークアダプターは、ビットマップ、WOL マジックパケット、または EAP over LAN (EAPOL) 要求識別子メッセージを受信したときにウェイクアップイベントを生成できます。 現在のオペレーティングシステムでサポートされているパターンの完全な一覧については、「 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)リファレンス」ページを参照してください。

<a href="" id="numtotalwolpatterns"></a>**NumTotalWoLPatterns**  
ネットワークアダプターがサポートする WOL パターンの合計数を含む**ULONG**値。 これは、「サポートされている WOL プロトコルパターンの数」と「サポートされている WOL ビットマップパターンの数」の合計です。

たとえば、ドライバーが8つの柔軟なビットマップパターン、IPv4 TCP SYN (プリセットフィルター経由)、およびマジックパケットをサポートしている場合は、NumTotalWoLPatterns で9を報告します。 (8 ビットマップ + 1 IPv4 TCP SYN = 9)

WOL パターンの合計数にマジックパケットウェイクアップパターンが含まれていない  に**注意**してください。

 

WOL プロトコルパターンの詳細については、「 [**NDIS\_PM\_wol\_パターン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)」を参照してください。

<a href="" id="maxwolpatternsize"></a>**MaxWoLPatternSize**  
パターンと比較できる最大バイト数を格納します。

<a href="" id="maxwolpatternoffset"></a>**MaxWoLPatternOffset**  
MAC ヘッダーの先頭から開始する、検査可能なパケット内のバイト数を格納します。

<a href="" id="maxwolpacketsavebuffer"></a>**MaxWoLPacketSaveBuffer**  
ミニポートドライバーがバッファーに保存できる WOL プロトコルパターンのバイト数を格納し、ドライバースタックを示します。

<a href="" id="supportedprotocoloffloads"></a>**SupportedProtocolOffloads**  
ネットワークアダプターがサポートする電源管理プロトコルのオフロード機能を指定するフラグが含まれています。 ミニポートドライバーは、これらのフラグを使用して、ネットワークアダプターの低電力プロトコルオフロード機能を報告します。 たとえば、ネットワークアダプターは、IPv4 ARP オフロード、IPv6 近隣要請 (NS)、または IEEE 802.11 の堅牢なセキュリティで保護されたネットワーク (RSN) の4方向および双方向のハンドシェイクをサポートできます。 現在のオペレーティングシステムでサポートされているプロトコルオフロードの完全な一覧については、「 [**NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)のリファレンス」ページを参照してください。

<a href="" id="numarpoffloadipv4addresses"></a>**NumArpOffloadIPv4Addresses**  
ARP オフロード IPv4 アドレスの数が含まれます。

<a href="" id="numnsoffloadipv6addresses"></a>**NumNSOffloadIPv6Addresses**  
ネットワークアダプターがサポートするネットワーク要請 (NS) オフロード IPv6 要求の数を含みます。

<a href="" id="minmagicpacketwakeup"></a>**MinMagicPacketWakeUp**  
ネットワークアダプターが*マジックパケット*の受信時にウェイクアップイベントを通知できる最も低いデバイス電源状態を指定します。 (*マジックパケット*は、受信側のネットワークアダプターのイーサネットアドレスの連続した16個のコピーを含むパケットです)。

<a href="" id="minpatternwakeup"></a>**Minpattern ウェイクアップ**  
プロトコルドライバーによって指定されたパターンを含むネットワークフレームを受信したときに、ネットワークアダプターがウェイクアップイベントを通知できる最も小さいデバイスの電源状態を指定します。

<a href="" id="minlinkchangewakeup"></a>**MinLinkChangeWakeUp**  
リンクの変更 (メディアの接続または切断) が発生したときに、ネットワークアダプターがウェイクアップイベントを通知できる最も低いデバイスの電源状態を指定します。

<a href="" id="supportedwakeupevents"></a>**SupportedWakeUpEvents**  
ネットワークアダプターがサポートする、メディアに依存しないウェイクアップイベントを指定します。 これらのイベントは、メディアの種類に固有のものではありません。 たとえば、これらのウェイクアップイベントには、リンク変更イベントが含まれます。

<a href="" id="mediaspecificwakeupevents"></a>**MediaSpecificWakeUpEvents**  
ネットワークアダプターがサポートするメディア固有のウェイクアップイベントを指定します。 たとえば、次のようなイベントがあります。

-   802.11 ネットワークアダプターがアクセスポイント (AP) との関連付けを解除します。

-   モバイルブロードバンド (MB) ネットワークアダプターは、その登録状態の変更を MB サービスに対して検出します。

ミニポートドライバーが低電力状態のネットワークアダプターへのオフロードプロトコルをサポートしている場合は、パターンマッチ WOL イベントに対してサポートされているプロトコルオフロードに対して、同じ低電力状態をサポートする必要があります。つまり、 **Minpattern ウェイクアップ**または**MinMagicPacketWakeUp**メンバーに指定された値です。

NDIS は、基盤となるネットワークアダプターの現在使用可能な電源管理機能を使用して、 [**ndis\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造を初期化し、バインド操作中にプロトコルにプロトコルを渡します。 Ndis は、ndis\_PM\_CAPABILITIES 構造体を指すように、 [**ndis\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)構造体**のメンバーを**設定します。

これまでのドライバーでは、 [oid\_PM\_ハードウェア\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-hardware-capabilities)の oid クエリを使用して、ネットワークアダプターのハードウェア電源管理機能を取得できます。 NDIS は、ミニポートドライバーに代わってこの OID 要求を処理します。 NDIS ミニポートドライバーは、OID\_PM\_ハードウェア\_機能の OID 要求をサポートするために必要ありません。

それまでのドライバーでは、 [oid\_PM\_現在の\_機能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-current-capabilities)oid を使用して、ネットワークアダプターの現在使用可能な電源管理機能を照会できます。 NDIS は、ミニポートドライバーに代わってこの OID 要求を処理します。 NDIS ミニポートドライバーは、OID\_PM\_現在の\_機能 OID 要求をサポートするためには必要ありません。

 

 





