---
title: V4 プリンター ドライバーのセキュリティに関する考慮事項
description: 特権の昇格、なりすましのデバイスや中間者攻撃など、一般的な脅威だけでなく v4 プリンター ドライバーは Internet Explorer 9 などの権限の低いアプリケーションと互換性があるも必要です。
ms.assetid: 8A1508C1-4856-4E3C-8378-AC5FDD55D118
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cf2299bbcf43dd90a02a75ce4ab64059aa280b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532524"
---
# <a name="v4-printer-driver-security-considerations"></a>V4 プリンター ドライバーのセキュリティに関する考慮事項


特権の昇格、なりすましのデバイスや中間者攻撃など、一般的な脅威だけでなく v4 プリンター ドライバーは Internet Explorer 9 などの権限の低いアプリケーションと互換性があるも必要です。

XPS 表示フィルターと JavaScript ファイルする必要がありますすべてに対して強固で信頼されていないデータのすべてのフォーム アプリケーション、ユーザー、またはからのデータからコンピューターの境界を越えてします。 形式が正しくない PrintTickets、XPS ドキュメント、プロパティ バッグ、およびでも BidiResponses 必要がありますを検証し、慎重に解析し、実行可能コードの格納に使用することはありません。 いるパートナー大雑把なファイルの広範なテストを使用してセキュリティの整合性を損なうことがなくグレースフル障害をことを確認することをお勧めします。

## <a name="related-topics"></a>関連トピック
[V4 プリンター ドライバーの開発に関するベスト プラクティス](v4-printer-driver-development-best-practices.md)  



