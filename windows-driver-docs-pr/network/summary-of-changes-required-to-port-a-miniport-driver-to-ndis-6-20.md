---
title: ミニポートドライバーを NDIS 6.20 に移植するための変更の概要
description: ミニポート ドライバーを NDIS 6.20 に移植するために必要な変更の概要
ms.assetid: e52137ac-5333-4b62-8e26-686196d8ca78
keywords:
- NDIS 6.20 WDK、移植ミニポートドライバー
- ミニポートドライバーを NDIS 6.20 WDK に移植する
- ミニポートドライバー WDK
- ミニポートドライバー WDK、NDIS 6.20 への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c53b88f0889702b0b41f22cf0f205e77cac098a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841810"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>ミニポート ドライバーを NDIS 6.20 に移植するために必要な変更の概要





このトピックでは、NDIS 6. x ミニポートドライバーを NDIS 6.20 に移植するために必要な変更について説明します。

NDIS 6.20 では、以前のバージョンの NDIS との下位互換性が維持されます。 旧バージョンとの互換性の詳細については、「 [NDIS 6.20 の旧バージョン](ndis-6-20-backward-compatibility.md)との互換性」を参照してください。

NDIS 6.20 環境をサポートするようにミニポートドライバーを更新するには、次のように NDIS 6.x ミニポートドライバーを変更する必要があります。

<a href="" id="build-environment"></a>**ビルド環境**  
プリプロセッサ定義 NDIS60\_ミニポート\_ドライバーまたは NDIS61\_ミニポート\_ドライバーを NDIS620\_ミニポート\_ドライバーに置き換えます。

<a href="" id="general-porting-requirements"></a>**一般的な移植の要件**  
-   旧式のインターフェイスを NDIS 6.20 バージョンに置き換えます。 互換性のために残されているインターフェイスの詳細については、「 [NDIS 6.20 の古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)」を参照してください。

-   64を超えるプロセッサをサポートするように、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイスドライバーインターフェイス
    -   リソース割り当て
    -   読み取りと書き込みのロック

    64を超えるプロセッサをサポートする方法の詳細については、「 [NDIS 6.20 で64を超えるプロセッサをサポートする](support-for-more-than-64-processors-in-ndis-6-20.md)」を参照してください。

<a href="" id="driver-initialization"></a>**ドライバーの初期化**  
-   Ndis [ **\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造の**MajorNdisVersion**および**MinorNdisVersion**メンバーで、ndis のバージョンを6.20 に設定します。これは NdisMRegisterMiniportDriver に渡されます。 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) 関数。

-   NDIS\_ミニポート\_ドライバー\_特性の構造にあるミニポートドライバー**のバージョンを**、適切なドライバー固有の値に**設定します**。

-   NDIS\_ミニポート\_ドライバー\_特性の構造で、直接 OID 要求のエントリポイントを定義します。 NDIS 6.1 ドライバーでは、直接 OID 要求インターフェイスのサポートは省略可能でしたが、NDIS 6.20 ドライバーでは必須です。 ミニポートドライバーの直接 OID 要求インターフェイスの詳細については、「[ミニポートアダプター OID 要求](miniport-adapter-oid-requests.md)」を参照してください。

<a href="" id="miniport-adapter-initialization"></a>**ミニポートアダプターの初期化**  
-   最新バージョンのミニポートアダプター機能の提供情報インターフェイスを使用します。 次のインターフェイスの機能が更新されました。
    -   電源管理
    -   受信側 scaling (RSS)
    -   ハードウェアアシスト (VMQ)
-   次の構造の更新されたバージョンを使用します。

    -   [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
    -   [**NDIS\_\_全般\_属性の再起動**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)
    -   [**NDIS\_受信\_スケール\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
    -   [**NDIS\_ミニポート\_アダプター\_ハードウェア\_サポート\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

    NDIS 構造のバージョン情報については、「 [Ndis バージョン情報の指定](specifying-ndis-version-information.md)」を参照してください。

<a href="" id="send-and-receive-code-paths"></a>**コードパスの送信と受信**  
-   NDIS 6.20 ドライバーは、受信割り込みを処理するときに、受信側スロットル (RST) をサポートする必要があります。 [*MiniportInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_interrupt_dpc)および[*MiniportMessageInterruptDPC*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_message_interrupt_dpc) DPC ハンドラー関数の*ReceiveThrottleParameters*パラメーターは、 [**NDIS\_受信\_スロットル\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_receive_throttle_parameters)構造体を指します。 遅延プロシージャ呼び出し (DPC) ハンドラーに入る**とき、Maxnblstoindicate** 、NDIS\_RECEIVE\_スロットル\_PARAMETERS 構造体のメンバーに、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)の最大数を指定します。ミニポートドライバーが DPC で示す必要のある構造体。 RST の詳細については、「 [NDIS 6.20 でのサイドスロットルの受信](receive-side-throttle-in-ndis-6-20.md)」を参照してください。

-   更新されたバージョンの[**NET\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造体を使用します。

-   必要に応じて、バーチャルマシンキュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、「[仮想マシンキュー (vmq) (NDIS 6.20)](virtual-machine-queue--vmq--in-ndis-6-20.md)」を参照してください。

 

 





