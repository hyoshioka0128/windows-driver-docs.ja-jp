---
title: NDIS 6.80 の概要
description: このセクションでは、NDIS 6.80 について説明し、NDIS 6.70 からの変更について説明します。 NDIS 6.80 は、Windows 10 version 1709 に含まれています。
ms.assetid: 5E6E12BF-DE34-4CDD-84BB-7708A59134E9
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: b107e386cea85422c146956f8d8282e942b43ac7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844165"
---
# <a name="introduction-to-ndis-680"></a>NDIS 6.80 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.80 について説明し、主な設計の追加について説明します。 NDIS 6.80 は、Windows 10 version 1709 に含まれています。

NDIS 6.80 は、ミニポート、プロトコル、フィルター、中間ドライバーの NDIS 6.70 に対するマイナーバージョンの更新です。 Ndis 6. x ドライバーを ndis 6.80 に移植する方法の詳細については、「ndis [6. x ドライバーを ndis 6.80 に移植する](porting-ndis-6-x-drivers-to-ndis-6-70.md)」を参照してください。

NIC ドライバーの場合、NetAdapter クラス拡張 (NetAdapterCx) は、Windows 10 version 1709 のバージョン1.0 からバージョン1.1 に更新されました。

## <a name="feature-updates"></a>機能更新プログラム

### <a name="synchronous-oid-requests"></a>同期 OID 要求

NDIS 6.80 では、Oid、同期 OID 要求の新機能が導入されています。 同期 OID 呼び出しは、通常の OID 要求と比較して、低待機時間、非ブロッキング、スケーラブル、および信頼性があります。 詳細については、「 [NDIS 6.80 の同期 OID 要求インターフェイス](synchronous-oid-request-interface-in-ndis-6-80.md)」を参照してください。

### <a name="rssv2"></a>RSSv2

NDIS 6.80 では、 [Receive Side Scaling (rss)](ndis-receive-side-scaling2.md)が rss バージョン 2 (RSSv2) にアップグレードされました。 RSSv2 は、VPort ごとの拡散を提供することで RSSv2 を改善します。 詳細については、「 [Receive Side Scaling Version 2 (RSSv2) IN NDIS 6.80](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md)」を参照してください。

RSSv2 は、Windows 10 バージョン1709でのみプレビュー版です。

### <a name="other-new-networking-features"></a>その他の新しいネットワーク機能

NDIS は、Windows 上のネットワークドライバープラットフォームのコア基盤となります。 NDIS 6.80 と同時に更新されたネットワークドライバーのその他の機能の一覧については、「[ドライバー開発の新](../what-s-new-in-driver-development.md)機能」のネットワークについて、Windows 10 のバージョン1709に関するセクションを参照してください。

## <a name="implementing-an-ndis-680-driver"></a>NDIS 6.80 ドライバーの実装

NDIS 6.80 ドライバーは、「 [ndis 6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で定義されている要件に従う必要があります。

また、NDIS 6.80 ドライバーは、次の要件に準拠している必要があります。

- Ndis 6.80 ドライバーは、ndis に登録するときに正しい NDIS バージョンを報告する必要があります。

   NDIS 6.80 をサポートするには、NDIS_Xxx_DRIVER_CHARACTERISTICS 構造体のメジャーおよびマイナーバージョン番号を更新する必要があります。 MajorNdisVersion メンバーには6を含める必要があり、MinorNdisVersion メンバーには80が含まれている必要があります。 この要件は、ミニポート、プロトコル、およびフィルタードライバーに適用されます。 また、コンパイラのバージョン情報も更新する必要があります (「 [NDIS 6.80 ドライバーのコンパイル](#compiling-an-ndis-680-driver)」を参照してください)。

## <a name="compiling-an-ndis-680-driver"></a>NDIS 6.80 ドライバーのコンパイル

### <a name="nic-drivers"></a>NIC ドライバー

NetAdapterCx を使用して NIC ドライバーをコンパイルする方法の詳細については、「 [NDIS ミニポートドライバーを NetAdapterCx に移植する (コンパイル設定)](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)」を参照してください。

### <a name="miniport-protocol-and-filter-drivers"></a>ミニポート、プロトコル、フィルタードライバー

Windows 10 バージョン1709の WDK は、ヘッダーのバージョン管理をサポートしています。 ヘッダーのバージョン管理により、コンパイル時に NDIS 6.80 ドライバーが適切な NDIS 6.80 データ構造を使用するようになります。

次のコンパイラ設定をドライバーの Visual Studio プロジェクトに追加します。

- ミニポートドライバーの場合は、```NDIS680_MINIPORT=1```を追加します。
- フィルターまたはプロトコルドライバーの場合は、```NDIS680=1```を追加します。

Windows 10 バージョン1709リリースの WDK を使用したドライバーの構築の詳細については、「[ドライバーのビルド](../develop/building-a-driver.md)」を参照してください。

## <a name="api-and-data-structure-changes"></a>API とデータ構造の変更

### <a name="new-apis-and-data-structures"></a>新しい Api とデータ構造

次の Api とデータ構造は、NDIS 6.80 で新しく追加されたものです。

- [MINIPORT_SYNCHRONOUS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-miniport_synchronous_oid_request)
- [FILTER_SYNCHRONOUS_OID_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request)
- [FILTER_SYNCHRONOUS_OID_REQUEST_COMPLETE](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-filter_synchronous_oid_request_complete)
- [NdisFSynchronousOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfsynchronousoidrequest)
- [NdisSynchronousOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissynchronousoidrequest)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters_v2)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entries)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_rss_set_indirection_entry)

### <a name="updated-apis-and-data-structures"></a>更新された Api とデータ構造

NDIS 6.80 では、次の Api とデータ構造が更新されました。

- [NDIS_MINIPORT_DRIVER_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)
- [NDIS_FILTER_DRIVER_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_driver_characteristics)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

