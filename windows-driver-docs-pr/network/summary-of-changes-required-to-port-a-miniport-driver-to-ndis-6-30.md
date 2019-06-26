---
title: NDIS 6.30 に、ミニポート ドライバーのポートへの変更の概要
description: NDIS 6.30 をサポートするためには、NDIS 6.x ミニポート ドライバーを更新するには、次のセクションで説明したよう変更する必要があります。
ms.assetid: 1EA926FE-367E-4A63-A197-60137D679AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c022e0e9cefd2e635a7f8e0a531afaf38ad28e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377986"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-630"></a>ミニポート ドライバーを NDIS 6.30 に移植するために必要な変更の概要


NDIS 6.30 をサポートするためには、NDIS 6.x ミニポート ドライバーを更新するには、次のセクションで説明したよう変更する必要があります。

-   [ビルド環境およびテスト](#build-environment-and-testing)
-   [移植の一般的な要件](#general-porting-requirements)
-   [Wi-Fi Direct ミニポート ドライバー](#wi-fi-direct-miniport-drivers)
-   [ミニポート ドライバーを USB ベース WWAN (モバイル ブロード バンド)](#usb-based-wwan-mobile-broadband-miniport-drivers)

NDIS 6.30 機能の詳細については、次を参照してください。 [NDIS 6.30 概要](introduction-to-ndis-6-30.md)します。

## <a name="build-environment-and-testing"></a>ビルド環境およびテスト


-   NDIS60 プリプロセッサの定義を置き換えます\_ミニポートまたは NDIS61\_ミニポートまたは NDIS620\_NDIS630 にミニポート\_ミニポートします。 詳細については、次を参照してください[NDIS 6.30 ドライバーのコンパイル。](compiling-an-ndis-6-30-driver.md)
-   NDIS630 で存在する場合、NDIS60 または NDIS61 NDIS620、プリプロセッサの定義を置き換えます。
    **注**  NDIS 中間、プロトコル、およびフィルター ドライバーにのみ、この項目が適用されます。 ほとんどの NDIS ミニポート ドライバーでは、このプリプロセッサの定義を必要はありません。

     

-   NDIS 6.30、NDIS を呼び出すことができます[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize) 2 回並列 2 つのアダプターがある場合は、同時にまたはシステムの起動時にシステムに接続します。 この"並列 startup"の条件下で、ミニポート ドライバーをテストすることを確認します。

## <a name="general-porting-requirements"></a>移植の一般的な要件


-   メジャーおよびマイナーの NDIS バージョン番号、NDIS で更新\_*Xxx*\_ドライバー\_特性構造」の説明に従って[NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md).
-   NDIS 6.30 の更新されたすべての構造体、ミニポート ドライバーが更新しなければ、**ヘッダー** 、適切な構造体のメンバー**リビジョン**と**サイズ**値。 詳細については、次を参照してください。 [NDIS 6.30 データ構造体を使用して](using-ndis-6-30-data-structures.md)します。
-   ミニポート ドライバーをすべていいえ-一時停止-上の中断機能を実装する必要があります。 詳しくは、次のトピックをご覧ください。
    -   [NDIS 6.30 で電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
    -   [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
    -   [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)
    -   [OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

## <a name="wi-fi-direct-miniport-drivers"></a>Wi-Fi Direct ミニポート ドライバー


中に[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)、Wi-Fi Direct 対応ミニポート ドライバーが 802.11 の既定の MAC エンティティを初期化する必要があります。 使用して、Wi-Fi Direct と仮想の Wi-fi 機能をレポートする必要がありますも、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)関数。

**注**  ドライバーが既定の MAC エンティティに対応する NDIS ポート NDIS に登録する必要はありません。

 

## <a name="usb-based-wwan-mobile-broadband-miniport-drivers"></a>ミニポート ドライバーを USB ベース WWAN (モバイル ブロード バンド)


USB ベース モバイル ブロード バンド デバイスの場合は、Windows 8 は、MBIM 仕様に準拠しているデバイスで動作するためのクラス ドライバーを提供します。 このモデルは、モバイル ブロード バンド (MB) のクラス ドライバーと呼ばれます。 ただし、クラス ドライバーでは、MB デバイスによって公開される機能のすべてをサポートできません。 このためは、MB 機能は、クラス ドライバー機能を拡張するのに使用できる明確に定義されたメカニズムを提供します。 詳細については、次を参照してください。 [MB デバイス サービス](mb-device-services.md)します。

実装する必要がありますには少なくとも、USB ベース WWAN ミニポート ドライバーでは、MB クラス ドライバーを実装できない場合、 [NDIS セレクティブ サスペンド](ndis-selective-suspend.md)機能します。

 

 





