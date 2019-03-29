---
title: 電源管理パラメーターの取得と更新
description: 電源管理パラメーターの取得と更新
ms.assetid: 46c4d2ab-e6d9-4d23-bf40-0037b80b01af
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a80244107ea0a90e0c527a9e004d6c277bd0512
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573133"
---
# <a name="obtaining-and-updating-power-management-parameters"></a>電源管理パラメーターの取得と更新





プロトコル ドライバーを使用できる、 [OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768)が現在有効になっているネットワーク アダプターのハードウェア機能のクエリを実行する OID。 で、クエリから正常に戻った後、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造に含まれる、ポインター、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)構造体。

プロトコル ドライバーできます OID を使用しても\_PM\_セットの要求としてパラメーターを有効またはネットワーク アダプターの現在のハードウェア機能を無効にします。 プロトコル ドライバー、NDIS へのポインターを提供する\_PM\_パラメーター構造体、 **InformationBuffer**の NDIS メンバー\_OID\_要求の構造。

**注**  プロトコル ドライブには、その他のプロトコルのドライバーを有効にしていた機能が無効にすることはできません。 機能を有効にすると、none プロトコル ドライバーの場合はその機能は使用されません。

 

**注**  NDIS マジック パケットを使用して低電力の切断、ユーザー設定に基づいて機能とプロトコル ドライバーによって、これらの機能を無効にすることはできません。

 

NDIS\_PM\_パラメーターには、次の情報が含まれています。

<a href="" id="enabledwolpacketpatterns"></a>**EnabledWoLPacketPatterns**  
内で報告して、ミニポート ドライバー機能に対応するフラグを含む、 **SupportedWoLPacketPatterns**のメンバー、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。 たとえば、ビットマップ、WOL マジック パケットの場合、または EAP over LAN (EAPOL) 要求の識別子のメッセージを受信すると、ウェイク アップ イベントを生成するネットワーク アダプターが有効にします。 現在のオペレーティング システムで可能なパターンの完全な一覧を参照してください、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)リファレンス ページです。

<a href="" id="enabledprotocoloffloads"></a>**EnabledProtocolOffloads**  
内で報告して、ミニポート ドライバー機能に対応するフラグを含む、 **SupportedProtocolOffloads**のメンバー、 [ **NDIS\_PM\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)構造体。 NDIS は、これらのフラグを使用して有効またはネットワーク アダプターでは、低電力プロトコル オフロード機能を無効にします。 たとえば、ネットワーク アダプターは、IPv4 ARP、IPv6 近隣要請 (NS)、または信頼性の高いセキュリティで保護されたネットワーク (RSN) 4 方向と双方向のハンドシェイクが有効になっている IEEE 802.11 オフロードします。 現在のオペレーティング システムでサポートされているプロトコルのオフロードの完全な一覧を参照してください、 [ **NDIS\_PM\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff566759)リファレンス ページです。

<a href="" id="wakeupflags"></a>**WakeUpFlags**  
NDIS を使用して有効にするか、ネットワーク アダプターにウェイク アップ機能を無効にするフラグが含まれています。

NDIS 6.20 が動作する場合、NDIS の\_PM\_WAKE\_ON\_リンク\_変更\_有効フラグを使用できます (メディア接続) リンクの変更でスリープ解除する機能。 このフラグの詳細については、次を参照してください。[メディア切断の低電力](low-power-on-media-disconnect.md)します。

NDIS 6.30、NDIS 以降\_PM\_セレクティブ\_SUSPEND\_有効フラグ NDIS 選択時に基になる USB のネットワーク アダプターを中断、サポートを有効します。 詳細については、次を参照してください。 [NDIS セレクティブ サスペンド](ndis-selective-suspend.md)します。

ドライバーが設定した場合、 [OID\_PM\_パラメーター](https://msdn.microsoft.com/library/windows/hardware/ff569768) OID、NDIS で、ミニポート ドライバーに転送することがなく、要求が完了します。 NDIS は、要求された設定を格納し、このような他の要求の設定ではそれらを結合します。

NDIS 低電力状態にネットワーク アダプターへの移行前に、NDIS は NDIS が格納されている要求のすべての設定の組み合わせを含むミニポート ドライバーにセットの要求を送信します。 低電力状態を設定する方法についての詳細については、次を参照してください。 [Wake on LAN の低電力](low-power-for-wake-on-lan.md)します。

現在有効になっている機能は、ハードウェアでサポートされる機能のサブセットであることができます。 ハードウェアでサポートされる機能の詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

 

 





