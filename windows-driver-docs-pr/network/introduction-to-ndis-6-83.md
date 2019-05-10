---
title: NDIS 6.83 の概要
description: このセクションでは、NDIS 6.83 を紹介し、NDIS 6.82 からの変更について説明します。 Windows 10、バージョンが 1903 NDIS 6.83 が含まれます。
ms.assetid: FC90E212-6ED6-432C-8729-5239EF5FDD65
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2792f730eef616478b0d8d04cac21be9220c6162
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65135257"
---
# <a name="introduction-to-ndis-683"></a>NDIS 6.83 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.83 を示し、その主要な設計の追加機能を説明します。 NDIS 6.83 は、Windows 10、バージョンが 1903 および Windows Server 2016 に含まれる以降です。

NDIS 6.83 は、NDIS 6.82 にマイナー バージョン更新です。 NDIS 6.83 する NDIS 6.x ドライバーの移植の詳細については、次を参照してください。 [NDIS 6.83 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-83.md)します。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.83 NDIS 6.82 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-683-driver"></a>NDIS 6.83、ドライバーを実装します。

NDIS 6.83、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.83 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.83 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.83 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバー 83 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.83 ドライバー](#compiling-an-ndis-683-driver))。

- Windows 10、バージョンが 1903 および Windows Server 2016 以降の NDIS 6.83 ミニポート ドライバーでは、データ構造の NDIS 6.83 バージョンを使用する必要があります。

## <a name="compiling-an-ndis-683-driver"></a>コンパイル、NDIS 6.83 ドライバー

Windows 10 の WDK バージョン 1903 は、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.83 ドライバーがコンパイル時に適切な NDIS 6.83 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加`NDIS683_MINIPORT=1`します。
- フィルターまたはプロトコルのドライバーを追加`NDIS683=1`します。

Windows 10 で、WDK のバージョンが 1903 リリースのドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。