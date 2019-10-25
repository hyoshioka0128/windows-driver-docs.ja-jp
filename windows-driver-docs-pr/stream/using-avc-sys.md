---
title: Avc.sys の使用
description: Avc.sys の使用
ms.assetid: 3b4ec139-ff01-40bd-8e29-92f554180585
keywords:
- Avc 関数ドライバー WDK、Avc 関数ドライバーについて
- AV/C WDK、Avc の使用
- サブユニットは WDK AV/C をサポートします
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f697fc5c418de4515ab45ee46e68f3d2ef97f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841656"
---
# <a name="using-avcsys"></a>Avc.sys の使用





Windows が*avc*を読み込んで初期化した後、avc は標準の Av/c ユニットとサブユニットコマンドを使用して、IEEE 1394 バスに接続されているすべての Av/c デバイス上のアクティブなサブユニットを検出します (コンピューターが仮想 AV である場合は、virtual サブユニットを含む) *。* /C 単位)。 次に、すべてのアクティブなサブユニットに対してデバイス識別子 (IDs) が生成さ*れます*。 次に、 *Avc*は標準のプラグアンドプレイ (PnP) メカニズムを使用して、各サブシステムに適切なサブユニットドライバーを読み込みます。 読み込まれるサブユニットドライバーは、サブシステムドライバーをインストールする INF ファイルと、 *Avc*によって生成されるサブユニットのデバイス id に基づいて選択され、「 [AV/C デバイス id](av-c-device-identifiers.md)」で説明されています。 デバイス id は、サブユニットの***SubunitType***および***SubunitID***フィールドと組み合わせて、AV/C デバイスのユニット情報から生成されます。 サブユニットをサポートするドライバーは、ベンダー固有のものにすることも、サブユニットの種類に対して汎用的なものにすることもできます。 たとえば、ほとんどの DV ビデオカメラのサブユニットドライバーは、Microsoft が提供する*Msdv. sys*です。

サブシステムドライバーは、WDM アーキテクチャに基づくすべてのドライバーによって使用される標準の IRP ベースのメカニズムによって、 *Avc*と通信します。 サブシステムドライバーは、Irp/c プロトコルドライバー ( *Avc*) に対して irp を割り当ててドライバースタックに送信することで、その Av/c サブユニットと通信します。 I/o 要求を行うには、Microsoft Windows Driver Kit (WDK) に付属しているヘッダーファイル*Avc. h*をインクルードします。

サブシステムドライバーは、 *Avc*によって処理される irp を割り当て、初期化します。 サブユニットドライバーは、必要な AV/C 操作に対応する IOCTL に、IRP の**DeviceIoControl**のメンバーを設定します。

*Avc*は、2つの[デバイスインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)のいずれかを登録します。これは、どのサブシステムドライバースタックが読み込まれたか (ピアまたは仮想) によって異なります。 これらのインターフェイスは、サブ*システム*ドライバー、その他のドライバー、および使用するアプリケーションについて、Avc によってエクスポートされる機能を定義します。 次に、ドライバーの PnP 状態に従って、インターフェイスの状態を有効または無効に変更し*ます*。

*Avc*は、外部 AV/C サブユニット (ピアスタック) のサポートを提供するために読み込まれた場合に、GUID\_AVC\_クラスの新しいインスタンスを登録します。 このインターフェイスは、次の i/o 制御 (IOCTL) コードのみをサポートしています。

-   [**IOCTL\_AVC\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

IOCTL\_AVC\_クラスでは、複数の関数コードがサポートされています。 ピアサブユニットをサポートするために、 *Avc*のインスタンスの子ドライバーは、親デバイスオブジェクトを介してこのインターフェイスにアクセスできることが保証されています。

GUID\_AVC\_クラスインターフェイスは、すべての IOCTL\_AVC\_クラス関数コードをサポートしていますが、各関数のリファレンスページで説明されているように、使用に制限があります。

サブユニットは、仮想\_AVC\_クラスが読み込まれた場合、そのクラス\_の新しいインスタンスを登録して、仮想 AV/C (仮想スタック) をサポートできるようにし*ます*。 このインターフェイスは、次の4つの i/o 制御 (IOCTL) コードをサポートしています。

-   [**IOCTL\_AVC\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_class)

-   [**IOCTL\_AVC\_更新\_仮想\_サブユニット\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_update_virtual_subunit_info)

-   [**IOCTL\_AVC\_\_仮想\_サブユニット\_情報を削除します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_remove_virtual_subunit_info)

-   [**IOCTL\_AVC\_BUS\_リセット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ni-avc-ioctl_avc_bus_reset)

GUID\_VIRTUAL\_AVC\_クラスインターフェイスは、すべての IOCTL\_AVC\_クラス関数コードをサポートしていません。 個々の関数コードのリファレンスページでは、各関数コードがサポートされているかどうかを指定します。このページでは、 *avc*の\_仮想\_AVC\_クラスのインスタンスが使用されます。

IOCTL\_AVC\_クラスの Irp は、 [**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)を介して、カーネルモード (通常はドライバー間通信) でのみサポートされます。 そのため、アプリケーションは、IOCTL\_AVC\_クラスの IOCTL コードによって提供される関数に直接アクセスすることはできません。

最後の3つの IOCTL コードは、カーネルモードとユーザーモードの両方で、 [**IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)でサポートされています。 これは、アプリケーションがこれらの Ioctl を*Avc*に直接送信できることを意味します。

IOCTL\_AVC\_クラスの ioctl コードには、常に i/o 要求ブロック (IRB) が付随している必要があります。これにより、実行する AV/C 操作がさらに説明されます。 IRB ヘッダーには、IRB の残りの部分の構造を決定する関数番号が含まれています。 IRB 構造体とサイズは、関数によって異なります。 Avc は、次の2つのカスタム IRBs*を使用します*。

-   [**AVC\_コマンド\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_command_irb)

-   [**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)

サブユニットドライバーが使用する必要がある IRB の選択は、目的の関数によって異なります。 Avc でサポートされている IOCTL\_AVC\_クラス関数コードの詳細については、「 [AV/C プロトコルドライバーの関数コード](https://docs.microsoft.com/windows-hardware/drivers/stream/av-c-protocol-driver-function-codes)」*を*参照してください。

サブメニュードライバーによって使用されるプライマリ AV/C 関数は、avc [ **\_function\_コマンド**](https://docs.microsoft.com/windows-hardware/drivers/stream/avc-function-command)であり、AVC\_コマンド\_IRB 構造体を使用します。 **AVC\_関数\_コマンド**は、Av/c 要求を送信し、対応する Av/c 応答を受信します。 AV/C コマンドのビルドの詳細は、 *Avc*によって処理されますが、サブシステムドライバーは、各コマンドの Av/c オペコードとオペランドを提供する必要があります。

 

 




