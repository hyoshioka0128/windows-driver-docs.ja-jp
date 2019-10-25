---
title: WDM オーディオの用語
description: WDM オーディオの用語
ms.assetid: bb36a66a-84dc-46c2-adcb-761d0acec3a1
keywords:
- WDM オーディオドライバー WDK、WDM オーディオドライバーについて
- オーディオドライバー WDK、オーディオドライバーについて
- 汎用ドライバーアーキテクチャ WDK オーディオ
- ミニポートドライバー WDK オーディオ、汎用および WDM オーディオ
- ポートドライバー WDK オーディオ、汎用および WDM オーディオ
- ミニドライバー WDK オーディオ
- バスドライバー WDK オーディオ
- アダプタードライバー WDK オーディオ
- クラスドライバー WDK オーディオ
- 最先端インターフェイス WDK audio
- 低エッジインターフェイスの WDK オーディオ
- スタック WDK オーディオ
- ドライバースタック WDK オーディオ
- システムバスドライバー WDK オーディオ
- サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01113712ce5c9c9aa67e1b90f4e832cb0493f3c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832248"
---
# <a name="wdm-audio-terminology"></a>WDM オーディオの用語


## <span id="wdm_audio_terminology"></span><span id="WDM_AUDIO_TERMINOLOGY"></span>


このセクションでは、Microsoft Windows Driver Model (WDM) オーディオドライバーアーキテクチャと汎用 Windows レイヤードドライバーアーキテクチャとの用語の違いについて説明します。 汎用ドライバーのアーキテクチャは、SCSI ポート/ミニポートドライバーによって例示されます (「[ストレージドライバーのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-driver-architecture)」を参照してください)。

Generic および WDM オーディオドライバーアーキテクチャで定義されている用語は似ていますが、以下に示すように、いくつかの重要な違いがあります。

### <a name="span-idminiport_driver__generic_spanspan-idminiport_driver__generic_spanspan-idminiport_driver__generic_spanminiport-driver-generic"></a><span id="Miniport_Driver__Generic_"></span><span id="miniport_driver__generic_"></span><span id="MINIPORT_DRIVER__GENERIC_"></span>ミニポートドライバー (汎用)

ミニポートドライバー (generic) は、システムバス上に存在するアダプターのハードウェア固有のドライバー (PCI や ISA など) です。 このドライバーは、エントリポイントと[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)を1つ持ち、関数のテーブルをポートドライバーに登録します。 この関数の表は、ミニポートドライバーの上端のインターフェイスとして機能します。

ミニポートドライバーは、ドライバースタックのポートドライバーの下に置かれます。 つまり、ミニポートドライバーへのすべての呼び出しはポートドライバーから行われ、ミニポートドライバーからのすべての呼び出しは、ポートドライバーの下端のインターフェイスに対して行われます。

次の図は、このコンテキストで使用される、用語*スタック*、*上部エッジインターフェイス*、および下端の*インターフェイス*の意味を示しています。 ポートドライバーを表すブロックは、ミニポートドライバーを表すブロックの上に積み重ねられます。 そのため、ミニポートドライバーは、"スタック" のポートドライバーの下にあります。

![ドライバースタックの用語を示す図](images/drvstack.png)

ポートとミニポートドライバーは、相互に公開されているソフトウェアインターフェイスを介して通信します。 上の図では、これらのインターフェイスは、ポートドライバーを表すブロックの下端と、ミニポートドライバーを表すブロックの上端に関連付けられています。 この表現は、"下端のインターフェイス" と "上端のインターフェイス" という用語のソースです。

### <a name="span-idport_driver__generic_spanspan-idport_driver__generic_spanspan-idport_driver__generic_spanport-driver-generic"></a><span id="Port_Driver__Generic_"></span><span id="port_driver__generic_"></span><span id="PORT_DRIVER__GENERIC_"></span>ポートドライバー (汎用)

ポートドライバー (汎用) は、ミニポートドライバーを囲みます。

ポートドライバー:

-   WDM ストリーミングフィルターを実装します。

-   オペレーティングシステムの残りの部分に共通のインターフェイスを提供します。

-   システムからの i/o 要求を処理し、これらの要求をミニポートドライバーの関数テーブルへの呼び出しとして処理します。

-   ミニポートドライバーに、サポート機能のライブラリ (ポートドライバーの下端のインターフェイス) を提供します。

ポートドライバーは、オペレーティングシステムの詳細の多くをミニポートドライバーから隠します。また、ミニポートドライバーは、基になるハードウェアの詳細をポートドライバーから隠します。 ポートドライバーの実装では、オペレーティングシステムのリリースごとに変更が行われる場合がありますが、ミニポートドライバーに対するポートドライバーのインターフェイスはそのままであるか、または低いため、ミニポートドライバーはプラットフォームに依存しません。

### <a name="span-idminidriver__generic_spanspan-idminidriver__generic_spanspan-idminidriver__generic_spanminidriver-generic"></a><span id="Minidriver__Generic_"></span><span id="minidriver__generic_"></span><span id="MINIDRIVER__GENERIC_"></span>ミニドライバー (ジェネリック)

ミニドライバー (generic) は、バス上のハードウェアコンポーネントを表します。 ミニドライバーはバスドライバーを使用してバスを介して物理デバイスと通信し、バスドライバーと1つ以上のクラスドライバーをバインドします。

*クラスドライバー*は、ミニドライバーが物理デバイスを論理デバイスの種類としてクライアントに提示するのに役立ちます。 WDM 環境では、ミニドライバーは通常、クラスドライバーから IRP 形式の要求を受け取り、IRP 形式の要求をバスドライバーに送信します。

ミニドライバーは、いくつかのクラスドライバーと通信する必要がある場合もあります。 複数のクラスドライバーにバインドするミニドライバーの例として、IEEE 1394 バス上の CD-ROM ドライブのミニドライバーがあります。 ファイルシステムドライバーにバインドして、ファイルシステムからドライブにアクセスできるようにすることができます。 ただし、オーディオを Cd からストリーミングできるように、 [Redbook システムドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver)にもバインドされています。

### <a name="span-idbus_driver__generic_spanspan-idbus_driver__generic_spanspan-idbus_driver__generic_spanbus-driver-generic"></a><span id="Bus_Driver__Generic_"></span><span id="bus_driver__generic_"></span><span id="BUS_DRIVER__GENERIC_"></span>バスドライバー (汎用)

バスドライバー (generic) は、物理バスへのミニドライバーアクセスを提供します。 Microsoft Windows*ハードウェアアブストラクションレイヤー (HAL)* は、システムバスへのアクセスを提供するため、*システムバスドライバー*と呼ばれることがあります。 詳細については、「[バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)」を参照してください。

### <a name="span-idclass_driver__generic_spanspan-idclass_driver__generic_spanspan-idclass_driver__generic_spanclass-driver-generic"></a><span id="Class_Driver__Generic_"></span><span id="class_driver__generic_"></span><span id="CLASS_DRIVER__GENERIC_"></span>クラスドライバー (ジェネリック)

クラスドライバー (ジェネリック) は、類似したデバイスのクラス全体で共通の動作を実装します。

クラスドライバー:

-   ハードウェア固有のドライバーの機能の重複を排除します。

-   はバス固有ではありません。

-   は、リソースの問題 (DMA や割り込みなど) を認識していません。

### <a name="span-idminiport_driver__wdm_audio_spanspan-idminiport_driver__wdm_audio_spanspan-idminiport_driver__wdm_audio_spanminiport-driver-wdm-audio"></a><span id="Miniport_Driver__WDM_Audio_"></span><span id="miniport_driver__wdm_audio_"></span><span id="MINIPORT_DRIVER__WDM_AUDIO_"></span>ミニポートドライバー (WDM オーディオ)

ミニポートドライバー (WDM オーディオ) は、システムバス上に存在するオーディオアダプターカード上の関数に対して関数固有のインターフェイスを実装します。 ミニポートドライバーは、アダプタードライバーのコンポーネントです。 オペレーティングシステムによってドライバーとして認識されません。 この点で、オーディオミニポートドライバーは汎用ミニポートドライバーとは異なります。

汎用ミニポートドライバーとは異なり、オーディオミニポートドライバーは[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)を実装しておらず、登録されていません。また、サポート用にそれぞれのポートドライバーに依存しません。 複数の関数に対応する複数のオーディオミニポートドライバーは、1つのアダプタードライバー (および1つのデバイスオブジェクトに関連付けられている) にリンクできます。

### <a name="span-idadapter_driver__wdm_audio_spanspan-idadapter_driver__wdm_audio_spanspan-idadapter_driver__wdm_audio_spanadapter-driver-wdm-audio"></a><span id="Adapter_Driver__WDM_Audio_"></span><span id="adapter_driver__wdm_audio_"></span><span id="ADAPTER_DRIVER__WDM_AUDIO_"></span>アダプタードライバー (WDM オーディオ)

アダプタードライバー (WDM オーディオ) は、特定のアダプターに関連付けられているすべてのミニポートドライバーのコンテナーとして機能します。 このアダプタドライバは、オペレーティングシステムによってドライバとして認識され、独自の .sys ファイルに含まれています。

オーディオアダプタードライバーは、一連のミニポートドライバーと、初期化の問題に対処する追加のコードで構成されています。 たとえば、アダプタードライバーは[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)エントリポイントを実装します。

### <a name="span-idport_driver__wdm_audio_spanspan-idport_driver__wdm_audio_spanspan-idport_driver__wdm_audio_spanport-driver-wdm-audio"></a><span id="Port_Driver__WDM_Audio_"></span><span id="port_driver__wdm_audio_"></span><span id="PORT_DRIVER__WDM_AUDIO_"></span>ポートドライバー (WDM オーディオ)

ポートドライバー (WDM オーディオ) は、ミニポートドライバーに代わって KS フィルターを実装し、ポートクラスドライバーのコンテキストで動作します。 ポートドライバーは、ミニポートドライバーの関数固有のコードを KS フィルターとしてシステムに公開し、アダプターに依存しない機能を実装します。

汎用ポートドライバーとは異なり、オーディオポートドライバーはデバイスオブジェクトを共有するため、異なる方法でインスタンス化されます。 オーディオポートドライバーは、汎用的なクラスドライバーに似ています。これは、一般的なポートドライバーが、デバイスのクラス (バスに依存しない) の動作を実装するということです。

### <a name="span-idport_class_driver__wdm_audio_spanspan-idport_class_driver__wdm_audio_spanspan-idport_class_driver__wdm_audio_spanport-class-driver-wdm-audio"></a><span id="Port_Class_Driver__WDM_Audio_"></span><span id="port_class_driver__wdm_audio_"></span><span id="PORT_CLASS_DRIVER__WDM_AUDIO_"></span>ポートクラスドライバー (WDM オーディオ)

ポートクラスドライバー (WDM オーディオ) は、ポートドライバーのコレクションのコンテナーとして機能し、それぞれが異なる種類のオーディオハードウェア機能のサポートを提供します。 次の図は、オーディオポートクラスとアダプタードライバーの関係を示しています。

![オーディオポートクラスとアダプタードライバーの関係を示す図](images/wdmaumi.png)

アダプタードライバーは、複数の異なるハードウェア機能を含む可能性のあるアダプターカードを管理します。 上の図に示すように、アダプタードライバーには、各種類のハードウェア機能を管理するためのミニポートドライバーが含まれています。 同様に、ポートクラスドライバーは、複数のハードウェア機能を備えたアダプターカードに対してサポートを提供するように設計されています。 Port クラス driver は、サポートする適切に定義された関数の種類ごとにポートドライバーを提供します。 アダプタードライバーは、特定の関数のミニポートドライバーを、その関数の種類の対応するポートドライバーにバインドします。 各関数のポートドライバーは、その関数を使用する WDM オーディオクライアントとの通信を処理します。 ミニポートドライバーには、その機能を管理するためのハードウェア固有のコードがすべて含まれています。

ポートクラスドライバー (WDM オーディオ) は、主に1つのデバイスオブジェクトに関連付けられている複数のサブデバイスのコンテナーとして機能します。 バスドライバーは、列挙するプラグアンドプレイ (PnP) ノードごとに1つの*物理デバイスオブジェクト (PDO)* を作成します。

オーディオアダプターの場合、1つの PnP ノードに複数のオーディオ機能が含まれることがよくあります。 ノードに関連付けられているさまざまな関数を個別のデバイスとして公開するには、通常、アダプターのバスドライバーを書き込む必要があります。 バスドライバーは、ハードウェア機能を列挙し、対応する PDOs を作成します。 このシナリオでは、1つまたは複数の関数固有のドライバーが、アダプター上の共有リソースにアクセスするために、PDOs にバインドし、バスドライバーとネゴシエートする必要があります。

Port クラスドライバーは、カーネルストリーミングドライバーの機能を使用して、オペレーティングシステムがデバイスを個別のサブデバイスのセットとして認識するように、1つのデバイスオブジェクトのさまざまな側面を公開します。

目的のサブデバイスを指定するために、デバイス名に参照文字列が追加されます。 カーネルストリーミングドライバーは、この参照文字列に基づいて作成 Irp をディスパッチします。 ファイルオブジェクトが作成された後、カーネルストリーミングドライバーは、サブデバイスを表すファイルオブジェクトを対象とする Irp のディスパッチを提供します。 また、ポートクラスドライバーは、サブデバイスをパッケージ化するための COM ベースのモデルを実装します。

アダプタードライバーは、ポートドライバーとミニポートドライバーをインスタンス化し、ポートドライバーの初期化関数のパラメーターとしてミニポートドライバーへのポインターを渡すことによって、それらをバインドします ([サブデバイスの作成](subdevice-creation.md)に関するコード例を参照してください)。 生成されたポート/ミニポートドライバースタックは、ポートクラスドライバーがサポートするサブデバイスの種類の1つを表す KS フィルターを構成します。

Port クラスドライバーの[**Pcregistersubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)関数は、サブデバイスを登録します。これは、システムの残りの部分でデバイスとして認識されます。 ポートドライバーは、デバイスオブジェクトを対象とした作成 Irp を受信しますが、サブデバイスが登録されている参照文字列で指定されている Irp に対してのみ使用されます。 また、ポートドライバーは、サブデバイスに関連付けられているファイルオブジェクトを対象とする Irp を受信します。 ポートドライバーは、サブデバイスの動作を KS フィルターとして、およびミニポートドライバーと適切に通信する役割を担います。

多機能オーディオカード用ドライバーの設計の詳細については、「[多機能オーディオデバイス](multifunction-audio-devices.md)」を参照してください。

 

 




