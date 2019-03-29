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
ms.openlocfilehash: f8df290bb0aaedd7a7c19b63ce6ffc2485ed2daa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578286"
---
# <a name="usb-video-class-properties"></a>USB ビデオ クラスのプロパティ


USB ビデオ クラスのクライアントは、次のビデオ キャプチャ プロパティ セットを使用できます。

[PROPSETID\_しました\_CAMERACONTROL](https://msdn.microsoft.com/library/windows/hardware/ff567802)
[PROPSETID\_しました\_ビデオ プロシージャ アンプ](https://msdn.microsoft.com/library/windows/hardware/ff568122)USB ビデオ クラスのクライアントは、フィルターに要求を行うことができますまたは、個々 のノード。 ノード ベースのプロパティの機能は、事前 USB ビデオ クラスのフィルターに基づくプロパティのと同じです。

ノード ベースのプロパティを指定する設定、KSPROPERTY\_型\_トポロジ フラグのフラグのメンバーでは、 [ **KSPROPERTY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)プロパティ記述子に含まれている構造体構造体-たとえば、 [ **KSPROPERTY\_CAMERACONTROL\_ノード\_S**](https://msdn.microsoft.com/library/windows/hardware/ff564420)します。

クライアントが複数のノードを 1 つのフィルターを処理できるため、USB ビデオ クラスにより、Ihv が個別に制御されたレンズを複数のカメラをサポートするために。

さらに、新しいプロパティ セットが定義されています。

[PROPSETID\_しました\_セレクター](https://msdn.microsoft.com/library/windows/hardware/ff567810) PROPSETID に含まれるプロパティ項目\_しました\_セレクターは、ノード ベースします。

呼び出す[ **KsSynchronousDeviceControl** ](https://msdn.microsoft.com/library/windows/hardware/ff567142)または**DeviceIoControl**ユーザー モード コンポーネントからプロパティの要求を行います。 **DeviceIoControl** Microsoft Windows SDK ドキュメントに記載されています。

上記の 4 つのプロパティ セットに含まれるプロパティ項目の各操作により、DirectShow の COM インターフェイスに対応するメソッドがあります。 メソッドの詳細については、Windows SDK の DirectShow のドキュメントを参照してください。

USB ビデオ クラス デバイスには、いくつかサポートできるまたは上に示したすべてのプロパティ セット。

 

 




