---
title: Storport でのポート構成情報の設定
description: Storport でのポート構成情報の設定
ms.assetid: dcc2cb3c-2fe6-4f70-814b-66b59a237dd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a45a6fba96058cc2dd24a1400ca7af1ac9609249
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363944"
---
# <a name="setting-port-configuration-information-with-storport"></a>Storport でのポート構成情報の設定


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


Microsoft Windows PnP マネージャーでは、Storport によって管理アダプターを検出、Storport ドライバーを開始することを通知します。 次に、ミニポート ドライバーの呼び出す Storport [ **HwStorFindAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_find_adapter)ルーチンに渡すこと、 [**ポート\_構成\_情報 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造体。

Storport によって管理されるすべてのアダプターは、の PnP デバイスであるため*HwStorFindAdapter*アダプターの物理的には検索しません。 このミニポート ドライバー ルーチンが、ポートで指定されたパラメーターを使用して、アダプターの初期化を試みる代わりに、\_構成\_情報構造体とポートの初期化が完了した\_構成\_については、ポートにそれらの値を格納する\_構成\_情報 Storport がデバイスの拡張機能を初期化するために必要があります。

詳細については、次を参照してください[**ポート\_構成\_情報 (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_port_configuration_information)と[**ポート\_構成\_。情報 (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))します。

 

 




