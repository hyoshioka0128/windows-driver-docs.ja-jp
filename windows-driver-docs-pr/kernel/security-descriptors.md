---
title: セキュリティ記述子
description: セキュリティ記述子
ms.assetid: a5edd5e8-6fc7-4ab0-aebc-f0cd8e9299b6
keywords:
- セキュリティ記述子 WDK オブジェクト
- システムの ACL の WDK オブジェクト
- オブジェクトの SACL の WDK
- 随意 ACL WDK オブジェクト
- DACL の WDK オブジェクト
- WDK のオブジェクトのアクセス制御リストします。
- ACL の WDK オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d2e9fc52a04ba5c3d3363750fb3e0964249e74
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574336"
---
# <a name="security-descriptors"></a>セキュリティ記述子


すべてのオブジェクトが、*セキュリティ記述子*オブジェクトのセキュリティ設定が含まれています。 カーネル モード、不透明で[**セキュリティ\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff563689)データ型は、セキュリティ記述子を表します。

セキュリティ記述子の情報が格納されている*アクセス制御リスト*(Acl)。 一連のアクセス制御リストから成る*アクセス制御エントリ*(Ace)。

セキュリティ記述子には、2 つの個別の Acl があります。

-   A*システム ACL* (SACL) オブジェクトの操作がログに記録されますを決定します。

-   A*随意 ACL* (DACL) のオブジェクトの特定の操作を実行できるユーザーを決定します。

通常、ドライバー開発者向けでは、随意 Acl で懸念のみです。 システムの Acl の詳細については、Microsoft Windows SDK を参照してください。

随意 ACL、ACE には、3 つ情報にはが含まれています。

-   A*セキュリティ識別子*(SID)。 セキュリティ識別子は、ACE を適用するユーザーを決定します。 SID は、1 人のユーザーまたはユーザーのグループを表すことができます。 たとえば、世界の SID は、すべてのユーザーのセットを表します。

-   アクセス権のセット。 アクセス権については、次を参照してください。[アクセス権](access-rights.md)します。

-   アクセス権のセットが許可または拒否するかどうか。

最も重要なセキュリティ記述子ではされる、ドライバーのドライバーのデバイス オブジェクトです。 詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](securing-device-objects.md)します。

記述子のセキュリティの詳細については、Windows SDK は一般を参照してください。

 

 




