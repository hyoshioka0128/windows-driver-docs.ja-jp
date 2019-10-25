---
title: Storport でのポート構成情報の設定
description: Storport でのポート構成情報の設定
ms.assetid: dcc2cb3c-2fe6-4f70-814b-66b59a237dd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5efbc603506523ec21eb99cef74e757dcb9d2165
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845229"
---
# <a name="setting-port-configuration-information-with-storport"></a>Storport でのポート構成情報の設定


## <span id="ddk_setting_port_configuration_information_with_storport_kg"></span><span id="DDK_SETTING_PORT_CONFIGURATION_INFORMATION_WITH_STORPORT_KG"></span>


Microsoft Windows PnP マネージャーは、Storport によって管理されているアダプターを検出すると、それを開始するように Storport ドライバーに通知します。 次に、Storport はミニポートドライバーの[**HwStorFindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)ルーチンを呼び出し、[**ポート\_CONFIGURATION\_INFORMATION (Storport)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))構造体を渡します。

Storport で管理されるすべてのアダプターは PnP デバイスなので、 *HwStorFindAdapter*は物理的にアダプターを検索しません。 代わりに、このミニポートドライバールーチンは、ポート\_構成\_情報構造体で指定されたパラメーターを使用してアダプターを初期化しようとし、ポート\_構成の初期化を完了\_デバイス拡張機能を初期化するために Storport が必要とする可能性のある情報\_ポート\_構成に格納されている情報。

詳細については、「 [**port\_configuration\_information (SCSI)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information) 」および「 [**port\_configuration\_information (STORPORT)** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))」を参照してください。

 

 




