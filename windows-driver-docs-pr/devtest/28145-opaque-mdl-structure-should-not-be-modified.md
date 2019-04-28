---
title: C28145
description: 警告 C28145 が不透明な MDL 構造体は、ドライバーによっては変更しないでください。
ms.assetid: efbd667b-fb0e-4a4d-bb6a-e8249c113a91
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28145
ms.openlocfilehash: ba336ed8a7c353fa107cd4378f3f5eb917049005
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361526"
---
# <a name="c28145"></a>C28145


C28145 を警告します。不透明な MDL 構造体は、ドライバーによっては変更しないでください。

ドライバーのコードでは、MDL 構造体のメンバーを変更します。

**MdlFlags**フィールドは MDL のすべてのフィールドのプロキシとして使用されます。 フィールドは変更できません、MDL を除き\_マッピング\_できます\_、および Microsoft Windows 98 または Windows NT (SP4) 互換性が必要なドライバーの使用は、失敗、および MDL\_ページ\_ロックされていると、互換性のある Windows 2000 を使用する必要があるドライバーの使用がされます。

 

 





