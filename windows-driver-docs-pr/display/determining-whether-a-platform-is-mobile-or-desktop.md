---
title: プラットフォームがモバイルとデスクトップのどちらであるかの確認
description: プラットフォームがモバイルとデスクトップのどちらであるかの確認
ms.assetid: f0a553a4-a23b-45c8-abc5-b5014ba328ae
keywords:
- TMM WDK 表示では、判別中のモバイルまたはデスクトップ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420f26fddec527b63c539a6adfc647d6b8034f44
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342424"
---
# <a name="determining-whether-a-platform-is-mobile-or-desktop"></a>プラットフォームがモバイルとデスクトップのどちらであるかの確認


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

 

 





