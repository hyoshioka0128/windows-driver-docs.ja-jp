---
title: デジタル著作権管理
description: デジタル著作権管理
ms.assetid: 7ce19196-5180-421f-b6be-ac4a235a8c16
keywords:
- WDM オーディオ ドライバー WDK、デジタル著作権管理
- オーディオ ドライバー WDK、デジタル著作権管理
- Rights Management の WDK のデジタル オーディオ
- DRM WDK オーディオ
- セキュリティの WDK オーディオ
- 独自のデータ セキュリティの WDK オーディオ
- 使用状況規則 WDK オーディオ
- ルールの WDK オーディオを再生
- 暗号化の WDK オーディオ
- 暗号化の WDK オーディオ
- WDM オーディオ ドライバー WDK、セキュリティ
- オーディオ ドライバー WDK、セキュリティ
- 保護されたコンテンツの WDK オーディオ
- デジタル コンテンツのセキュリティの WDK オーディオ
- スクランブル コンテンツ WDK オーディオ
- 承認されていないコピー WDK オーディオ
- コピー防止 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ebb78ebef471b8d786b4dd5561e4f7ea62f1d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574863"
---
# <a name="digital-rights-management"></a>デジタル著作権管理


## <span id="digital_rights_management"></span><span id="DIGITAL_RIGHTS_MANAGEMENT"></span>


デジタル著作権管理 (DRM) では、コンテンツ プロバイダーが独自の音楽またはその他のデータから不正コピーとその他の無効な使用を保護する手段を提供します。 DRM テクノロジは、暗号化することにアタッチしてデジタル コンテンツを保護するユーザーはコンテンツを再生する条件を決定するための使用に関する規則。 使用に関する規則は通常コピーを防止またはコンテンツを再生する時間数を制限します。 オペレーティング システムのこれらの規則を適用するドライバーと共に動作します。

DRM は、デジタル コンテンツを購入するときに合意した、使用状況規則に違反する場合を除き、ユーザーに対して透過的に設計されています。

信頼済みのオーディオ ドライバーによってのみ、DRM で保護されているすべてのデジタル オーディオ コンテンツを再生できます。 これらは、microsoft DRM 準拠していることを確認し、回避することができます DRM セキュリティ対策を抜け穴が含まれていないハードウェアの互換性テストに合格したドライバーです。

さらに、ドライバーにデバッガーがアタッチされている場合は、保護されたコンテンツを再生できません。

Microsoft Windows Me ドライバー、DRM 準拠のためのテスト WHQL (Microsoft Windows ハードウェア品質ラボ) は省略可能です。 ただし、Windows XP 以降のドライバー、DRM 準拠が必要です。 詳細については、次を参照してください。、 **DRM 要件**トピックは、次の一覧。

このセクションでは、次のトピックが表示されます。

[DRM の概要](drm-overview.md)

[コンテンツの Id およびコンテンツの権限](content-ids-and-content-rights.md)

[DRM コンテンツ Id の転送](forwarding-drm-content-ids.md)

[DRM の要件](drm-requirements.md)

[開発およびデバッグ DRM ドライバー](developing-and-debugging-drm-drivers.md)

[DRM 関数とインターフェイス](drm-functions-and-interfaces.md)

 

 




