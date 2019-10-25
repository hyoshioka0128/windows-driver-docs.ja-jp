---
title: 複数ストリームのサポート
description: 複数ストリームのサポート
ms.assetid: 89f79078-129a-44cc-8b7e-5f5c1c33a473
keywords:
- .Sys クラスドライバー WDK Windows 2000 カーネル、複数ストリーム
- streaming ミニドライバー WDK Windows 2000 カーネル、複数ストリーム
- ミニドライバー WDK Windows 2000 カーネルストリーミング、複数ストリーム
- 複数のストリームの WDK streaming ミニドライバー
- サポートされる WDK streaming ミニドライバーのストリーム番号
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19780e8a065963f21aaa59c012fb9e3fd912ecf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837667"
---
# <a name="supporting-multiple-streams"></a>複数ストリームのサポート





ミニドライバーは、SRB\_GET\_STREAM\_INFO 要求に応答して、その[*Strminireceivedevicepacket*](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nc-strmini-phw_receive_device_srb)ルーチンでサポートされるストリームを記述します。 **Commanddata. StreamBuffer**は、 [**HW\_ストリーム\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_descriptor)の構造体を指します。これは、ミニドライバーがサポートしているストリームの説明を入力する必要があります。

HW\_ストリームの\_記述子の構造は、[**ハードウェア\_ストリーム\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_header)構造体で始まります。これは、ミニドライバーがサポートするストリームの数を示します。 その後に、各ストリームを記述する[**HW\_stream\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_information)構造体の配列が続きます。 クラスドライバーは、各 HW\_ストリームの\_情報を使用して、 [Ksk Propsetid\_ピン](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)のプロパティセットを処理します。配列内のインデックスは、pin の種類の ID として機能します。

ほとんどのミニドライバーでは、ハードウェア\_ストリーム\_記述子のデータはコンパイル時に固定されています。 この場合、ミニドライバーはデータ構造を静的に割り当てることができます。

ミニドライバーは、HW\_STREAM\_ヘッダーのトポロジメンバーを介して、そのストリーム間の接続のトポロジを記述します。 クラスドライバーは、この構造体を使用して、ミニドライバーに設定されている[Ksk Propsetid\_トポロジ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-topology)プロパティを処理します。

 

 




