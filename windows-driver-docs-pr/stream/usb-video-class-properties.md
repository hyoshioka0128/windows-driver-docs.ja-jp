---
title: USB ビデオ クラスのプロパティ
description: USB ビデオ クラスのクライアントは、このトピックで説明する次のビデオ キャプチャ プロパティ セットを使用できます。
ms.assetid: 6295926b-4ec5-42f5-98ca-a375d36f917b
keywords:
- USB ビデオ クラス ドライバー WDK AVStream、プロパティ
- ビデオのクラス ドライバー WDK USB、プロパティ
- UVC ドライバー WDK AVStream、プロパティ
- プロパティは、WDK USB ビデオ クラスを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1454f3a7107afaca69b26289bd3741af00c7024d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383138"
---
# <a name="usb-video-class-properties"></a>USB ビデオ クラスのプロパティ


USB ビデオ クラスのクライアントは、次のビデオ キャプチャ プロパティ セットを使用できます。

[PROPSETID\_しました\_CAMERACONTROL](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-cameracontrol)
[PROPSETID\_しました\_ビデオ プロシージャ アンプ](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-videoprocamp)USB ビデオ クラスのクライアントは、フィルターに要求を行うことができますまたは、個々 のノード。 ノード ベースのプロパティの機能は、事前 USB ビデオ クラスのフィルターに基づくプロパティのと同じです。

ノード ベースのプロパティを指定する設定、KSPROPERTY\_型\_トポロジ フラグのフラグのメンバーでは、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)プロパティ記述子に含まれている構造体構造体-たとえば、 [ **KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)します。

クライアントが複数のノードを 1 つのフィルターを処理できるため、USB ビデオ クラスにより、Ihv が個別に制御されたレンズを複数のカメラをサポートするために。

さらに、新しいプロパティ セットが定義されています。

[PROPSETID\_しました\_セレクター](https://docs.microsoft.com/windows-hardware/drivers/stream/propsetid-vidcap-selector) PROPSETID に含まれるプロパティ項目\_しました\_セレクターは、ノード ベースします。

呼び出す[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)または**DeviceIoControl**ユーザー モード コンポーネントからプロパティの要求を行います。 **DeviceIoControl** Microsoft Windows SDK ドキュメントに記載されています。

上記の 4 つのプロパティ セットに含まれるプロパティ項目の各操作により、DirectShow の COM インターフェイスに対応するメソッドがあります。 メソッドの詳細については、Windows SDK の DirectShow のドキュメントを参照してください。

USB ビデオ クラス デバイスには、いくつかサポートできるまたは上に示したすべてのプロパティ セット。

 

 




