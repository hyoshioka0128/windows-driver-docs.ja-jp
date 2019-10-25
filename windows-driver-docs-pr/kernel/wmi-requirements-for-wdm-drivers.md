---
title: WDM ドライバーについての WMI の要件
description: WDM ドライバーについての WMI の要件
ms.assetid: 8290e570-acd9-4047-bd0b-c1c74847f243
keywords:
- WMI WDK カーネル、WDM ドライバー
- WDM ドライバー WDK WMI
- Irp WDK WMI
- WDK WMI を要求する
- WMI WDK カーネル、要求
- データプロバイダー WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8b76759d6d80963c549b6cabade93963040d015
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835641"
---
# <a name="wmi-requirements-for-wdm-drivers"></a>WDM ドライバーについての WMI の要件





*データプロバイダー*として WMI に登録する irp を処理するドライバー。 システムによって提供されるストレージポートドライバー、クラスドライバー、および NDIS プロトコルドライバーは、このカテゴリに分類されます。 を WMI データプロバイダーとして登録する方法の詳細については、「 [wmi Data Provider と](registering-as-a-wmi-data-provider.md)しての登録」を参照してください。

Irp を処理しないドライバーは、単に WMI 要求をドライバースタック内の次の下位のドライバーに転送する必要があります。 次に下位のドライバーは、WMI に登録し、最初のドライバーの代わりに WMI 要求を処理します。 たとえば、SCSI ミニポートドライバーと NDIS ミニポートドライバーは、WMI プロバイダーとして登録し、対応するクラスドライバーに WMI データを提供できます。

クラスまたはポートドライバーに WMI データを提供するドライバーは、クラスまたはポートドライバーによって定義されているドライバータイプ固有の WMI インターフェイスをサポートする必要があります。 たとえば、SCSI ミニポートドライバーでは、[**ポート\_構成\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)の構造で、SRB\_\_機能を**TRUE** **に設定し**、scsi ポートドライバーからの WMI 要求を処理する必要があります。

同様に、カスタムデータブロックを定義する接続指向の NDIS ミニポートドライバーは、[サポートされている\_guid\_共同\_の OID\_GEN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-supported-guids)をサポートする必要があります。それ以外の場合、ndis は OID\_GEN から返された Oid と状態の表示を、ndis によって定義されている、NDIS に共通して認識される\_サポートされる\_リストにマップします。

以下のセクションでは、Irp を処理するドライバーで WMI をサポートする方法について説明します。

 

 




