---
title: NDIS ウェイク理由状態表示の発行
description: NDIS ウェイク理由状態表示の発行
ms.assetid: F3DBE0DB-9787-4C3D-8DE3-AD47E5778B21
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ea8b9e3526a346cafafe919b52ef7e739761ecf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581425"
---
# <a name="issuing-ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示の発行


ミニポート ドライバーが NDIS ウェイク理由状態インジケーターをサポートしているかどうか ([**NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808))、これを生成する必要があります電力状態にウェイク アップ イベントと、アダプターにネットワーク アダプターが生成した直後に状態を示す値を再開します。

**注**サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

オブジェクト識別子 (OID) セット要求を電源管理 (PM) パラメーターを持つ、ミニポート ドライバーが構成されている[OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)します。 この OID 要求を通じて PM パラメーターを指定する、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

[ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造がウェイク アップのイベントの種類は次のパラメーターを指定します。

<a href="" id="received-packet-wake-up-events"></a>受信パケットのウェイク アップ イベント  
ネットワーク アダプターでは、wake on LAN (WOL) のパターンに一致するパケットを受信した場合、ウェイク アップ イベントが生成されます。 WOL パターンを以下に示します。

-   マジック パケットや TCP/IP パケット ペイロード内のデータのパターンなどのメディアに依存しない WOL パターン。 たとえば、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体の TCP SYN フレーム WOL パターンを指定できます。

-   EAPOL 要求識別子パケットやモバイル ブロード バンド (MB) のショート メッセージ サービス (SMS) メッセージなどのメディア固有 WOL パターン。

-   OID セットの要求で指定された受信フィルターと一致するワイルドカード パターン[OID\_GEN\_現在\_パケット\_フィルター](https://msdn.microsoft.com/library/windows/hardware/ff569575)します。

**注**この種類のウェイク アップの理由の状態の表示にするは、ネットワーク アダプターで受信したパケットを保存できる必要があります。 ドライバーは、受信パケット内の状態を示す値を返す必要があります。

WOL パターンを使用して指定、 **EnabledWoLPacketPatterns**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

<a href="" id="media-specific-wake-up-events"></a>メディアに固有のウェイク アップ イベント  
ネットワーク アダプターでは、802.11 アクセス ポイント (AP) またはモバイル ブロード バンド (MB) のショート メッセージ サービス (SMS) メッセージの受信から関連付け解除など、メディア固有の理由のため、ウェイク アップ イベントが生成されます。

この種類のウェイク アップのイベントがで指定された、 **MediaSpecificWakeUpEvents**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

<a href="" id="media-independent-wake-up-events"></a>メディアに依存しないウェイク アップ イベント  
ネットワーク アダプターでは、メディア接続または切断などのメディアに依存しない理由のため、ウェイク アップ イベントが生成されます。

この種類のウェイク アップのイベントがで指定された、 **WakeUpFlags**のメンバー、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

ネットワーク アダプターにウェイク アップの信号が生成された場合、ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態示します。 それがの OID のセット要求を処理中にこのドライバーは[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)電力状態にアダプターを移行します。

**注**ミニポート ドライバーを発行する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態を示す値を発行する前に、ウェイク アップ イベントに関連する状態を示します。 たとえば、メディア接続の状態の変更されたため、ウェイク アップ イベントであった場合、ミニポート ドライバー発行する必要があります、 [ **NDIS\_状態\_リンク\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff567391)発行済みの状態を示す値、 **NDIS\_状態\_PM\_WAKE\_理由**状態を示す値。

ミニポート ドライバーを発行したとき、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態を示す値、次の手順に従う必要があります。

1.  ミニポート ドライバーでは、以下を格納するのに十分な大きさであるバッファーを割り当てる必要があります。

    -   [ **NDIS\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh451605)構造体。

    -   [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)と共に受信パケットの構造 (*パケットの wake*)、ネットワークの原因となったウェイク アップのイベントを生成するアダプター。

        **注**ミニポート ドライバーがメディア固有またはメディアに依存しないウェイク アップのイベントが示されている場合は、このバッファー領域を割り当てる必要はありません。

2.  ミニポート ドライバーを初期化します、 [ **NDIS\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh451605)バッファーの先頭にある構造体。 ドライバーのセット、 **WakeReason**にメンバーを[ **NDIS\_PM\_WAKE\_理由\_型**](https://msdn.microsoft.com/library/windows/hardware/hh451607)列挙型ウェイク アップ イベントの種類を定義する値。

    たとえば、ミニポート ドライバーは、受信パケットのウェイク アップ イベントを示すは場合、設定があります、 **WakeReason**メンバー **NdisWakeReasonPacket**します。 それ以外の場合、ドライバーの設定、 **WakeReason**を最適なメディア固有またはメディアに依存しないウェイク アップ イベントを説明する列挙値のメンバー。

3.  Miniportdriver 発行している場合、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)受信パケットのウェイク アップ イベント、状態を示す値が次の手順に従います。

    1.  ミニポート ドライバーのセット、 **InfoBufferOffset**のオフセットにメンバーを[ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)構造体後の[ **NDIS\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh451605)バッファー内の構造体。

        **注**ミニポート ドライバーの開始を配置する必要があります、 [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603) 64 ビットの境界で構造体。

    2.  ミニポート ドライバーのセット、 **InfoBufferSize**メンバーのサイズを[ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)プラス構造体ウェイク アップ イベントが発生したパケットのサイズ。

    3.  ミニポート ドライバーを初期化します、 [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)構造次、 [ **NDIS\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh451605)バッファー内の構造体。

        ミニポート ドライバーがのメンバーを設定、 [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)次のように構造体します。

        -   **PatternId**メンバー ウェイク アップ パケットに一致する WOL パターンの識別子に設定されます。 この識別子が指定された、 **PatternId**のメンバー、 [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)渡される構造体OID の中にドライバーへの要求の設定[OID\_PM\_追加\_WOL\_パターン](https://msdn.microsoft.com/library/windows/hardware/ff569764)します。

        -   **PatternFriendlyName**で指定されたウェイク パターンのユーザーが判読できる説明にメンバーが設定されている、 **PatternId**メンバー。 この値を指定して、 **FriendlyName**のメンバー、 [ **NDIS\_PM\_WOL\_パターン**](https://msdn.microsoft.com/library/windows/hardware/ff566768)構造体。

            **注**ミニポート ドライバーはこのメンバーを初期化する必要はありません。 NDIS セット、 **PatternFriendlyName**を渡す前に、正しい値へのメンバー、 [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)ドライバーに関連する構造体。

        -   **OriginalPacketSize**メンバーは、ネットワーク アダプターで受信されたパケットの長さに設定されます。

        -   **SavedPacketSize**を通じて報告されるパケットの長さにメンバーを設定する必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)状態を示す値。

            **注**このメンバーの値がミニポート ドライバーに設定した値より大きくはできません、 **MaxWoLPacketSaveBuffer**のメンバー、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。 ドライバーは、ウェイク アップ パケットを示す値機能を報告する場合に、この構造体を返します。 詳細については、次を参照してください。 [Reporting Wake 理由の状態を示す値機能](reporting-wake-reason-status-indication-capabilities.md)します。

        -   **SavedPacketOffset**に続くウェイク アップ パケットをバイト単位のオフセットにメンバーを設定する必要があります、 [ **NDIS\_PM\_WAKE\_パケット**](https://msdn.microsoft.com/library/windows/hardware/hh451603)構造体。

            **注**ミニポート ドライバーは、バッファー内の 64 ビット境界のウェイク アップ パケットの開始を配置する必要があります。

    4.  ミニポートで指定されたオフセットからバッファーにウェイク アップ パケットをコピーする、 **SavedPacketOffset**メンバー。

4.  ミニポート ドライバーを発行する場合、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)メディア固有の状態を示す値、またはメディアに依存しないウェイク アップ イベント、設定、 **InfoBufferOffset**と**InfoBufferSize**のメンバー、 [ **NDIS\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh451605)構造体をゼロにします。

5.  ミニポート ドライバーを初期化します、 [ **NDIS\_状態\_INDICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体。 ドライバーのセット、 **StatusCode** NDIS メンバー\_状態\_PM\_WAKE\_理由。 ドライバーも設定、 **StatusBuffer**バッファー、およびセットを指すメンバー、 **StatusBufferLength**バッファーの長さ、(バイト単位)。

6.  ミニポート ドライバー呼び出し[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)へのポインターを渡すと、 [ **NDIS\_状態\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373)構造体、 *StatusIndication*パラメーター。

**注**ミニポート ドライバーの問題の後、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)を受信した状態の表示パケットのウェイク アップのイベントを呼び出すことによってこの受信パケットを示すその必要があります[ **NdisMIndicateReceiveNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff563598)します。