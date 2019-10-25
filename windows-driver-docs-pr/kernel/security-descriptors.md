---
title: セキュリティ記述子
description: セキュリティ記述子
ms.assetid: a5edd5e8-6fc7-4ab0-aebc-f0cd8e9299b6
keywords:
- セキュリティ記述子 WDK オブジェクト
- システム ACL WDK オブジェクト
- SACL WDK オブジェクト
- 随意 ACL WDK オブジェクト
- DACL WDK オブジェクト
- アクセス制御リスト WDK オブジェクト
- ACL WDK オブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a671b5eccc1b7e38622836fcf817cb8ce8f77a64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838449"
---
# <a name="security-descriptors"></a>セキュリティ記述子


すべてのオブジェクトには、オブジェクトのセキュリティ設定を含む*セキュリティ記述子*があります。 カーネルモードの場合、不透明[**セキュリティ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_security_descriptor)のデータ型はセキュリティ記述子を表します。

セキュリティ記述子の情報は、*アクセス制御リスト*(acl) に格納されます。 アクセス制御リストは、一連の*アクセス制御エントリ*(ace) で構成されます。

セキュリティ記述子には、次の2つの異なる Acl があります。

-   *システム ACL* (SACL)。オブジェクトのどの操作をログに記録するかを決定します。

-   *随意 ACL* (DACL)。オブジェクトに対して特定の操作を実行できるユーザーを決定します。

通常、ドライバー開発者は随意 Acl のみを使用します。 システム Acl の詳細については、Microsoft Windows SDK を参照してください。

随意 ACL の場合、各 ACE には次の3つの情報が含まれます。

-   *セキュリティ識別子*(SID)。 セキュリティ識別子は、ACE が適用されるユーザーを決定します。 SID は、1人のユーザー、またはユーザーのグループを表すことができます。 たとえば、World SID は、すべてのユーザーのセットを表します。

-   一連のアクセス権。 アクセス権の詳細については、「[アクセス権](access-rights.md)」を参照してください。

-   アクセス権のセットを許可するか、拒否するかを指定します。

ドライバーの場合、最も重要なセキュリティ記述子は、ドライバーのデバイスオブジェクトのものです。 詳細については、「[デバイスオブジェクトのセキュリティ保護](securing-device-objects.md)」を参照してください。

一般的なセキュリティ記述子の詳細については、Windows SDK を参照してください。

 

 




