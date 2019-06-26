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
ms.openlocfilehash: dfe6669c7d315c4a105d449a9bcb670e9733ff08
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373365"
---
# <a name="security-descriptors"></a>セキュリティ記述子


すべてのオブジェクトが、*セキュリティ記述子*オブジェクトのセキュリティ設定が含まれています。 カーネル モード、不透明で[**セキュリティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_security_descriptor)データ型は、セキュリティ記述子を表します。

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

 

 




