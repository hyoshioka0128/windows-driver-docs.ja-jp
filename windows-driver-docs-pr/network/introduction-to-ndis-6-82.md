---
title: NDIS 6.82 の概要
description: このセクションでは、NDIS 6.82 について説明し、NDIS 6.81 からの変更について説明します。 NDIS 6.82 は、Windows 10 version 1809 に含まれています。
ms.assetid: 6BB75BC5-0E49-4467-B030-E0A23D0ED2DA
ms.date: 08/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: d567e6ceb2e29d53ee968a9a2e1452631b325396
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473756"
---
# <a name="introduction-to-ndis-682"></a>NDIS 6.82 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.82 について説明し、主な設計の追加について説明します。 NDIS 6.82 は、Windows 10、バージョン1809、および Windows Server 2019 以降に含まれています。

NDIS 6.82 は、NDIS 6.81 に対するマイナーバージョンの更新です。 Ndis 6. x ドライバーを ndis 6.82 に移植する方法の詳細については、「ndis [6. x ドライバーを ndis 6.82 に移植する](porting-ndis-6-x-drivers-to-ndis-6-82.md)」を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.82 は NDIS 6.81 の増分更新であり、主要な新機能は含まれていません。

## <a name="implementing-an-ndis-682-driver"></a>NDIS 6.82 ドライバーの実装

NDIS 6.82 ドライバーは、「 [ndis 6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で定義されている要件に従う必要があります。

また、NDIS 6.82 ドライバーは、次の要件に準拠している必要があります。

- Ndis 6.82 ドライバーは、ndis に登録するときに正しい NDIS バージョンを報告する必要があります。
   
   NDIS 6.82 をサポートするには、NDIS_Xxx_DRIVER_CHARACTERISTICS 構造体のメジャーおよびマイナーバージョン番号を更新する必要があります。 MajorNdisVersion メンバーには6を含める必要があり、MinorNdisVersion メンバーには82が含まれている必要があります。 この要件は、ミニポート、プロトコル、およびフィルタードライバーに適用されます。 また、コンパイラのバージョン情報も更新する必要があります (「 [NDIS 6.82 ドライバーのコンパイル](#compiling-an-ndis-682-driver)」を参照してください)。

- Windows 10、バージョン1809、および Windows Server 2019 以降の NDIS 6.82 ミニポートドライバーでは、NDIS 6.82 バージョンのデータ構造を使用する必要があります。

## <a name="compiling-an-ndis-682-driver"></a>NDIS 6.82 ドライバーのコンパイル

Windows 10 バージョン1809の WDK は、ヘッダーのバージョン管理をサポートしています。 ヘッダーのバージョン管理により、コンパイル時に NDIS 6.82 ドライバーが適切な NDIS 6.82 データ構造を使用するようになります。

次のコンパイラ設定をドライバーの Visual Studio プロジェクトに追加します。

- ミニポートドライバーの場合は、を追加 `NDIS682_MINIPORT=1` します。
- フィルターまたはプロトコルドライバーの場合は、を追加 `NDIS682=1` します。

Windows 10 バージョン1809リリースの WDK を使用したドライバーの構築の詳細については、「[ドライバーのビルド](../develop/building-a-driver.md)」を参照してください。
