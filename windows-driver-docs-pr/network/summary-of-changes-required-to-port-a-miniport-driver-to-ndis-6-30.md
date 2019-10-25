---
title: ミニポートドライバーを NDIS 6.30 に移植するための変更の概要
description: Ndis 6. x ミニポートドライバーを更新して NDIS 6.30 をサポートするには、次のセクションで説明されているように変更する必要があります。
ms.assetid: 1EA926FE-367E-4A63-A197-60137D679AE6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 304d5da1a2fbaa9601b9230512fc541321c8bb96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841808"
---
# <a name="summary-of-changes-required-to-port-a-miniport-driver-to-ndis-630"></a>ミニポート ドライバーを NDIS 6.30 に移植するために必要な変更の概要


Ndis 6. x ミニポートドライバーを更新して NDIS 6.30 をサポートするには、次のセクションで説明されているように変更する必要があります。

-   [ビルド環境とテスト](#build-environment-and-testing)
-   [一般的な移植の要件](#general-porting-requirements)
-   [Wi-fi ダイレクトミニポートドライバー](#wi-fi-direct-miniport-drivers)
-   [USB ベースの WWAN (モバイルブロードバンド) ミニポートドライバー](#usb-based-wwan-mobile-broadband-miniport-drivers)

NDIS 6.30 の機能の詳細については、「 [ndis 6.30 の概要](introduction-to-ndis-6-30.md)」を参照してください。

## <a name="build-environment-and-testing"></a>ビルド環境とテスト


-   プリプロセッサ定義 NDIS60\_ミニポートまたは NDIS61\_ミニポートまたは NDIS620\_ミニポートを NDIS630\_ミニポートに置き換えます。 詳細については、「 [NDIS 6.30 ドライバーのコンパイル](compiling-an-ndis-6-30-driver.md)」を参照してください。
-   プリプロセッサ定義 NDIS60 または NDIS61 または NDIS620 (存在する場合) を NDIS630 に置き換えます。
    この項目は、NDIS 中間、プロトコル、およびフィルタードライバーにのみ適用さ  に**注意**してください。 ほとんどの NDIS ミニポートドライバーは、このプリプロセッサ定義を必要としません。

     

-   NDIS 6.30 では、2つのアダプターが同時にシステムに接続されている場合、またはシステムの起動時に2つのアダプターが同時に[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)を呼び出すことができます。 ミニポートドライバーは、この "並列スタートアップ" 条件で必ずテストしてください。

## <a name="general-porting-requirements"></a>一般的な移植の要件


-   「Ndis [6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で説明されているように、Ndis\_*Xxx*\_ドライバー\_特性の構造に含まれるメジャーおよびマイナーバージョン番号を更新します。
-   NDIS 6.30 用に更新されたすべての構造体について、ミニポートドライバーは、正しい**リビジョン**と**サイズ**の値を使用して、構造体の**ヘッダー**メンバーを更新する必要があります。 詳細については、「 [NDIS 6.30 データ構造体の使用](using-ndis-6-30-data-structures.md)」を参照してください。
-   すべてのミニポートドライバーは、一時停止なしの機能を実装する必要があります。 詳しくは、次のトピックをご覧ください。
    -   [NDIS 6.30 の電源管理の機能強化](power-management-enhancements-in-ndis-6-30.md)
    -   [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)
    -   [**NET\_PNP\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event)
    -   [OID\_PNP\_設定\_電源](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)

## <a name="wi-fi-direct-miniport-drivers"></a>Wi-fi ダイレクトミニポートドライバー


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)中、wi-fi Direct 対応ミニポートドライバーは、既定の 802.11 MAC エンティティを初期化する必要があります。 また、 [**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)機能を使用して wi-fi ダイレクトおよび仮想 wi-fi 機能を報告する必要があります。

既定の MAC エンティティに対応する NDIS ポートを NDIS に登録するためにドライバーが必要ない  に**注意**してください。

 

## <a name="usb-based-wwan-mobile-broadband-miniport-drivers"></a>USB ベースの WWAN (モバイルブロードバンド) ミニポートドライバー


USB ベースのモバイルブロードバンドデバイスの場合、Windows 8 には、MBIM 仕様に準拠したデバイスで動作するクラスドライバーが用意されています。 このモデルは、モバイルブロードバンド (MB) クラスドライバーと呼ばれています。 ただし、クラスドライバーは、MB デバイスによって公開されているすべての機能をサポートすることはできません。 このため、MB 機能には、クラスドライバーの機能を拡張するために使用できる、明確に定義されたメカニズムが用意されています。 詳細については、「 [MB デバイスサービス](mb-device-services.md)」を参照してください。

USB ベースの WWAN ミニポートドライバーが MB クラスドライバーを実装できない場合は、少なくとも[NDIS セレクティブサスペンド](ndis-selective-suspend.md)機能を実装する必要があります。

 

 





