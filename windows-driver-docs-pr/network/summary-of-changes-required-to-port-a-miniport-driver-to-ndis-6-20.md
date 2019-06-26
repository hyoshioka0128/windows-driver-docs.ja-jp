---
title: NDIS 6.20 が動作するためのミニポート ドライバーのポートへの変更の概要
description: ミニポート ドライバーを NDIS 6.20 に移植するために必要な変更の概要
ms.assetid: e52137ac-5333-4b62-8e26-686196d8ca78
keywords:
- NDIS 6.20 WDK、ミニポート ドライバーの移植
- ミニポート ドライバーには、NDIS 6.20 WDK の移植
- ミニポート ドライバー WDK
- ミニポート ドライバー WDK、NDIS 6.20 が動作への移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72e2de480ac47b9f92730bbee2b4655a9fe600fc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360758"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-620"></a>ミニポート ドライバーを NDIS 6.20 に移植するために必要な変更の概要





このトピックでは、NDIS 6.20 が動作する NDIS 6.x ミニポート ドライバーを移植するために必要な変更をまとめたものです。

NDIS 6.20 が動作は、以前のバージョンの NDIS との下位互換性を保持します。 旧バージョンと互換性の詳細については、次を参照してください。 [NDIS 6.20 が動作の下位互換性](ndis-6-20-backward-compatibility.md)します。

NDIS 6.20 が動作環境をサポートするために、ミニポート ドライバーを更新するには、ように NDIS 6.x のミニポート ドライバーを変更する必要があります。

<a href="" id="build-environment"></a>**環境を構築します。**  
NDIS60 プリプロセッサの定義を置き換えます\_ミニポート\_ドライバーまたは NDIS61\_ミニポート\_NDIS620 ドライバー\_ミニポート\_ドライバー。

<a href="" id="general-porting-requirements"></a>**移植の一般的な要件**  
-   NDIS 6.20 バージョンでは、古い形式のインターフェイスを置き換えます。 古い形式のインターフェイスの詳細については、次を参照してください。 [NDIS 6.20 で古いインターフェイス](obsolete-interfaces-in-ndis-6-20.md)します。

-   64 を超えるプロセッサをサポートするために、次のインターフェイスを更新します。

    -   受信側 scaling (RSS)
    -   プロセッサ情報デバイス ドライバー インターフェイス
    -   リソース割り当て
    -   読み取り/書き込みロック

    64 を超えるプロセッサのサポートに関する詳細については、次を参照してください。 [NDIS 6.20 で 64 を超えるプロセッサのサポート](support-for-more-than-64-processors-in-ndis-6-20.md)します。

<a href="" id="driver-initialization"></a>**ドライバーの初期化**  
-   NDIS バージョンで 6.20 が動作を設定、 **MajorNdisVersion**と**MinorNdisVersion**のメンバー、 [ **NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)に渡される構造体、 [ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)関数。

-   ミニポート ドライバーのバージョンを設定、 **MajorDriverVersion**と**MinorDriverVersion**の NDIS メンバー\_ミニポート\_ドライバー\_特性適切なドライバー固有の値構造体。

-   NDIS の直接の OID 要求エントリ ポイントを定義\_ミニポート\_ドライバー\_特性構造体。 直接の OID 要求インターフェイスのサポートが NDIS 6.1 ドライバーでは省略可能が、ドライバーの NDIS 6.20 が動作するために必須です。 ミニポート ドライバー直接 OID 要求インターフェイスの詳細については、次を参照してください。[ミニポート アダプター OID 要求](miniport-adapter-oid-requests.md)します。

<a href="" id="miniport-adapter-initialization"></a>**ミニポート アダプタの初期化**  
-   ミニポート アダプタの機能の提供情報インターフェイスの最新バージョンを使用します。 次のインターフェイスには、機能が更新されます。
    -   電源管理
    -   受信側 scaling (RSS)
    -   ハードウェア支援 (VMQ)
-   これらの構造の更新バージョンを使用します。

    -   [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)
    -   [**NDIS\_再起動\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_general_attributes)
    -   [**NDIS\_受信\_スケール\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
    -   [**NDIS\_ミニポート\_アダプター\_ハードウェア\_支援\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

    NDIS 構造のバージョン情報については、次を参照してください。 [NDIS バージョン情報を指定する](specifying-ndis-version-information.md)します。

<a href="" id="send-and-receive-code-paths"></a>**コード パスの送受信**  
-   NDIS 6.20 ドライバーは、受信側をサポートする必要があります (RST) をスロットル処理では割り込みを受信します。 *ReceiveThrottleParameters*のパラメーター、 [ *MiniportInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_interrupt_dpc)と[ *MiniportMessageInterruptDPC* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_message_interrupt_dpc) DPC ハンドラー関数を指す、 [ **NDIS\_受信\_スロットル\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_throttle_parameters)構造体。 エントリを遅延プロシージャ呼び出し (DPC) ハンドラー、 **MaxNblsToIndicate** NDIS のメンバー\_受信\_スロットル\_の最大数を指定するパラメーター構造体[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)ミニポート ドライバーを指定する必要があります、DPC 構造。 RST の詳細については、次を参照してください。[受信側スロットル NDIS 6.20](receive-side-throttle-in-ndis-6-20.md)します。

-   更新バージョンを使用して、 [ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。

-   必要に応じて、仮想マシン キュー (VMQ) インターフェイスをサポートします。 VMQ の詳細については、次を参照してください。 [NDIS 6.20 で仮想マシン キュー (VMQ)](virtual-machine-queue--vmq--in-ndis-6-20.md)します。

 

 





