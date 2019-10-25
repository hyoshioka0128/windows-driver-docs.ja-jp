---
title: NDIS 6.60 の概要
description: このセクションでは、NDIS 6.60 について説明し、NDIS 6.50 からの変更について説明します。 NDIS 6.60 は、Windows 10、バージョン1607、および Windows Server 2016 以降に含まれています。
ms.assetid: AFDFD1CD-2E07-4A4F-82E2-5E6C5AABD5A3
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae9374d3aacd415bc282d2496525d96859cdb325
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844167"
---
# <a name="introduction-to-ndis-660"></a>NDIS 6.60 の概要

このトピックでは、Network Driver Interface Specification (NDIS) 6.60 について説明し、主な設計の追加について説明します。 NDIS 6.60 は、Windows 10、バージョン1607、および Windows Server 2016 以降に含まれています。

NDIS 6.60 は、NDIS 6.50 に対するマイナーバージョンの更新です。 Ndis 6. x ドライバーを ndis 6.60 に移植する方法の詳細については、「ndis [6. x ドライバーを ndis 6.60 に移植する](porting-ndis-6-x-drivers-to-ndis-6-60.md)」を参照してください。

## <a name="feature-updates"></a>機能更新プログラム

NDIS 6.60 は NDIS 6.50 の増分更新であり、主要な新機能は含まれていません。

## <a name="implementing-an-ndis-660-driver"></a>NDIS 6.60 ドライバーの実装

NDIS 6.60 ドライバーは、「 [ndis 6.30 ドライバーの実装](implementing-an-ndis-6-30-driver.md)」で定義されている要件に従う必要があります。

また、NDIS 6.60 ドライバーは、次の要件に準拠している必要があります。

- Ndis 6.60 ドライバーは、ndis に登録するときに正しい NDIS バージョンを報告する必要があります。
   
   NDIS 6.60 をサポートするには、NDIS_Xxx_DRIVER_CHARACTERISTICS 構造体のメジャーおよびマイナーバージョン番号を更新する必要があります。 MajorNdisVersion メンバーには6を含める必要があり、MinorNdisVersion メンバーには60が含まれている必要があります。 この要件は、ミニポート、プロトコル、およびフィルタードライバーに適用されます。 また、コンパイラのバージョン情報も更新する必要があります (「 [NDIS 6.60 ドライバーのコンパイル](#compiling-an-ndis-660-driver)」を参照してください)。

- Windows 10、バージョン1607、および Windows Server 2016 以降の NDIS 6.60 ミニポートドライバーでは、NDIS 6.60 バージョンのデータ構造を使用する必要があります。 詳細については、「 [NDIS 6.60 データ構造体の使用](#using-ndis-660-data-structures)」を参照してください。

## <a name="compiling-an-ndis-660-driver"></a>NDIS 6.60 ドライバーのコンパイル

Windows 10 バージョン1607の WDK は、ヘッダーのバージョン管理をサポートしています。 ヘッダーのバージョン管理により、コンパイル時に NDIS 6.60 ドライバーが適切な NDIS 6.60 データ構造を使用するようになります。

次のコンパイラ設定をドライバーの Visual Studio プロジェクトに追加します。

- ミニポートドライバーの場合は、```NDIS660_MINIPORT=1```を追加します。
- フィルターまたはプロトコルドライバーの場合は、```NDIS660=1```を追加します。

Windows 10 バージョン1607リリースの WDK を使用したドライバーの構築の詳細については、「[ドライバーのビルド](../develop/building-a-driver.md)」を参照してください。

## <a name="using-ndis-660-data-structures"></a>NDIS 6.60 データ構造体の使用

### <a name="updated-data-structures"></a>更新されたデータ構造

次のデータ構造は、NDIS 6.60 で更新されました。

- [NDIS_NIC_SWITCH_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)
- [NDIS_RECEIVE_SCALE_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_parameters)
- [NDIS_RECEIVE_SCALE_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

