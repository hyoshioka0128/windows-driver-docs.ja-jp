---
title: デバイス マネージャーの詳細 タブ
description: デバイス マネージャーの詳細 タブ
ms.assetid: 5f1e345f-72c6-4bd4-a0fa-304e5d0d91be
keywords:
- デバイス マネージャーの WDK、[詳細] タブ
- ファームウェアのリビジョン番号を WDK デバイス マネージャー
- リビジョン番号を WDK デバイス マネージャー
- デバイス マネージャーの WDK [詳細] タブします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58a78d25c9337b6115c48481810560df69f3446f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529790"
---
# <a name="device-manager-details-tab"></a>デバイス マネージャーの詳細 タブ

デバイス マネージャーを提供する**詳細**デバイスごとにタブ。 このタブは、ドライバー開発者およびテスト担当者には多くの便利な情報を表示され、Microsoft カスタマー サポート サービス (CSS) お客様の問題の診断に役に立ちます。 タブのページが表示されます[識別文字列](device-identification-strings.md)ドライバーをデバッグするときに役に立ちますデバイスとドライバーの構成情報とします。

## <a name="viewing-a-devices-details-tab"></a>デバイスの詳細 タブを表示します。

[詳細] タブは既定で有効にします。 このタブを有効にするには、1 に DEVMGR_SHOW_DETAILS ユーザー環境変数を設定します。 この環境変数を設定した後、**詳細**デバイスのタブがデバイス マネージャーで使用可能になります。 ユーザーの環境変数を永続的に設定するには、使用、**詳細**システム プロパティ シートのタブ。

## <a name="providing-firmware-revision-numbers-for-the-details-tab"></a>[詳細] タブのファームウェアのリビジョン番号を提供します。

デバイス マネージャーの**詳細**使用可能な場合、タブは、デバイスのファームウェアのリビジョン番号を表示できます。 ドライバーは、WMI 要求に応答することによって、ファームウェアのリビジョン番号を指定できます。 具体的には、ドライバーの[ **DpWmiQueryDataBlock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_query_datablock_callback)ルーチンをサポートする必要があります**MSDeviceUI_FirmwareRevision_GUID** DEVICE_UI_FIRMWARE_REVISION を返すことによって(予測で定義されている) 構造体。 構造体は、前に文字列の長さを格納している USHORT 値、NULL で終わる WCHAR 文字列として、ファームウェアのリビジョン番号を含める必要があります (など、 **NULL**)。
