---
title: NDK 機能の有効化と無効化
description: NDK 機能を有効または無効にするために、NDIS は OID_NDK_SET_STATE OID 要求を発行します。 NDK 対応のミニポートドライバーは、この OID のサポートを MiniportOidRequest 関数に登録する必要があります。
ms.assetid: A72AD98E-FF84-48FF-B627-5534231244B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db6915b5d8aa8d3fc41db792b3e2e1277d94d2b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838123"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>NDK 機能の有効化と無効化


NDK 機能を有効または無効にするために、NDIS は\_状態 oid 要求の[oid\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)します。 NDK 対応のミニポートドライバーは、この OID のサポートを[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)関数に登録する必要があります。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>NDK 機能を有効にするかどうかを判断する


**\*NetworkDirect**キーワードは、ミニポートドライバーの NDK 機能を有効にできるかどうかを決定します。

このキーワード値が 1 ("Enabled") に設定されている場合、NDK 機能を有効にすることができます。

0 ("Disabled") に設定されている場合、NDK 機能を有効にすることはできません。

ミニポートドライバーがインストールされると、その INF ファイルでは、このキーワードの値が既定で 1 ("有効") に設定されます。 詳細については、「 [NDKPI の INF 要件](inf-requirements-for-ndkpi.md)」を参照してください。

ミニポートドライバーをインストールした後で、管理者はアダプターの **[詳細**設定] プロパティページで新しい値を設定することによって、 **\*の NetworkDirect**キーワード値を更新できます。 詳細プロパティの詳細については、「 [[詳細プロパティ] ページの構成パラメーターの指定](specifying-configuration-parameters-for-the-advanced-properties-page.md)」を参照してください。

アダプターの **[詳細設定**] プロパティページで変更が行われた後に、ミニポートドライバーが自動的に再起動  **ことに注意**してください。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>NDK 機能を有効または無効にする場合


この状態の変更は、 [oid\_NDK\_設定\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)oid 要求、またはアダプター自体の成功または失敗によってトリガーできます。

## <a name="enabling-or-disabling-ndk-functionality"></a>NDK 機能の有効化または無効化


NDK 機能を有効または無効にするには、ミニポートドライバーが NDIS に**NetEventNDKEnable**または**NetEventNDKDisable**プラグアンドプレイ (PnP) イベントを送信する必要があります。

PnP イベントを送信するために、ミニポートドライバー[**は NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)関数を呼び出し、 *NetPnPEvent*パラメーターを指定して、 [**NET\_PnP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)構造体の**NetPnPEvent**メンバーを設定します。次のようにを指します。

-   NDK 機能が有効になっている場合は**NetEventNDKEnable** 。

-   NDK 機能を無効にする場合は**NetEventNDKDisable** 。

**NetEventNDKDisable** PnP イベントは、ndk 機能が無効になっているアダプタ上で、開かれた[**ndk\_アダプタ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)インスタンスを終了するために、NDIS および上位レイヤードライバをトリガーします。 PnP イベントは、アダプターを介して開かれたすべての**NDK\_アダプター**インスタンスが閉じられるまで、保留中のままになります。

## <a name="related-topics"></a>関連トピック


[ネットワークダイレクトカーネルプロバイダーインターフェイス (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






