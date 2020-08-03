---
title: NDIS 6.83 の概要
description: このセクションでは、NDIS 6.83 について説明し、NDIS 6.82 からの変更について説明します。 NDIS 6.83 は、Windows 10 version 1903 に含まれています。
ms.assetid: FC90E212-6ED6-432C-8729-5239EF5FDD65
ms.date: 05/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9048830b7007bbe4963204483989509ae94843ac
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473754"
---
# <a name="introduction-to-ndis-683"></a>NDIS 6.83 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.83 について説明し、主な設計の追加について説明します。 NDIS 6.83 は、Windows 10、バージョン1903、および Windows Server 2019 以降に含まれています。

NDIS 6.83 は、NDIS 6.82 に対するマイナーバージョンの更新です。 Ndis 6. x ドライバーを ndis 6.83 に移植する方法の詳細については、「ndis [6. x ドライバーを ndis 6.83 に移植する](porting-ndis-6-x-drivers-to-ndis-6-83.md)」を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.83 は NDIS 6.82 の増分更新であり、主要な新機能は含まれていません。

## <a name="implementing-an-ndis-683-driver"></a>NDIS 6.83 ドライバーの実装

NDIS 6.83 ドライバーは、「 [ndis 6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で定義されている要件に従う必要があります。

また、NDIS 6.83 ドライバーは、次の要件に準拠している必要があります。

- Ndis 6.83 ドライバーは、ndis に登録するときに正しい NDIS バージョンを報告する必要があります。
   
   NDIS 6.83 をサポートするには、NDIS_Xxx_DRIVER_CHARACTERISTICS 構造体のメジャーおよびマイナーバージョン番号を更新する必要があります。 MajorNdisVersion メンバーには6を含める必要があり、MinorNdisVersion メンバーには83が含まれている必要があります。 この要件は、ミニポート、プロトコル、およびフィルタードライバーに適用されます。 また、コンパイラのバージョン情報も更新する必要があります (「 [NDIS 6.83 ドライバーのコンパイル](#compiling-an-ndis-683-driver)」を参照してください)。

- Windows 10、バージョン1903、および Windows Server 2019 以降の NDIS 6.83 ミニポートドライバーでは、NDIS 6.83 バージョンのデータ構造を使用する必要があります。

## <a name="compiling-an-ndis-683-driver"></a>NDIS 6.83 ドライバーのコンパイル

Windows 10 バージョン1903の WDK は、ヘッダーのバージョン管理をサポートしています。 ヘッダーのバージョン管理により、コンパイル時に NDIS 6.83 ドライバーが適切な NDIS 6.83 データ構造を使用するようになります。

次のコンパイラ設定をドライバーの Visual Studio プロジェクトに追加します。

- ミニポートドライバーの場合は、を追加 `NDIS683_MINIPORT=1` します。
- フィルターまたはプロトコルドライバーの場合は、を追加 `NDIS683=1` します。

Windows 10 バージョン1903リリースの WDK を使用したドライバーの構築の詳細については、「[ドライバーのビルド](../develop/building-a-driver.md)」を参照してください。