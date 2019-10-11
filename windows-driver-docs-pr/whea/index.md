---
title: Windows Hardware Error Architecture (WHEA) 設計ガイド
description: Windows Hardware Error Architecture (WHEA) 設計ガイド
ms.assetid: 7a42bacd-cafe-48e0-8568-402738fd6e7c
keywords:
- Windows Hardware Error Architecture WDK
- WHEA WDK
- ハードウェア エラー WDK WHEA
- エラー WDK WHEA
- ハードウェア エラー WDK の検出
- ハードウェア エラー WDK のレポート
- ハードウェア エラー WDK WHEA からの回復
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: af2d98f959ee24bb734a898cf52075b898b7cf5b
ms.sourcegitcommit: 76147255532f5fedacf591679e2604216e89365d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72021050"
---
# <a name="windows-hardware-error-architecture-whea-design-guide"></a>Windows Hardware Error Architecture (WHEA) 設計ガイド

このセクションでは、ハードウェア エラーの報告と回復のサポートを提供する Windows Hardware Error Architecture (WHEA) について説明します。 このセクションでは、次の情報について説明します。

- WHEA とそのコンポーネントの概要 詳細については、「[Windows Hardware Error Architecture Overview (Windows Hardware Error Architecture の概要)](windows-hardware-error-architecture-overview.md)」を参照してください。

- プラットフォーム固有ハードウェア エラー ドライバー (PSHED) プラグインを開発および配布する方法。詳細については、「[Platform-Specific Hardware Error Driver Plug-Ins (プラットフォーム固有ハードウェア エラー ドライバー プラグイン)](platform-specific-hardware-error-driver-plug-ins2.md)」を参照してください。

- ユーザーモード アプリケーションが WHEA プラットフォームと通信する方法。 詳細については、「[Windows Hardware Error Architecture-Aware User-Mode Applications (Windows Hardware Error Architecture 対応のユーザーモード アプリケーション)](windows-hardware-error-architecture-aware-user-mode-applications.md)」を参照してください。

WHEA に関する詳細と、WHEA のハードウェア プラットフォームへの実装方法については、**WHEA プラットフォーム 設計ガイド**をご覧ください。 プラットフォーム ベンダーは、<wheafb@microsoft.com> に電子メールを送信してこの設計ガイドを入手できます。

## <a name="in-this-section"></a>このセクションの内容

[Windows Hardware Error Architecture の基本](introduction-to-the-windows-hardware-error-architecture.md)

[Windows Hardware Error Architecture の新情報](new-information-for-windows-hardware-error-architecture.md)

[Windows Hardware Error Architecture の定義](windows-hardware-error-architecture-definitions.md)

[Windows Hardware Error Architecture の概要](windows-hardware-error-architecture-overview.md)

[プラットフォーム固有ハードウェア エラー ドライバー プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)

[Windows Hardware Error Architecture 対応のユーザーモード アプリケーション](windows-hardware-error-architecture-aware-user-mode-applications.md)

[Windows Hardware Error Architecture デバッガー拡張機能](windows-hardware-error-architecture-debugger-extensions.md)

## <a name="related-topics"></a>関連トピック

[Windows Hardware Error Architecture ACPI テーブルの仕様](http://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WHEA_ACPI-tables.docx)  

[ハードウェアの管理とセキュリティ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614601(v=vs.85))  

[**Bug Check 0x124:WHEA\_UNCORRECTABLE\_ERROR (Windows デバッガー)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x124---whea-uncorrectable-error)  
