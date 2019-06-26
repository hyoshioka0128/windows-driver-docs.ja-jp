---
title: サポートされるプロパティ セット
description: サポートされるプロパティ セット
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルでは、プロパティの設定します。
- ミニドライバー WDK Windows 2000 のカーネルをストリーミングするには、プロパティの設定します。
- WDK Windows 2000 のカーネル ストリーミング ミニドライバー、プロパティの設定します。
- プロパティは、WDK ストリーミング ミニドライバーを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96754871919410a9b6094368ac0ab12155757d43
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377753"
---
# <a name="supporting-property-sets"></a>サポートされるプロパティ セット





全体として、両方のミニドライバーと個別のストリームは、プロパティの要求を受信できます。 サポートするプロパティ セットを提供する、ミニドライバー、 **DevicePropertiesArray**の[ **HW\_ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)します。 各ストリームでは、プロパティ セットを提供する、 **StreamPropertiesArray**の[ **HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)構造体そのストリーム。

ミニドライバーを通じて処理プロパティのセットを定義する、 [ **KSPROPERTY\_設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_set)データ構造体の配列を指す順番[ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)構造、プロパティ セット内の各プロパティのいずれか。 場合、 **GetSupported** KSPROPERTY のメンバー\_項目が**TRUE**プロパティ データを取得するミニドライバーがサポートされます。 場合、 **SetSupported** KSPROPERTY のメンバー\_項目が**TRUE**プロパティ データを設定するミニドライバーがサポートされます。

KSPROPERTY で提供情報、ミニドライバーを使用してほとんどのプロパティのサポートを要求クラス ドライバーによって自動的に処理されます、\_プロパティの項目の構造体。 たとえば、次のクラス ドライバーの受信、KSPROPERTY\_型\_BASICSUPPORT が要求内のデータの型と値の範囲を検索、**値**KSPROPERTY のメンバー\_項目。 参照してください[ **KSPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksproperty_item)詳細についてはします。 ミニドライバーは、カスタムを実行する必要がある場合 (これはまれです)、サポート要求の処理、設定、 **SupportHandler** KSPROPERTY のメンバー\_項目を**TRUE**します。 プロパティの get 要求の場合と同様、クラス ドライバーは、サポート要求を処理します。 ミニドライバーは、要求からの実際の型を判断できます、**フラグ**プロパティの識別子のメンバー。

クラスのドライバーを取得または渡すことによってミニドライバー プロパティを設定、 [ **SRB\_取得\_デバイス\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-get-device-property)または[ **SRB\_設定\_デバイス\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/stream/srb-set-device-property)ミニドライバーへの要求[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb)ルーチン。 クラス ドライバーを取得または設定では、プロパティをストリーム、SRB を渡すことによって\_取得\_ストリーム\_プロパティまたは SRB\_設定\_ストリーム\_プロパティ要求ストリームの**StrMiniReceiveStreamControlPacket**ルーチン。

クラス ドライバーは、ミニドライバーのコールバックのいずれかを通じてミニドライバーから不定期の支援をミニドライバーに代わって、多くのプロパティを処理します。 ミニドライバーは、そのプロパティ セットの配列でこれらのプロパティを定義しません。 クラスのドライバーを処理する方法の詳細については、 [KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)と[KSPROPSETID\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティのセットを参照してください[複数サポートしています。ストリーム](supporting-multiple-streams.md)します。

 

 




