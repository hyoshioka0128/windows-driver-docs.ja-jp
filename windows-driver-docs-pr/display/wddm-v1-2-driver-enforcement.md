---
title: WDDM 1.2 ドライバーの強制
description: WDDM 1.2 ドライバーによって、Windows Display Driver Model (WDDM) 1.2 の必須の機能がサポートされているかどうかを判断する Windows 8 以降では、Microsoft DirectX グラフィックスのカーネルのサブシステム (Dxgkrnl) による検証が適用されます。
ms.assetid: DF0C6F50-CC68-4002-9ED3-F42EA24D24B1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c596a2f25f46e1d35d85a80a8152cd18566548e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391188"
---
# <a name="wddm-12-driver-enforcement"></a>WDDM 1.2 ドライバーの強制


WDDM 1.2 ドライバーによって、Windows Display Driver Model (WDDM) 1.2 の必須の機能がサポートされているかどうかを判断する Windows 8 以降では、Microsoft DirectX グラフィックスのカーネルのサブシステム (Dxgkrnl) による検証が適用されます。

WDDM 1.2 には、必須およびオプションの両方の機能があります。 ドライバーのオプションの機能の任意の組み合わせ (または none) ドライバーを実装できる、WDDM 1.2 ドライバーとして自体を要求するすべての必須機能上限を設定する必要があります。 非-WDDM 1.2 ドライバーには、WDDM 1.2 機能はありませんを報告する必要があります。

## <a name="span-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanspan-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanspan-iduserexperiencewhenadriverfailsthedxgkrnlvalidationspanuser-experience-when-a-driver-fails-the-dxgkrnl-validation"></a><span id="User_experience_when_a_driver_fails_the_Dxgkrnl_validation"></span><span id="user_experience_when_a_driver_fails_the_dxgkrnl_validation"></span><span id="USER_EXPERIENCE_WHEN_A_DRIVER_FAILS_THE_DXGKRNL_VALIDATION"></span>ドライバー Dxgkrnl 検証が失敗したときに、ユーザー エクスペリエンス


ドライバーはそれ自体を要求および WDDM 1.2 として誤ってまたは必須の機能の一部のみが実装は、アダプターを作成に失敗し、システムが劣る Microsoft 基本的なディスプレイ ドライバー (MSBDD) にします。

 

 





