---
title: NDIS ウェイク理由状態表示の概要
description: NDIS ウェイク理由状態表示の概要
ms.assetid: 94B54281-7A7E-4DBA-85AE-313EEF09E733
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f174738bab9d6bbffdab9a28d29606be4c4921b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573679"
---
# <a name="overview-of-ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示の概要


NDIS 6.30 以降、ミニポート ドライバーで NDIS ウェイク アップの理由の状態を示す値を発行 ([**NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) するNDIS とシステムのウェイク アップ イベントの理由についての上にあるドライバーに通知します。 ネットワーク アダプターでは、ウェイク アップのイベントを生成する場合、ミニポート ドライバーのすぐに問題の NDIS 状態を示す値**NDIS\_状態\_PM\_WAKE\_理由**とネットワークアダプターは、完全な電源状態を再開します。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

オブジェクト識別子 (OID) セット要求を電源管理 (PM) パラメーターを持つ、ミニポート ドライバーが構成されている[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)します。 この OID 要求を通じて PM パラメーターを指定する、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

[ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造がウェイク アップのイベントの種類は次のパラメーターを指定します。

<a href="" id="received-packet-wake-up-events"></a>受信パケットのウェイク アップ イベント  
ネットワーク アダプターでは、wake on LAN (WOL) のパターンに一致するパケットを受信した場合、ウェイク アップ イベントが生成されます。 WOL パターンを以下に示します。

-   マジック パケットや TCP/IP パケット ペイロード内のデータのパターンなどのメディアに依存しない WOL パターン。 たとえば、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体の TCP SYN フレーム WOL パターンを指定できます。

-   EAPOL 要求識別子パケットやモバイル ブロード バンド (MB) のショート メッセージ サービス (SMS) メッセージなどのメディア固有 WOL パターン。

-   OID セットの要求で指定された受信フィルターと一致するワイルドカード パターン[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

**注**  この種類のウェイク アップの理由の状態の表示にするは、ネットワーク アダプターで受信したパケットを保存できる必要があります。 ドライバーは、受信パケット内の状態を示す値を返す必要があります。

 

WOL パターンを使用して指定、 **EnabledWoLPacketPatterns**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

<a href="" id="media-specific-wake-up-events"></a>メディアに固有のウェイク アップ イベント  
ネットワーク アダプターでは、802.11 アクセス ポイント (AP) またはモバイル ブロード バンド (MB) のショート メッセージ サービス (SMS) メッセージの受信から関連付け解除など、メディア固有の理由のため、ウェイク アップ イベントが生成されます。

この種類のウェイク アップのイベントがで指定された、 **MediaSpecificWakeUpEvents**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

<a href="" id="media-independent-wake-up-events"></a>メディアに依存しないウェイク アップ イベント  
ネットワーク アダプターでは、メディア接続または切断などのメディアに依存しない理由のため、ウェイク アップ イベントが生成されます。

この種類のウェイク アップのイベントがで指定された、 **WakeUpFlags**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

NDIS wake 理由状態インジケーターのミニポート ドライバーは次のガイドラインに従います。

-   ミニポート ドライバーでは、ウェイク アップ パケットがないを発行する機能をサポートする場合は、NDIS ドライバーを呼び出すときにこの機能を報告する必要があります[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。 詳細については、[Reporting Wake 理由の状態を示す値機能](reporting-wake-reason-status-indication-capabilities.md)を参照してください。

    **注**  ミニポート ドライバーは WOL パケットの受信に関連していないイベントの状態インジケーターの NDIS ウェイク アップの理由を発行するには、その機能を報告する必要はありません。

     

-   ミニポート ドライバーが WOL パケット、ウェイク アップ パケットを示す値を発行すると、ウェイク アップ イベントの原因となったパケット含める必要があります。 詳細については、[発行 NDIS Wake 理由状態インジケーター](issuing-ndis-wake-reason-indications.md)を参照してください。

-   ネットワーク アダプターにウェイク アップの信号が生成された場合、ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態示します。 それがの OID のセット要求を処理中にこのドライバーは[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)の電力状態に遷移します。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態を示す値を状態を示す値を発行する前にウェイク アップ イベントに関連します。 たとえば、メディア接続の状態の変更されたため、ウェイク アップ イベントであった場合、ミニポート ドライバー発行する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391)発行済みの状態を示す値、 **NDIS\_状態\_PM\_WAKE\_理由**状態を示す値。

-   ミニポート ドライバー ssue する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)のみが、電源管理イベントの状態の表示以前の OID セット要求を有効になっている[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)します。

-   ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)のみ生成されたウェイク アップ イベントの状態の表示基になるネットワーク アダプター。

 

 





