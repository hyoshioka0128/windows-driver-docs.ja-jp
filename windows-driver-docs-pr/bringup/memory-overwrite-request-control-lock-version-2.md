---
title: メモリ上書き要求制御 (MOR) LOCK バージョン 2
description: メモリ上書き要求制御 (MOR) LOCK バージョン 2
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: b3706ffb99d3c8f86f6f19d4b8c42f939c82f14e
ms.sourcegitcommit: 969a98d4866be74e145df617a9f0963053898a0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153178"
---
# <a name="memory-overwrite-request-control-mor-lock-version-2"></a>メモリ上書き要求制御 (MOR) ロックバージョン2

高度なメモリ攻撃を防ぐために、既存のシステム BIOS のセキュリティ対策 MemoryOverwriteRequestControl が改善され、新しい脅威から保護するためのロックがサポートされるようになりました。

バージョン1では、UEFI 変数が定義されています。これは、設定されると、元の MOR は byte をロックして、OS カーネルなどの未承認のエージェントによって変更されるのを防ぎます。 MOR lock が有効になっている場合、元の MOR は byte は0x11 に設定されます。これは、プラットフォームがすべてのリセットでメモリをワイプする必要があることを示します。自動検出は禁止されています。 これにより、プラットフォームを有効にするとパフォーマンスが低下します。

バージョン2は、ハイパーバイザーなどの承認されたエージェントがロックを無効にできるようにするキーをサポートしています。 通常のシャットダウン中に、ハイパーバイザーは最初に RAM からシークレットを削除し、バージョン2キーを使用してロックを無効にし、元の MOR は byte をクリアして、プラットフォームが RAM をクリアせずに再起動できるようにすることを想定しています。 バージョン2の MOR Lock を実装するファームウェアは、バージョン1に関連するパフォーマンスの低下を回避しながら、追加の保護を提供します。

MOR Lock V2 のサポートは、次のバージョンの Windows に含まれています。

- Windows Server Technical Preview 2016

- Windows 10 バージョン 1607 以降

## <a name="related-resources"></a>関連リソース

[TCG プラットフォームリセット攻撃の緩和の仕様](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

[Secure MOR 実装](https://docs.microsoft.com/windows-hardware/drivers/bringup/device-guard-requirements)
