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
ms.openlocfilehash: d35e9561036a90667c9c7da5876c2dd7add3efd1
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/10/2020
ms.locfileid: "78947424"
---
# <a name="windows-hardware-error-architecture-whea-design-guide"></a>Windows Hardware Error Architecture (WHEA) 設計ガイド

このセクションでは、ハードウェア エラーの報告と回復のサポートを提供する Windows Hardware Error Architecture (WHEA) について説明します。 このセクションでは、次の情報について説明します。

- WHEA とそのコンポーネントの概要 詳細については、「[Windows Hardware Error Architecture Overview (Windows Hardware Error Architecture の概要)](windows-hardware-error-architecture-overview.md)」を参照してください。

- プラットフォーム固有ハードウェア エラー ドライバー (PSHED) プラグインを開発および配布する方法。詳細については、「[Platform-Specific Hardware Error Driver Plug-Ins (プラットフォーム固有ハードウェア エラー ドライバー プラグイン)](platform-specific-hardware-error-driver-plug-ins2.md)」を参照してください。

- ユーザーモード アプリケーションが WHEA プラットフォームと通信する方法。 詳細については、「[Windows Hardware Error Architecture-Aware User-Mode Applications (Windows Hardware Error Architecture 対応のユーザーモード アプリケーション)](windows-hardware-error-architecture-aware-user-mode-applications.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

[Windows Hardware Error Architecture の基本](introduction-to-the-windows-hardware-error-architecture.md)

[Windows Hardware Error Architecture の新情報](new-information-for-windows-hardware-error-architecture.md)

[Windows Hardware Error Architecture の定義](windows-hardware-error-architecture-definitions.md)

[Windows Hardware Error Architecture の概要](windows-hardware-error-architecture-overview.md)

[プラットフォーム固有ハードウェア エラー ドライバー プラグイン](platform-specific-hardware-error-driver-plug-ins2.md)

[Windows Hardware Error Architecture 対応のユーザーモード アプリケーション](windows-hardware-error-architecture-aware-user-mode-applications.md)

[Windows Hardware Error Architecture デバッガー拡張機能](windows-hardware-error-architecture-debugger-extensions.md)

## <a name="related-topics"></a>関連トピック

[Windows Hardware Error Architecture ACPI テーブルの仕様](https://download.microsoft.com/download/9/c/5/9c5b2167-8017-4bae-9fde-d599bac8184a/WHEA_ACPI-tables.docx)  

[ハードウェアの管理とセキュリティ](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn614601(v=vs.85))  

[**Bug Check 0x124:WHEA\_UNCORRECTABLE\_ERROR (Windows デバッガー)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x124---whea-uncorrectable-error)  
