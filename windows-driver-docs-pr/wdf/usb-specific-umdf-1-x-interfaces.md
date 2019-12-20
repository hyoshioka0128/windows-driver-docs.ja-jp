---
title: USB 固有の UMDF 1.x インターフェイス
description: USB 固有の UMDF 1.x インターフェイス
ms.assetid: b458d96d-e15e-4a9b-a26e-490620cec38e
keywords:
- UMDF WDK、UMDF USB オブジェクトモデル
- ユーザーモードドライバーフレームワーク WDK、UMDF USB オブジェクトモデル
- ユーザーモードドライバー WDK UMDF、UMDF USB オブジェクトモデル
- UMDF-USB オブジェクトモデル WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c5d9acc49518fbbfe7edf37ab4ae6e118cd2d80
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210900"
---
# <a name="usb-specific-umdf-1x-interfaces"></a>USB 固有の UMDF 1.x インターフェイス


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

USB デバイスは、1つまたは複数の構成を持つことができます。 各構成には、1つまたは複数のインターフェイスを含めることができます。 各インターフェイスは、1つまたは複数の代替設定に関連付けられており、それぞれの代替設定によって1つ以上のエンドポイントが定義されます。 エンドポイントは、デバイスハードウェアのバッファーを表します。

パイプは、ホストコントローラーと現在の代替設定のエンドポイントとの間の接続をソフトウェアで抽象化したものです。 パイプは、i/o のターゲットにすることができ、 [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)インターフェイスによって UMDF で公開されます。

USB 固有の UMDF インターフェイスは、 [Winusb](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)アーキテクチャの上に構築されています。 WinUSB では、仕様により、複数の構成デバイスの最初の構成にのみアクセスできます。 そのため、WinUSB インターフェイスは、選択構成要求を送信する機能を公開しません。 その結果、UMDF の i/o ターゲット機能では、最初のデバイス構成以外のデバイス構成を選択することはできません。

USB 固有の UMDF インターフェイスには、一般的な USB モデルと同様のオブジェクト階層があります。 UMDF ドライバーは、 [IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)インターフェイスによって公開されるターゲットデバイスオブジェクトを作成します。 ドライバーは、IWDFUsbTargetDevice のメソッドを使用して、 [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)のインスタンスによって公開されている USB インターフェイスにアクセスできます。 ドライバーは IWDFUsbInterface メソッドを呼び出して、設定とエンドポイントを操作できます。

次の表は、USB 固有の UMDF インターフェイス階層を示しています。

| USB 固有の UMDF インターフェイス                    | 派生元                     |
|------------------------------------------------|----------------------------------|
| [IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) | [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) |
| [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)       | [IWDFObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)     |
| [IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)     | [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget) |

 

[IWDFUsbTargetDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)インターフェイスと[IWDFUsbTargetPipe](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)インターフェイスは[iwdfiotarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイスから派生しているため、i/o ターゲットオブジェクトを公開します。 [IWDFUsbInterface](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)インターフェイスは IWDFIoTarget (IWDFUsbInterface は[Iwdfobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)インターフェイスから派生) から派生していません。したがって、は i/o ターゲットオブジェクトを公開しません。 インターフェイスの詳細を検出して操作するために送信された i/o は、ターゲットデバイスに送信されます。

単純な UMDF ベースの USB クライアントドライバーを記述する手順の詳細については、「[最初の usb クライアントドライバー (umdf) を作成する方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

UMDF ベースの USB クライアントドライバーに必要なソースコードについては、「 [usb クライアントドライバーコードの構造 (umdf)](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)について」を参照してください。

 

 





