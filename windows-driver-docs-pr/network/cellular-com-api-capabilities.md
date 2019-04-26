---
title: 携帯ネットワーク COM API の機能
description: このトピックでは、携帯電話の COM API の機能についてを説明します。
ms.assetid: f6172f25-9003-4b98-a87d-26dc193d40e3
keywords:
- COM API 機能が移動体通信ネットワーク ドライバー
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87107e64fd6fffd5c62e6f6e8cc4dc9bdbed98c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341902"
---
# <a name="cellular-com-api-capabilities"></a>携帯ネットワーク COM API の機能

> [!WARNING]
> 携帯電話の COM API は、Windows 10 で非推奨とされます。 このコンテンツは、OEM および携帯電話会社が Windows Phone 8.1 アプリケーションの作成の保守をサポートするために提供されます。

実行する携帯電話の Api は、携帯電話のアプリケーションを含むパッケージ ファイルへの機能を追加する必要があります。 アプリケーションが呼び出すメソッドごとに、必要な機能が含まれます。

携帯電話のすべての COM インターフェイス メソッドには、ID_CAP_CELL_API_COMMON 機能が必要です。 追加の機能の要件は次のとおりです。

| メソッド | ID_CAP_CELL_API_COMMON に加えての機能 |
| --- | --- |
| IOemCellularModem::SendModemOpaqueCommand | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::RegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::UnRegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::SetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::GetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCan::GetPositionInfo | ID_CAP_CELL_API_LOCATION |
| IOemUiccApp::GetAppId | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetType | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetPinLockState | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecord | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecord | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetRecordStatusOnFilePath | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecordOnFilePath | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecordOnFilePath | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetIMSI | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetSIDNID | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetSubscriberNumbers | ID_CAP_CELL_API_UICC |
| IOemUiccAppEx2::GetNAI | ID_CAP_CELL_API_UICC |

## <a name="related-topics"></a>関連トピック

[携帯電話の COM API の設計ガイド](cellular-com-api-design-guide.md)

[携帯電話の COM API リファレンス](https://msdn.microsoft.com/library/windows/hardware/dn946508)

