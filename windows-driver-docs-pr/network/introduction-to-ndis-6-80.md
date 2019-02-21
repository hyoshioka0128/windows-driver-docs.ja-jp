---
title: NDIS 6.80 の概要
description: このセクションでは、NDIS 6.80 を紹介し、NDIS 6.70 からの変更について説明します。 Windows 10 バージョン 1709 では、NDIS 6.80 が含まれます。
ms.assetid: 5E6E12BF-DE34-4CDD-84BB-7708A59134E9
ms.date: 07/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85aa0c719bfcf42a74057d332a1c203ed8352e4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557647"
---
# <a name="introduction-to-ndis-680"></a>NDIS 6.80 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.80 を示し、その主要な設計の追加機能を説明します。 Windows 10 バージョン 1709 では、NDIS 6.80 が含まれます。

NDIS 6.80 は、NDIS 6.70 にミニポート、プロトコル、フィルター、および中間ドライバーのマイナー バージョン更新です。 NDIS 6.80 する NDIS 6.x ドライバーの移植の詳細については、次を参照してください。 [NDIS 6.80 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-70.md)します。

NIC ドライバーでは、NetAdapter クラス拡張 (NetAdapterCx) をバージョン 1.0 からバージョン 1.1 では、Windows 10 バージョン 1709 に更新されましたがします。

## <a name="feature-updates"></a>機能更新プログラム

### <a name="synchronous-oid-requests"></a>同期の OID 要求

NDIS 6.80 では、Oid の新しい機能が導入されて、同期の OID を要求します。 OID の同期呼び出しは、低待機時間、非ブロッキング、スケーラブルでと、通常の OID 要求信頼性の高い比較されます。 詳細については、次を参照してください。[同期 OID 要求インターフェイスで NDIS 6.80](synchronous-oid-request-interface-in-ndis-6-80.md)します。

### <a name="rssv2"></a>RSSv2

NDIS 6.80 で[Receive Side Scaling (RSS)](ndis-receive-side-scaling2.md) RSS バージョン 2 (RSSv2) にアップグレードされました。 RSSv2 が RSSv2 上あたり VPort の拡散を提供することで向上します。 詳細については、次を参照してください。[受信側のスケーリング バージョン 2 (RSSv2) で NDIS 6.80](receive-side-scaling-version-2-rssv2-in-ndis-6-80.md)します。

RSSv2 は、Windows 10 バージョン 1709 でのみプレビューです。

### <a name="other-new-networking-features"></a>その他の新しいネットワーク機能

NDIS は、Windows 上のネットワーク ドライバーのプラットフォームの基盤を形成します。 NDIS 6.80 と同時に更新されたその他のネットワーク ドライバーの機能の一覧は、Windows 10 バージョン 1709 のセクションで、ネットワーク接続を参照してください。[ドライバーの開発における新](../what-s-new-in-driver-development.md)します。

## <a name="implementing-an-ndis-680-driver"></a>NDIS 6.80、ドライバーを実装します。

NDIS 6.80、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.80 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.80 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.80 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーが 80 を含める必要があります。 この要件は、プロトコルとフィルター ドライバーをミニポートに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.80 ドライバー](#compiling-an-ndis-670-driver))。

## <a name="compiling-an-ndis-680-driver"></a>コンパイル、NDIS 6.80 ドライバー

### <a name="nic-drivers"></a>NIC ドライバー

コンパイル、NetAdapterCx で NIC ドライバーの詳細については、次を参照してください。 [NetAdapterCx (コンパイルの設定) に移植する NDIS ミニポート ドライバー](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)します。

### <a name="miniport-protocol-and-filter-drivers"></a>ミニポート、プロトコル、およびフィルター ドライバー

Windows 10 の WDK バージョン 1709 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.80 ドライバーがコンパイル時に適切な NDIS 6.80 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加```NDIS680_MINIPORT=1```します。
- フィルターまたはプロトコルのドライバーを追加```NDIS680=1```します。

Windows 10 バージョン 1709 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。

## <a name="api-and-data-structure-changes"></a>API とデータ構造の変更

### <a name="new-apis-and-data-structures"></a>新しい Api、データの構造

次の Api とデータの構造は、NDIS 6.80 の新機能。

- [MINIPORT_SYNCHRONOUS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/0DDF9CF8-91F6-4D7C-A8E8-FC425BF155CB)
- [FILTER_SYNCHRONOUS_OID_REQUEST](https://msdn.microsoft.com/library/windows/hardware/AC84B27B-6FBF-429D-A8FA-F3C8F583F738)
- [FILTER_SYNCHRONOUS_OID_REQUEST_COMPLETE](https://msdn.microsoft.com/library/windows/hardware/E0749F52-CC7C-484D-8350-1986154957C1)
- [NdisFSynchronousOidRequest](https://msdn.microsoft.com/library/windows/hardware/01B625EB-AB6D-496F-95F2-22845460324A)
- [NdisSynchronousOidRequest](https://msdn.microsoft.com/library/windows/hardware/BF539DDA-59ED-4010-88BC-3C7D8DC475EF)
- [OID_GEN_RECEIVE_SCALE_PARAMETERS_V2](oid-gen-receive-scale-parameters-v2.md)
- [OID_GEN_RSS_SET_INDIRECTION_TABLE_ENTRIES](oid-gen-rss-set-indirection-table-entries.md)
- [NDIS_RECEIVE_SCALE_PARAMETERS_V2](https://msdn.microsoft.com/library/windows/hardware/96EAB6EE-BF9A-46AD-8DED-5D9BD2B6F219)
- [NDIS_RSS_SET_INDIRECTION_ENTRIES](https://msdn.microsoft.com/library/windows/hardware/9AB69EC6-FE78-4242-89C7-D36AA16676BF)
- [NDIS_RSS_SET_INDIRECTION_ENTRY](https://msdn.microsoft.com/library/windows/hardware/4430E19F-C603-4C52-8FC8-C36197FD2996)

### <a name="updated-apis-and-data-structures"></a>更新された Api、データの構造

次の Api、データの構造は、NDIS 6.80 で更新されました。

- [NDIS_MINIPORT_DRIVER_CHARACTERISTICS](https://msdn.microsoft.com/library/windows/hardware/ff565958)
- [NDIS_FILTER_DRIVER_CHARACTERISTICS](https://msdn.microsoft.com/library/windows/hardware/ff565515)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)

