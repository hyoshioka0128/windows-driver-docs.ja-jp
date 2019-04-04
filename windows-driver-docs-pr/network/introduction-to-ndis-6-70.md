---
title: NDIS 6.70 の概要
description: このセクションでは、NDIS 6.70 を紹介し、NDIS 6.60 からの変更について説明します。 Windows 10 バージョン 1703 では、NDIS 6.70 が含まれます。
ms.assetid: D846EE68-2C84-40E0-91DE-2034F75D576F
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91c955a03143d8f96d7c01dc4d47090ed41cb7ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532316"
---
# <a name="introduction-to-ndis-670"></a>NDIS 6.70 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.70 を示し、その主要な設計の追加機能を説明します。 Windows 10 バージョン 1703 では、NDIS 6.70 が含まれます。

NDIS 6.70 は、NDIS 6.60 にミニポート、プロトコル、フィルター、および中間ドライバーのマイナー バージョン更新です。 NDIS 6.70 する NDIS 6.x ドライバーの移植の詳細については、[NDIS 6.70 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-70.md)を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

### <a name="netadaptercx"></a>NetAdapterCx

と共に NDIS 6.70、Windows 10 バージョン 1703 別名: ネットワーク アダプターの WDF クラス拡張と呼ばれる NIC ドライバーの主要な新機能が含まれています [NetAdapterCx](../netcx/index.md)します。 NetAdapterCx は、Windows 10 バージョン 1703 だけではプレビュー版です。 NetAdapterCx モデルにより、すべての機能と WDF の簡略化されたドライバー モデルを利用する NIC ドライバー開発者向け、NIC ドライバーの意味は簡単に記述します。

### <a name="other-feature-updates"></a>その他の機能更新プログラム

NDIS は、Windows 上のネットワーク ドライバーのプラットフォームの基盤を形成します。 NDIS 6.70 と同時に更新されたその他のネットワーク ドライバーの機能の一覧は、Windows 10 バージョン 1703 セクションで、ネットワーク接続を参照してください。[ドライバーの開発における新](../what-s-new-in-driver-development.md)します。

## <a name="feature-deprecations"></a>機能の廃止された機能

NDIS 6.70 のリリースと共に、次のネットワーク ドライバー機能が廃止されました。

- [TCP Chimney オフロード](https://docs.microsoft.com/previous-versions/windows/hardware/network/ndis-tcp-chimney-offload)
- [IPsec オフロード バージョン 2](ipsec-offload-version-2.md)

## <a name="implementing-an-ndis-670-driver"></a>NDIS 6.70、ドライバーを実装します。

### <a name="nic-drivers"></a>NIC ドライバー

NetAdapterCx NIC ドライバーの実装の詳細については、[NetAdapterCx](../netcx/index.md)を参照してください。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>ミニポート、プロトコル、フィルター、および中間ドライバー

NDIS 6.70、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.70 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.70 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。

   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.70 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーが 70 を含める必要があります。 この要件は、プロトコルとフィルター ドライバーをミニポートに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.70 ドライバー](#compiling-an-ndis-670-driver))。

## <a name="compiling-an-ndis-670-driver"></a>コンパイル、NDIS 6.70 ドライバー

### <a name="nic-drivers"></a>NIC ドライバー

コンパイル、NetAdapterCx で NIC ドライバーの詳細については、[NetAdapterCx (コンパイルの設定) に移植する NDIS ミニポート ドライバー](../netcx/porting-ndis-miniport-drivers-to-netadaptercx.md#compilation-settings)を参照してください。

### <a name="miniport-protocol-and-filter-drivers"></a>ミニポート、プロトコル、およびフィルター ドライバー

Windows 10 の WDK バージョン 1703 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.70 ドライバーがコンパイル時に適切な NDIS 6.70 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加```NDIS670_MINIPORT=1```します。
- フィルターまたはプロトコルのドライバーを追加```NDIS670=1```します。

Windows 10 バージョン 1703 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。

## <a name="using-ndis-670-driver-data-structures"></a>NDIS 6.70 ドライバーのデータ構造を使用します。

### <a name="nic-drivers"></a>NIC ドライバー

NetAdapterCx データ構造の詳細については、[NetAdapterCx](../netcx/index.md)を参照してください。

### <a name="miniport-protocol-filter-and-intermediate-drivers"></a>ミニポート、プロトコル、フィルター、および中間ドライバー

#### <a name="new-data-structures"></a>新しいデータの構造

次のデータ構造は、NDIS 6.70 の新機能。

- [NDIS_STATUS_WWAN_DEVICE_CAPS_EX](https://msdn.microsoft.com/library/windows/hardware/mt782396)

