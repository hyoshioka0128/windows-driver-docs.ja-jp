---
title: NDIS 6.30 で電源管理の機能強化
ms.assetid: A3B64252-DD6C-4715-8D4B-8D8176BC585B
description: コンピューターの電力消費量を削減する NDIS 6.30 電源管理の機能強化が導入されています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e73c806ca55185eac4c4410cedfd1e443bd65ad
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560988"
---
# <a name="power-management-enhancements-in-ndis-630"></a>NDIS 6.30 で電源管理の機能強化


NDIS 6.20 が動作には、電源管理の新機能とコンピューターの電力消費の削減の機能強化が含まれています。 NDIS 6.30」の説明に従って、次の機能では、NDIS 6.20 電源管理のサポートを拡張し[電源管理 (NDIS 6.30)](power-management--ndis-6-30-.md):

### <a name="ndis-packet-coalescing"></a>NDIS パケットの結合

NDIS パケット結合 NDIS 6.30 以降では、ネットワーク アダプターをサポートできます。 この機能は、処理を軽減ランダム ブロードキャストまたはマルチキャスト パケットの受信のためのホスト システム上のオーバーヘッドと電力の消費量。

詳細については、[NDIS パケット結合](ndis-packet-coalescing.md)を参照してください。

### <a name="ndis-selective-suspend"></a>選択的 NDIS 中断します。

NDIS 6.30 以降では、選択的 NDIS 中断インターフェイスでは、アダプターを低電力状態に遷移することによって、アイドル状態のネットワーク アダプターを中断する NDIS できます。 これにより、CPU とネットワーク アダプターのオーバーヘッドが電力を減らすため、システムができます。

詳細については、[NDIS セレクティブ サスペンド](ndis-selective-suspend.md)を参照してください。

### <a name="ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態インジケーター

NDIS 6.30 以降、ミニポート ドライバーで NDIS ウェイク アップの理由の状態を示す値を発行 ([**NDIS\_状態\_PM\_WAKE\_理由**](https://msdn.microsoft.com/library/windows/hardware/hh439808)) するNDIS とシステムのウェイク アップ イベントの理由についての上にあるドライバーに通知します。 ネットワーク アダプターでは、ウェイク アップのイベントを生成する場合、ミニポート ドライバーはシステムの電力状態に再開時この NDIS 状態を示す値を発行するすぐにします。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

詳細については、[NDIS Wake 理由状態インジケーター](ndis-wake-reason-status-indications.md)を参照してください。

### <a name="ndis-no-pause-on-suspend"></a>一時停止オンが中断しない NDIS

NDIS 6.30 以降、ミニポート ドライバーは、属性のフラグを指定できます (**NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**) で[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)構造体。 ドライバーがその呼び出しでこの構造体へのポインターを渡します、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数。

ミニポートが設定されている場合、 **NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**属性フラグ、NDIS はミニポート呼び出しませんドライバーの[ *MiniportPause* ](https://msdn.microsoft.com/library/windows/hardware/ff559418)関数のオブジェクト識別子 (OID) を要求する前に[OID\_PNP\_設定\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)ドライバーに発行します。 ミニポート ドライバーでは、OID 要求を処理するときにそれが以前一時停止されたことを低電力状態に遷移のミニポート アダプターを準備するときに、必要がありますわけです。

詳細については、[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565934)を参照してください。

 

 





