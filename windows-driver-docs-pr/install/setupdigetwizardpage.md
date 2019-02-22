---
title: SetupDiGetWizardPage
description: SetupDiGetWizardPage
ms.assetid: c43ee948-10aa-4b8f-91d0-0f3baf8ccf16
keywords:
- SetupDiGetWizardPage デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- SetupDiGetWizardPage
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a4898a9e6ea9445f26954a166de9f077240a31d4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559745"
---
# <a name="setupdigetwizardpage"></a>SetupDiGetWizardPage


**SetupDiGetWizardPage**関数はシステム用に予約されています。 ウィザードのページについてを参照してください、DIF_NEWDEVICEWIZARD_*XXX*要求、たとえば、 [ **DIF_NEWDEVICEWIZARD_FINISHINSTALL**](dif-newdevicewizard-finishinstall.md)します。

```cpp
HPROPSHEETPAGE
 SetupDiGetWizardPage(
 IN HDEVINFO DeviceInfoSet, 
 IN PSP_DEVINFO_DATA DeviceInfoData..OPTIONAL,
 IN PSP_INSTALLWIZARD_DATA InstallWizardData,
 IN DWORD PageType,
    IN DWORD Flags
 );
```

 

 





