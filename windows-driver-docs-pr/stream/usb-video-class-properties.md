---
title: USB ビデオ クラスのプロパティ
description: USB Video クラスのクライアントは、このトピックで説明する次のビデオキャプチャプロパティセットを使用できます。
ms.assetid: 6295926b-4ec5-42f5-98ca-a375d36f917b
keywords:
- USB ビデオクラスドライバー WDK AVStream、プロパティ
- ビデオクラスドライバー WDK USB、プロパティ
- UVC ドライバー WDK AVStream、プロパティ
- プロパティセット WDK USB ビデオクラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dae84f8a8162d842e71e30d835353dcb6ad1ede
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844655"
---
# <a name="usb-video-class-properties"></a>USB ビデオ クラスのプロパティ


USB Video クラスのクライアントは、次のビデオキャプチャのプロパティセットを使用できます。

[Propsetid\_VIDCAP\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)
[PROPSETID\_VIDCAP\_VIDEOPROCAMP](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp) 、USB ビデオクラスのクライアントは、フィルターまたは個々のノードで要求を行うことができます。 ノードベースのプロパティの機能は、事前 USB Video クラスのフィルターベースのプロパティと同じです。

ノードベースのプロパティを指定するには、プロパティ記述子の構造に含まれている[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)構造体の Flags メンバー (たとえば、 [**KSPROPERTY\_CAMERACONTROL\_node\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)) で、ksk プロパティ\_TYPE\_TOPOLOGY フラグに設定します。

クライアントは1つのフィルター上の複数のノードに対応できるため、USB ビデオクラスを使用すると、複数の独立したレンズがあるカメラをサポートできます。

さらに、新しいプロパティセットが定義されています。

[Propsetid\_VIDCAP\_SELECTOR](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-selector)PROPSETID\_VIDCAP\_SELECTOR に含まれるプロパティ項目はノードベースです。

[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)または**DeviceIoControl**を呼び出して、ユーザーモードコンポーネントからのプロパティ要求を作成します。 **DeviceIoControl**については、Microsoft Windows SDK のドキュメントを参照してください。

上記の4つのプロパティセットに含まれる各プロパティ項目には、DirectShow COM インターフェイスに対応するメソッドがあります。 メソッドの詳細については、Windows SDK の DirectShow のドキュメントを参照してください。

USB ビデオクラスデバイスは、上記のプロパティセットの一部またはすべてをサポートできます。

 

 




