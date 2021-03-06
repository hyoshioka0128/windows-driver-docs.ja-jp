---
title: NDIS 6.30 で電源管理の機能強化
ms.assetid: A3B64252-DD6C-4715-8D4B-8D8176BC585B
description: コンピューターの電力消費量を削減する NDIS 6.30 電源管理の機能強化が導入されています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b9863aa0f7ca456312b134cffdd0558092180e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384713"
---
# <a name="power-management-enhancements-in-ndis-630"></a>NDIS 6.30 の電源管理の機能強化


NDIS 6.20 が動作には、電源管理の新機能とコンピューターの電力消費の削減の機能強化が含まれています。 NDIS 6.30」の説明に従って、次の機能では、NDIS 6.20 電源管理のサポートを拡張し[電源管理 (NDIS 6.30)](power-management--ndis-6-30-.md):

### <a name="ndis-packet-coalescing"></a>NDIS パケット結合

NDIS パケット結合 NDIS 6.30 以降では、ネットワーク アダプターをサポートできます。 この機能は、処理を軽減ランダム ブロードキャストまたはマルチキャスト パケットの受信のためのホスト システム上のオーバーヘッドと電力の消費量。

詳細については、次を参照してください。 [NDIS パケット結合](ndis-packet-coalescing.md)します。

### <a name="ndis-selective-suspend"></a>NDIS セレクティブ サスペンド

NDIS 6.30 以降では、選択的 NDIS 中断インターフェイスでは、アダプターを低電力状態に遷移することによって、アイドル状態のネットワーク アダプターを中断する NDIS できます。 これにより、CPU とネットワーク アダプターのオーバーヘッドが電力を減らすため、システムができます。

詳細については、次を参照してください。 [NDIS セレクティブ サスペンド](ndis-selective-suspend.md)します。

### <a name="ndis-wake-reason-status-indications"></a>NDIS ウェイク理由状態表示

NDIS 6.30 以降、ミニポート ドライバーで NDIS ウェイク アップの理由の状態を示す値を発行 ([**NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)) するNDIS とシステムのウェイク アップ イベントの理由についての上にあるドライバーに通知します。 ネットワーク アダプターでは、ウェイク アップのイベントを生成する場合、ミニポート ドライバーはシステムの電力状態に再開時この NDIS 状態を示す値を発行するすぐにします。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

詳細については、次を参照してください。 [NDIS Wake 理由状態インジケーター](ndis-wake-reason-status-indications.md)します。

### <a name="ndis-no-pause-on-suspend"></a>一時停止オンが中断しない NDIS

NDIS 6.30 以降、ミニポート ドライバーは、属性のフラグを指定できます (**NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**) で[ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造体。 ドライバーがその呼び出しでこの構造体へのポインターを渡します、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。

ミニポートが設定されている場合、 **NDIS\_ミニポート\_属性\_いいえ\_一時停止\_ON\_SUSPEND**属性フラグ、NDIS はミニポート呼び出しませんドライバーの[ *MiniportPause* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_pause)関数のオブジェクト識別子 (OID) を要求する前に[OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)ドライバーに発行します。 ミニポート ドライバーでは、OID 要求を処理するときにそれが以前一時停止されたことを低電力状態に遷移のミニポート アダプターを準備するときに、必要がありますわけです。

詳細については、次を参照してください。 [ **NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)します。

 

 





