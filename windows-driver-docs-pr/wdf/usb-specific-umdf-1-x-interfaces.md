---
title: 特定の USB UMDF 1.x インターフェイス
description: 特定の USB UMDF 1.x インターフェイス
ms.assetid: b458d96d-e15e-4a9b-a26e-490620cec38e
keywords:
- UMDF WDK、UMDF USB オブジェクト モデル
- ユーザー モード ドライバー フレームワーク WDK、UMDF USB オブジェクト モデル
- ユーザー モード ドライバー WDK UMDF、UMDF USB オブジェクト モデル
- オブジェクト モデルの UMDF USB WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90b45c2193ed3b0395b4947786b393f68947e025
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537559"
---
# <a name="usb-specific-umdf-1x-interfaces"></a>特定の USB UMDF 1.x インターフェイス


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

USB デバイスは、1 つまたは複数の構成を持つことができます。 各構成には、1 つまたは複数のインターフェイスを持つことができます。 各インターフェイスに関連付けられている 1 つまたは複数の代替設定し、各代替の設定が 1 つまたは複数のエンドポイントを定義します。 エンドポイントは、デバイスのハードウェア上のバッファーを表します。

パイプは、ホスト コント ローラーと代替の現在の設定でエンドポイント間の接続のソフトウェアの抽象化です。 パイプは、I/O のターゲットにすることができ、によって UMDF で公開されている、 [IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)インターフェイス。

上に構築された特定の USB UMDF インターフェイス、 [WinUSB](https://msdn.microsoft.com/library/windows/hardware/ff540196)アーキテクチャ。 仕様は、WinUSB は、複数のデバイス構成の最初の構成にのみアクセスを許可します。 したがって、WinUSB インターフェイスでは、選択構成要求を送信する機能は公開されません。 その結果、UMDF に I/O ターゲット機能では、先頭以外の任意のデバイス構成の選択はできません。

USB 固有 UMDF インターフェイスでは、一般的な USB モデルに似ていますが、オブジェクトの階層があります。 UMDF ドライバーによって公開される、ターゲット デバイス オブジェクトを作成し、 [IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362)インターフェイス。 ドライバーのインスタンスによって公開されている USB インターフェイスへのアクセスに IWDFUsbTargetDevice のメソッドを使用できますし、 [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)します。 ドライバーは、設定とエンドポイントを操作する IWDFUsbInterface メソッドを呼び出すことができます。

次の表は、USB 固有 UMDF インターフェイスの階層構造を示しています。

| 特定の USB UMDF インターフェイス                    | 派生元                     |
|------------------------------------------------|----------------------------------|
| [IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362) | [IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170) |
| [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)       | [IWDFObject](https://msdn.microsoft.com/library/windows/hardware/ff560200)     |
| [IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)     | [IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170) |

 

[IWDFUsbTargetDevice](https://msdn.microsoft.com/library/windows/hardware/ff560362)と[IWDFUsbTargetPipe](https://msdn.microsoft.com/library/windows/hardware/ff560391)インターフェイスから派生、 [IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170)インターフェイスし、そのため、I/O のターゲット オブジェクトを公開します。 [IWDFUsbInterface](https://msdn.microsoft.com/library/windows/hardware/ff560312)インターフェイスが IWDFIoTarget から派生していません (から派生した IWDFUsbInterface、 [IWDFObject](https://msdn.microsoft.com/library/windows/hardware/ff560200)インターフェイス) と、したがって、I/O のターゲット オブジェクトは公開されません。 検出し、インターフェイスの詳細の操作に送信されるすべての I/O は、ターゲット デバイスに送信されます。

単純な UMDF ベースの USB クライアント ドライバーの記述に関する詳細な手順は、次を参照してください。 [、最初の USB クライアント ドライバー (UMDF) を書き込む方法](https://msdn.microsoft.com/library/windows/hardware/hh706184)します。

UMDF ベースの USB クライアント ドライバーに必要なソース コードについては、次を参照してください。 [USB クライアント ドライバー コード構造 (UMDF) について](https://msdn.microsoft.com/library/windows/hardware/hh770893)します。

 

 





