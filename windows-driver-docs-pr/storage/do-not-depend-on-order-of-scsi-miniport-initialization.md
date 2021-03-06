---
title: SCSI ミニポート初期化の順序への依存禁止
description: SCSI ミニポート初期化の順序への依存禁止
ms.assetid: 762fa062-4eaa-40f2-acdb-99fc6cafe680
keywords:
- SCSI ミニポート ドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- プラグ アンド プレイ WDK SCSI
- SCSI ミニポート ドライバーに変換します。
- SCSI ミニポート ドライバーの初期化
- SCSI ミニポート ドライバー WDK のストレージの初期化
- 順序に依存するコード WDK SCSI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a16725531c16dcfc7ab93182f8b569cfe2415f52
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368283"
---
# <a name="do-not-depend-on-order-of-scsi-miniport-initialization"></a>SCSI ミニポート初期化の順序への依存禁止


## <span id="ddk_do_not_depend_on_order_of_scsi_miniport_initialization_kg"></span><span id="DDK_DO_NOT_DEPEND_ON_ORDER_OF_SCSI_MINIPORT_INITIALIZATION_KG"></span>


一部のミニポート ドライバー PCI、EISA サーフィンなどのいくつかの別のシステム バス上の Hba をサポートします。 Microsoft Windows NT 4.0 で、このようなミニポート ドライバーの*HwScsiFindAdapter*ミニポート ドライバーと呼ばれる順序で呼び出された routine(s) [ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize). いくつかのケースでは、ミニポート ドライバーは、別の検出がされない場合がありますので、バスの種類を 1 つのカードの場所を追跡するためにこの使用されました。

たとえば、近づけ、PCI SCSI HBA も ISA バスにアクセスできます。 Windows NT 4.0 では、近づけ、ミニポート ドライバーはの追跡を初期化するために呼び出された PCI Hba と ISA バスの場所が表示されていました。 ミニポート ドライバーでは、スキップするのに I/O の範囲を判断するために、ISA のバスをスキャン中にこの情報を使用できます。

Windows 2000 以降では、この手法は信頼性の高いではなくなりました。 プラグ アンド プレイは初期化の順序を予測できないため、近づけ、ミニポート ドライバーは、PCI カードを初期化する前に、ISA のカードをスキャンする簡単に呼び出す可能性があります。 ミニポート ドライバーには、各 PCI HBA 2 回、システムのクラッシュを招く可能性があるが検出されます。

この場合、近づけ、HBA カードの実際のバスのインターフェイスを決定するために使用するコマンドがある場合、ISA バスをスキャンは見つかった各カードをクエリでした。 カードの PCI カードと ISA カードではない場合、し近づけ、ミニポート ドライバーはのままにプラグ アンド プレイを取得する要求を発行するまでに単独でします。

ミニポート ドライバーの順序に依存するコードを削除できない場合は、そので Windows 2000 以降のプラットフォームで従来、ドライバーとしてに実行する必要があります。

 

 




