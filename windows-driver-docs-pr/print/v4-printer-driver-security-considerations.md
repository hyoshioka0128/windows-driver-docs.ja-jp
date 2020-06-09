---
title: V4 プリンター ドライバー セキュリティ考慮事項
description: 権限の昇格、なりすましデバイス、注入攻撃などの通常の脅威に加えて、v4 プリンタードライバーも、低い権限のアプリケーションと互換性がある必要があります。
ms.assetid: 8A1508C1-4856-4E3C-8378-AC5FDD55D118
ms.date: 06/08/2020
ms.localizationpriority: medium
ms.openlocfilehash: 278aeabac863c9a81a0c4c98188299d0607c348b
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534937"
---
# <a name="v4-printer-driver-security-considerations"></a>V4 プリンター ドライバー セキュリティ考慮事項

権限の昇格、なりすましデバイス、注入攻撃などの通常の脅威に加えて、v4 プリンタードライバーも、低い権限のアプリケーション (Internet Explorer 9 など) と互換性がある必要があります。

XPS レンダリングフィルターと JavaScript ファイルはすべて、アプリケーション、ユーザー、またはコンピューターの境界を越えたデータから、信頼されていないデータのすべての形式に対してセキュリティで保護する必要があります。 形式が正しくない PrintTickets、XPS ドキュメント、プロパティバッグ、および BidiResponses は、慎重に検証して解析する必要があり、実行可能コードの保存には使用しないでください。 パートナーは、広範な fuzzed ファイルテストを使用して、セキュリティの整合性を損なうことなく、正常な障害を確実に実現することをお勧めします。

## <a name="related-topics"></a>関連トピック

[V4 プリンター ドライバー開発ベスト プラクティス](v4-printer-driver-development-best-practices.md)  
