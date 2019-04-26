---
title: NDIS 6.82 の概要
description: このセクションでは、NDIS 6.82 を紹介し、NDIS 6.81 からの変更について説明します。 Windows 10、バージョンは 1809 NDIS 6.82 が含まれます。
ms.assetid: 6BB75BC5-0E49-4467-B030-E0A23D0ED2DA
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 90e7a6a86cd5af9a5d486c9df176c24503859bde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343658"
---
# <a name="introduction-to-ndis-682"></a>NDIS 6.82 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.82 を示し、その主要な設計の追加機能を説明します。 NDIS 6.82 は、Windows 10、バージョンは 1809 および Windows Server 2016 に含まれる以降です。

NDIS 6.82 は、NDIS 6.81 にマイナー バージョン更新です。 NDIS 6.82 する NDIS 6.x ドライバーの移植の詳細については、次を参照してください。 [NDIS 6.82 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-82.md)します。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.82 NDIS 6.81 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-682-driver"></a>NDIS 6.82、ドライバーを実装します。

NDIS 6.82、ドライバーがで定義されている要件に従う必要があります[、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.82 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.82 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.82 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーは 82 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.82 ドライバー](#compiling-an-ndis-682-driver))。

- Windows 10、バージョンは 1809 および Windows Server 2016 以降の NDIS 6.82 ミニポート ドライバーでは、データ構造の NDIS 6.82 バージョンを使用する必要があります。

## <a name="compiling-an-ndis-682-driver"></a>コンパイル、NDIS 6.82 ドライバー

Windows 10 の WDK バージョンは 1809 では、ヘッダー バージョン管理をサポートしています。 ヘッダー バージョン管理は、NDIS 6.82 ドライバーがコンパイル時に適切な NDIS 6.82 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加`NDIS682_MINIPORT=1`します。
- フィルターまたはプロトコルのドライバーを追加`NDIS682=1`します。

Windows 10 で、WDK のバージョンは 1809 リリースのドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。
