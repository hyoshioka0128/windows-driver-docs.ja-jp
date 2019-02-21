---
title: ファイル システムのセキュリティ機能
description: ファイル システムのセキュリティ機能
ms.assetid: 344083d5-781a-46e3-ab90-b70e57d07dd0
keywords:
- セキュリティ WDK ファイル システムの機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5c946b7a0bd284656990cec4583e29358d1f628
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532402"
---
# <a name="security-features-for-file-systems"></a>ファイル システムのセキュリティ機能


## <span id="ddk_security_features_for_file_systems_if"></span><span id="DDK_SECURITY_FEATURES_FOR_FILE_SYSTEMS_IF"></span>


その他のほとんどの種類のドライバーとは異なりファイル システムは密接、通常のセキュリティの処理に関係します。 これは、セキュリティと Microsoft Windows 内での実装の性質のためです。 一般的な Windows セキュリティ モデルは、セキュリティ記述子オブジェクトに関連付けます、--この場合、ファイル\_オブジェクト。 Windows セキュリティをサポートするファイル システムは、格納して、セキュリティ記述子を取得する責任を負います。 さらに、ファイル システムは、標準のカーネル モード ドライバーの通常のスコープ外にあるその他のいくつかの特別なセキュリティ考慮事項に対応します。

このセクションでは、Windows セキュリティをサポートするためにファイル システムに追加することがありますを主な機能について説明します。 これらの [なし] は必須で、これらのインターフェイスを使用せずにファイル システムを構築できます。 無視しているときにいくつかのセキュリティ機能を実装することはさらに、他のユーザー - これは、ファイル システムの実装に固有です。

ここでは、次のトピックについて説明します。

[セキュリティ記述子](security-descriptors.md)

[権限](privileges.md)

[監査](auditing.md)

[拡張属性のカーネル](kernel-extended-attributes.md)

 


