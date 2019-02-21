---
title: プロパティのセットをサポート
description: プロパティのセットをサポート
ms.assetid: 49a3e3e6-3a09-4202-a2cb-df65806d3336
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネルでは、プロパティの設定します。
- ミニドライバー WDK Windows 2000 のカーネルをストリーミングするには、プロパティの設定します。
- WDK Windows 2000 のカーネル ストリーミング ミニドライバー、プロパティの設定します。
- プロパティは、WDK ストリーミング ミニドライバーを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25b00f3143c814c4390bd577864ee6f8d85554ea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556946"
---
# <a name="supporting-property-sets"></a>プロパティのセットをサポート





全体として、両方のミニドライバーと個別のストリームは、プロパティの要求を受信できます。 サポートするプロパティ セットを提供する、ミニドライバー、 **DevicePropertiesArray**の[ **HW\_ストリーム\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff559690)します。 各ストリームでは、プロパティ セットを提供する、 **StreamPropertiesArray**の[ **HW\_ストリーム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff559692)構造体そのストリーム。

ミニドライバーを通じて処理プロパティのセットを定義する、 [ **KSPROPERTY\_設定**](https://msdn.microsoft.com/library/windows/hardware/ff565617)データ構造体の配列を指す順番[ **KSPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff565176)構造、プロパティ セット内の各プロパティのいずれか。 場合、 **GetSupported** KSPROPERTY のメンバー\_項目が**TRUE**プロパティ データを取得するミニドライバーがサポートされます。 場合、 **SetSupported** KSPROPERTY のメンバー\_項目が**TRUE**プロパティ データを設定するミニドライバーがサポートされます。

KSPROPERTY で提供情報、ミニドライバーを使用してほとんどのプロパティのサポートを要求クラス ドライバーによって自動的に処理されます、\_プロパティの項目の構造体。 たとえば、次のクラス ドライバーの受信、KSPROPERTY\_型\_BASICSUPPORT が要求内のデータの型と値の範囲を検索、**値**KSPROPERTY のメンバー\_項目。 参照してください[ **KSPROPERTY\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff565176)詳細についてはします。 ミニドライバーは、カスタムを実行する必要がある場合 (これはまれです)、サポート要求の処理、設定、 **SupportHandler** KSPROPERTY のメンバー\_項目を**TRUE**します。 プロパティの get 要求の場合と同様、クラス ドライバーは、サポート要求を処理します。 ミニドライバーは、要求からの実際の型を判断できます、**フラグ**プロパティの識別子のメンバー。

クラスのドライバーを取得または渡すことによってミニドライバー プロパティを設定、 [ **SRB\_取得\_デバイス\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff568170)または[ **SRB\_設定\_デバイス\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff568204)ミニドライバーへの要求[ *StrMiniReceiveDevicePacket* ](https://msdn.microsoft.com/library/windows/hardware/ff568463)ルーチン。 クラス ドライバーを取得または設定では、プロパティをストリーム、SRB を渡すことによって\_取得\_ストリーム\_プロパティまたは SRB\_設定\_ストリーム\_プロパティ要求ストリームの**StrMiniReceiveStreamControlPacket**ルーチン。

クラス ドライバーは、ミニドライバーのコールバックのいずれかを通じてミニドライバーから不定期の支援をミニドライバーに代わって、多くのプロパティを処理します。 ミニドライバーは、そのプロパティ セットの配列でこれらのプロパティを定義しません。 クラスのドライバーを処理する方法の詳細については、 [KSPROPSETID\_Pin](https://msdn.microsoft.com/library/windows/hardware/ff566584)と[KSPROPSETID\_トポロジ](https://msdn.microsoft.com/library/windows/hardware/ff566598)プロパティのセットを参照してください[複数サポートしています。ストリーム](supporting-multiple-streams.md)します。

 

 




