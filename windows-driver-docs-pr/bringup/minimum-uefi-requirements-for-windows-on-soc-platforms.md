---
title: SoC プラットフォーム上の Windows に対する最小限の UEFI 要件
description: SoC プラットフォーム上の Windows に対する最小限の UEFI 要件
ms.assetid: 32743d69-83a2-4658-8652-6d624e75e3db
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0ac9e3fc0c1c96f9f7826a96e06fed183fb449ad
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851737"
---
# <a name="minimum-uefi-requirements-for-windows-on-soc-platforms"></a>SoC プラットフォーム上の Windows に対する最小限の UEFI 要件

Unified Extensible Firmware Interface (UEFI) は、Windows を実行している SoC プラットフォームに必要なブートファームウェアです。 このセクションでは、SoC プラットフォームで Windows を実行するための UEFI 実装要件について説明します。 これらの要件に対する監視と準拠は、Windows の適切な機能を保証するのに役立ちます。

この一連の要件は、すべての SoC ベースのコンピューティングシステムに適用されますが、いくつかの制限があります。 このガイドは、Windows の全機能セットを前提としており、従来の netbook フォームファクターとワイヤレス、マルチタッチのみのモバイルデバイスをサポートしています。 そのため、このようなシステムで広く使用されるテクノロジに限定されます。 このドキュメントで取り上げられていないテクノロジを実装しているシステムについては[、uefi 仕様](https://uefi.org/specifications)の uefi 仕様を参照してください。

Windows では、Unified Extensible Firmware Interface (UEFI) バージョン2.3.1 以降に基づくファームウェアのリビジョンがサポートされています。

> [!NOTE]
> Windows では、UEFI 2.3.1 仕様で定義されている機能のサブセットをサポートしています。 Windows の実装には、ファームウェアのより高いリビジョンに対する明示的なチェックはありません。 このドキュメントで説明されている必要なサポートが含まれている場合、オペレーティングシステムはファームウェアのより高いリビジョンをサポートします。

## <a name="in-this-section"></a>このセクションの内容

| トピック | 説明 |
| --- | --- |
| [SoC プラットフォーム上のすべての Windows エディションに適用される UEFI 要件](uefi-requirements-that-apply-to-all-windows-platforms.md) | デスクトップエディション (Home、Pro、Enterprise、および教育) および Windows 10 Mobile 用の Windows 10 に適用される UEFI の要件について説明します。 |
| [Windows 10 Mobile に対する UEFI 要件](uefi-requirements-specific-to-windows-mobile.md) | Windows 10 Mobile を実行するデバイスは、このトピックで説明されている追加の要件を満たしている必要があります。 |
| [USB フラッシング サポートのための UEFI 要件](uefi-requirements-for-usb-flashing-support.md) | Microsoft では、エンジニアリングおよび製造環境で使用するために、USB ベースの点滅ソリューションをいくつか提供しています。 これらのツールでデバイスを使用するには、デバイス上の UEFI 環境が、このトピックに記載されている要件を満たしている必要があります。 |
