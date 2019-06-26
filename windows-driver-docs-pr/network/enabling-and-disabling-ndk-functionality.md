---
title: NDK 機能の有効化と無効化
description: 有効または NDK 機能を無効にする場合は、NDIS は、OID_NDK_SET_STATE OID 要求を発行します。 NDK 対応のミニポート ドライバーでは、その MiniportOidRequest 関数でこの OID のサポートを登録する必要があります。
ms.assetid: A72AD98E-FF84-48FF-B627-5534231244B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56d1da6f3753cd4770e69bdc1567ff13350f7a49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378687"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>NDK 機能の有効化と無効化


NDK 機能、NDIS 問題有効または無効にする[OID\_NDK\_設定\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID 要求。 NDK 対応のミニポート ドライバーでは、この OID のサポートを登録する必要があります、 [ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)関数。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>NDK 機能を有効にするかどうかを決定します。


**\*NetworkDirect** キーワードは、ミニポート ドライバーの NDK 機能を有効にするかどうかを判断します。

このキーワードの値が 1 ("Enabled") に設定されている場合は、NDK 機能を有効にできます。

0 ("Disabled") に設定されている場合、NDK 機能を有効にすることはできません。

ミニポート ドライバーがインストールされているときに、INF ファイルは、既定では 1 ("Enabled") にこのキーワードの値を設定します。 詳細については、次を参照してください。 [NDKPI の INF 要件](inf-requirements-for-ndkpi.md)します。

管理者を更新できますミニポート ドライバーをインストールした後、  **\*NetworkDirect**キーワードの値で新しい値を設定して、 **[詳細設定]** アダプターのプロパティ ページ。 高度なプロパティの詳細については、次を参照してください。[プロパティの詳細 ページの構成パラメーターを指定する](specifying-configuration-parameters-for-the-advanced-properties-page.md)します。

**注**  ミニポート ドライバーが自動的に再起動で、変更を行った後、 **[詳細設定]** アダプターのプロパティ ページ。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>有効または NDK 機能を無効にするタイミング


この状態の変更をトリガーできます、 [OID\_NDK\_設定\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID の要求、成功またはエラー アダプター自体にします。

## <a name="enabling-or-disabling-ndk-functionality"></a>有効化または NDK 機能を無効にします。


有効または NDK 機能を無効にする、ミニポート ドライバーに送信する必要があります、 **NetEventNDKEnable**または**NetEventNDKDisable** NDIS にプラグ アンド プレイ (PnP) イベント。

PnP、イベントをミニポート ドライバーの呼び出しを送信する、 [ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)関数の場合、設定、 **NetPnPEvent**のメンバー、 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)構造体、 *NetPnPEvent*パラメーターは次の手順を指します。

-   **NetEventNDKEnable** NDK の機能が有効にする場合。

-   **NetEventNDKDisable** NDK の機能が無効にする場合。

**NetEventNDKDisable** PnP イベントは、開かれた終了を開始するには、NDIS および上位レイヤー ドライバー トリガー [ **NDK\_アダプター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)アダプター上でインスタンスNDK 機能が無効されている場所です。 PnP イベントが保留中に残りますまですべての開かれている**NDK\_アダプター**アダプター上でインスタンスが閉じられます。

## <a name="related-topics"></a>関連トピック


[ネットワーク ダイレクト カーネル プロバイダー インターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






