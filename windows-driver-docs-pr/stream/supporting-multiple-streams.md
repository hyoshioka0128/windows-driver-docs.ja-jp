---
title: 複数ストリームのサポート
description: 複数ストリームのサポート
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- Stream.sys クラス ドライバー WDK Windows 2000 のカーネル、複数のストリーム
- ミニドライバー WDK Windows 2000 のカーネル、複数のストリームのストリーミング
- ミニドライバー WDK Windows 2000 カーネル ストリーミング、複数のストリーム
- 複数のストリーム WDK ストリーミング ミニドライバー
- ストリームの番号は、WDK のミニドライバーのストリーミングをサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30a21a50550c342800bccec215f152d2749cb6c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377763"
---
# <a name="supporting-multiple-streams"></a>複数ストリームのサポート





ミニドライバーでサポートするストリームを説明します。 その[ *StrMiniReceiveDevicePacket* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nc-strmini-phw_receive_device_srb) 、SRB への応答で、日常的な\_取得\_ストリーム\_情報要求。 **CommandData.StreamBuffer**を指す、 [ **HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_descriptor)構造で、ミニドライバーを入力する必要があります、ストリームのサポートの説明です。

ハードウェア ベース\_ストリーム\_記述子構造体の始まりを[ **HW\_ストリーム\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_header)構造体は、ストリームの数について説明します、ミニドライバーをサポートします。 配列が続く[ **HW\_ストリーム\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_information)構造体、それぞれが個別のストリームをについて説明します。 クラス ドライバーは、各ハードウェアを使用して\_ストリーム\_情報を処理するために、 [KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin) − 暗証番号 (pin) の ID 型として、配列内のインデックスのプロパティ セット

ハードウェア ベースのデータ、ほとんどのミニドライバーの\_ストリーム\_記述子は、コンパイル時に固定されます。 その場合は、ミニドライバーは、静的なデータ構造を割り当てることができます。

ミニドライバーは、ハードウェアのトポロジのメンバーを介してそのストリーム間の接続のトポロジをについて説明します\_ストリーム\_ヘッダー。 クラスのドライバーでは、この構造体を使用して、処理、 [KSPROPSETID\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)ミニドライバーのプロパティの設定。

 

 




