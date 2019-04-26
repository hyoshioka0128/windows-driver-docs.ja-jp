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
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348629"
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

 

 





