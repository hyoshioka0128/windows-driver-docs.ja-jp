---
title: 確認するかどうか、プラットフォーム、モバイルまたはデスクトップ
description: 確認するかどうか、プラットフォーム、モバイルまたはデスクトップ
ms.assetid: f0a553a4-a23b-45c8-abc5-b5014ba328ae
keywords:
- TMM WDK 表示では、判別中のモバイルまたはデスクトップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420f26fddec527b63c539a6adfc647d6b8034f44
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551293"
---
# <a name="determining-whether-a-platform-is-mobile-or-desktop"></a>確認するかどうか、プラットフォーム、モバイルまたはデスクトップ


TMM では、モバイル コンピューターでのみ実行しは、デスクトップ コンピューターに自動的に無効にします。 ハードウェア ベンダーは、有効にし、独自のメソッドを使用して、デスクトップ コンピューターに複製ビューを入力する必要があります。 プラットフォームがモバイルで、モバイル コンピューターで複製ビューを入力し、TMM を代わりに使用する、独自の方法を使用しないためかどうかを判断する必要があります。

ハードウェア ベンダーは、次のコードを使用して、プラットフォームがモバイルまたはデスクトップかを判断します。 プラットフォームは、複製のビューを入力するのに適切なメカニズムを使用できます。

```cpp
#include <Powrprof.h>   // For GetPwrCapabilities

    BOOL IsMobilePlatform()
    {
        BOOL fIsMobilePlatform = FALSE;

        fIsMobilePlatform = (PlatformRoleMobile == PowerDeterminePlatformRole());

        POWER_PLATFORM_ROLE iRole;

        // Check if the operating system determines 
        // that the computer is a mobile computer.
        iRole = PowerDeterminePlatformRole();

        if (PlatformRoleMobile == iRole)
        {
            fIsMobilePlatform = TRUE;
        }
        else if (PlatformRoleDesktop == iRole) 
        // Can happen when a battery is not plugged into a laptop
        {
            SYSTEM_POWER_CAPABILITIES powerCapabilities;

            if (GetPwrCapabilities(&powerCapabilities))
            {
         // Check if a battery exists, and it is not for a UPS.
         // Note that SystemBatteriesPresent is set on a laptop even if the battery is unplugged.
                fIsMobilePlatform = ((TRUE == powerCapabilities.SystemBatteriesPresent) && (FALSE == powerCapabilities.BatteriesAreShortTerm));
            }
            // GetPwrCapabilities should never fail 
            // However, if it does, leave fReturn == FALSE.
        }

        return fIsMobilePlatform;
    }
```

上記のコードで呼び出された関数については、Microsoft Windows SDK のドキュメントを参照してください。

 

 





