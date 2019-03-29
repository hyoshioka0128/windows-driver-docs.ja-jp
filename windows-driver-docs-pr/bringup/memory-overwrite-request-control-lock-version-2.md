---
title: メモリ上書き要求制御 (MOR) LOCK バージョン 2
description: メモリ上書き要求制御 (MOR) LOCK バージョン 2
ms.date: 05/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: a86784ffc1142ea38e3dfec682a0120d6bc7a0cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574745"
---
# <a name="memory-overwrite-request-control-mor-lock-version-2"></a>メモリ上書き要求制御 (MOR) LOCK バージョン 2


Windows の主要なセキュリティ機能 Device Guard では、ハイパーバイザーが悪意のある OS カーネルからシークレットを保護する必要が現在メモリ内でのシークレットの脅威モデルが変更されました。 これには、「プラットフォーム リセット攻撃軽減策」悪意のある管理者やカーネルから RAM 内のシークレットを保護する TCG の拡張が必要です。 バージョン 1 には、UEFI 変数が定義されているロック元されますバイト、によって変更されているを避ける権限を設定すると、このエージェントが OS カーネルなど。 Device Guard が有効にすると、元の複数のバイトは、プラットフォームは、すべてのリセットの間でメモリをワイプする必要があります –、自動検出が禁止されていることを示すパターンに設定されます。 これには、Device Guard が有効になっているプラットフォームで、パフォーマンスの低下が導入されました。

ロックのバージョン 2 では、ロックを無効にする、ハイパーバイザー、たとえば、承認されたエージェントを許可するキーをサポートします。 想定されるは、通常のシャット ダウン中に、ハイパーバイザーはまず RAM からシークレットを削除、バージョン 2 のキーを使用して、ロックを無効に RAM をオフにせずに再起動するプラットフォームを有効にすると、元の複数バイトをオフにです。 バージョン 1 と関連付けられているパフォーマンスの低下を回避、されますロックのバージョン 2 を実装するファームウェアは Device Guard のシークレットの保護を提供します。 そのため、突然再起動攻撃の攻撃対象領域を減らす

次のバージョンの Windows では、されますロック V2 のサポートが含まれます。

-   Windows Server Technical Preview 2016

-   Windows 10 バージョン 1607 以降


## <a name="related-resources"></a>関連リソース

[TCG プラットフォーム リセット攻撃の軽減策の仕様](https://www.trustedcomputinggroup.org/wp-content/uploads/Platform-Reset-Attack-Mitigation-Specification.pdf)

[セキュリティで保護された複数の実装](https://docs.microsoft.com/windows-hardware/drivers/bringup/device-guard-requirements)



