---
title: デバイスマネージャーの詳細 タブ
description: デバイスマネージャーの詳細 タブ
ms.assetid: 5f1e345f-72c6-4bd4-a0fa-304e5d0d91be
keywords:
- デバイスマネージャー WDK、[詳細] タブ
- ファームウェアリビジョン番号 WDK デバイスマネージャー
- リビジョン番号 WDK デバイスマネージャー
- '[詳細] タブ WDK デバイスマネージャー'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5f92c8347abca45a050ec0cf7ae3e5c5958a65f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837510"
---
# <a name="device-manager-details-tab"></a>デバイスマネージャーの詳細 タブ

デバイスマネージャーには、各デバイスの **[詳細]** タブがあります。 このタブには、ドライバーの開発者やテスト担当者に役立つ多くの情報が表示されます。また、Microsoft カスタマーサポートサービス (CSS) を使用して、顧客の問題を診断できます。 タブのページには、デバイス[id 文字列](device-identification-strings.md)と、ドライバーをデバッグするときに役立つデバイスとドライバーの構成情報が表示されます。

## <a name="viewing-a-devices-details-tab"></a>デバイスの [詳細] タブの表示

[詳細] タブは、既定で有効になっています。 このタブを有効にするには、ユーザー環境変数 DEVMGR_SHOW_DETAILS を1に設定します。 この環境変数を設定すると、デバイスの **[詳細]** タブがデバイスマネージャーで使用できるようになります。 ユーザー環境変数を永続的に設定するには、システムプロパティシートの **[詳細**設定] タブを使用します。

## <a name="providing-firmware-revision-numbers-for-the-details-tab"></a>[詳細] タブのファームウェアリビジョン番号の指定

デバイスマネージャーの **[詳細]** タブでは、デバイスのファームウェアリビジョン番号を表示できます (使用可能な場合)。 ドライバーは、WMI 要求に応答してファームウェアのリビジョン番号を提供できます。 具体的には、ドライバー[**の**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)MSDeviceUI_FirmwareRevision_GUID は、DEVICE_UI_FIRMWARE_REVISION 構造体 (で定義されています) を返すことによって、ドライバーの設定をサポートする必要があります。 構造体には、NULL で終わる WCHAR 文字列としてファームウェアのリビジョン番号が含まれている必要があります。その前に、文字列の長さ ( **null**を含む) を含む USHORT 値を指定します。
