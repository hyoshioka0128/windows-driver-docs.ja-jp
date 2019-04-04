---
title: NDIS 6.60 の概要
description: このセクションでは、NDIS 6.60 を紹介し、NDIS 6.50 からの変更について説明します。 NDIS 6.60 は、Windows 10、バージョン 1607 および Windows Server 2016 に含まれる以降です。
ms.assetid: AFDFD1CD-2E07-4A4F-82E2-5E6C5AABD5A3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe12b73f1a4db94720a6468cf480407f2449d19d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557650"
---
# <a name="introduction-to-ndis-660"></a>NDIS 6.60 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.60 を示し、その主要な設計の追加機能を説明します。 NDIS 6.60 は、Windows 10、バージョン 1607 および Windows Server 2016 に含まれる以降です。

NDIS 6.60 は、NDIS 6.50 にマイナー バージョン更新です。 NDIS 6.60 する NDIS 6.x ドライバーの移植の詳細については、[NDIS 6.60 に移植する NDIS 6.x ドライバー](porting-ndis-6-x-drivers-to-ndis-6-60.md)を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.60 NDIS 6.50 を増分更新は、主要な新機能が含まれていません。

## <a name="implementing-an-ndis-660-driver"></a>NDIS 6.60、ドライバーを実装します。

定義されている要件を従う必要があります、NDIS 6.60 ドライバー [、NDIS 6.30 ドライバーを実装する](implementing-an-ndis-6-30-driver.md)します。

さらに、NDIS 6.60 ドライバーは、次の要件に準拠する必要があります。

- NDIS 6.60 ドライバーは、NDIS に登録する際に、正しい NDIS バージョンを報告する必要があります。
   
   必要があります、メジャーおよびマイナー NDIS バージョン番号を更新 NDIS_Xxx_DRIVER_CHARACTERISTICS 構造で NDIS 6.60 をサポートするためにします。 MajorNdisVersion メンバーは、6 を含める必要があり、MinorNdisVersion メンバーは、60 を含める必要があります。 この要件は、ミニポート、プロトコル、およびフィルター ドライバーに適用されます。 コンパイラのバージョン情報を更新することも必要があります (を参照してください[コンパイル、NDIS 6.60 ドライバー](#compiling-an-ndis-660-driver))。

- Windows 10、バージョン 1607 および Windows Server 2016 以降の NDIS 6.60 ミニポート ドライバーでは、データ構造の NDIS 6.60 バージョンを使用する必要があります。 詳細については、[データ構造を使用する NDIS 6.60](#using-ndis-660-data-structures)を参照してください。

## <a name="compiling-an-ndis-660-driver"></a>コンパイル、NDIS 6.60 ドライバー

Windows 10 の WDK バージョン 1607 では、ヘッダー バージョン管理をサポートします。 ヘッダー バージョン管理は、NDIS 6.60 ドライバーがコンパイル時に適切な NDIS 6.60 データ構造を使用することを確認します。

ドライバーの Visual Studio プロジェクトには、次のコンパイラ設定を追加します。

- ミニポート ドライバーでは、追加```NDIS660_MINIPORT=1```します。
- フィルターまたはプロトコルのドライバーを追加```NDIS660=1```します。

Windows 10 バージョン 1607 リリース、WDK のドライバーを構築する方法についてを参照してください。[ドライバーをビルド](../develop/building-a-driver.md)します。

## <a name="using-ndis-660-data-structures"></a>NDIS 6.60 データ構造を使用

### <a name="updated-data-structures"></a>更新されたデータ構造体

次のデータ構造は、NDIS 6.60 で更新されました。

- [NDIS_NIC_SWITCH_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff566583)
- [NDIS_RECEIVE_SCALE_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff567228)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/ff567220)

