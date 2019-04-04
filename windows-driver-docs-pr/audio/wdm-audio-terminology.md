---
title: WDM オーディオの用語
description: WDM オーディオの用語
ms.assetid: bb36a66a-84dc-46c2-adcb-761d0acec3a1
keywords:
- WDM オーディオ ドライバー WDK、WDM オーディオ ドライバーについて
- オーディオ ドライバー WDK、オーディオ ドライバーについて
- 一般的なドライバーのアーキテクチャの WDK オーディオ
- ミニポート ドライバー WDK オーディオの一般的な vs です。WDM オーディオ
- ポート ドライバー WDK オーディオの一般的な vs です。WDM オーディオ
- ミニドライバー WDK オーディオ
- バス ドライバー WDK オーディオ
- アダプターのドライバー WDK オーディオ
- クラス ドライバー WDK オーディオ
- 上端インターフェイス WDK オーディオ
- 下位 edge インターフェイスの WDK オーディオ
- スタックの WDK オーディオ
- ドライバー スタックの WDK オーディオ
- システム バス ドライバー WDK オーディオ
- サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da081c1b5fcbe3f4e74a17a818e41a13552dcb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577757"
---
# <a name="wdm-audio-terminology"></a>WDM オーディオの用語


## <span id="wdm_audio_terminology"></span><span id="WDM_AUDIO_TERMINOLOGY"></span>


このセクションでは、Microsoft Windows Driver Model (WDM) オーディオ ドライバーのアーキテクチャと一般的な階層型 Windows ドライバーのアーキテクチャでは、用語の違いについて説明します。 SCSI ポート/ミニポート ドライバーによって、汎用ドライバー アーキテクチャが典型的な例 (を参照してください[ストレージ ドライバーのアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff566978))。

ジェネリックと WDM オーディオ ドライバーのアーキテクチャによって定義されている用語は似ていますが、いくつかの重要な相違点を以下に示す必要が。

### <a name="span-idminiportdrivergenericspanspan-idminiportdrivergenericspanspan-idminiportdrivergenericspanminiport-driver-generic"></a><span id="Miniport_Driver__Generic_"></span><span id="miniport_driver__generic_"></span><span id="MINIPORT_DRIVER__GENERIC_"></span>ミニポート ドライバー (汎用)

ミニポート ドライバー (ジェネリック) は、(たとえば、PCI または ISA など) のシステム バス上に存在するアダプターのハードウェアに固有のドライバーです。 このドライバーは、1 つのエントリ ポイント[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)ポートのドライバーを使用した関数のテーブルを登録します。 この関数のテーブルは、ミニポート ドライバーの上端のインターフェイスとして機能します。

ミニポート ドライバーがドライバー スタックでポート ドライバーの下に配置されます。 つまり、ミニポート ドライバーのすべての呼び出しは、ポート ドライバーから行われ、ミニポート ドライバーからのすべての呼び出しは、ポート ドライバーの下位 edge インターフェイスには。

次の図は、用語の意味を示します*スタック*、*上端インターフェイス*、および*下 edge インターフェイス*このコンテキストで使用するためです。 ポートのドライバーを表すブロックはミニポート ドライバーを表すブロックの上に積み上げ横します。 そのため、ミニポート ドライバーでは、「スタック」でポート ドライバーの下に配置されます。

![ドライバー スタックの用語を示す図](images/drvstack.png)

ポートおよびミニポートのドライバーは、相互に公開されるソフトウェア インターフェイスを介して通信します。 上記の図では、これらのインターフェイスは、ポート ドライバーとミニポート ドライバーを表すブロックの上端を表すブロックの下端に関連付けられます。 この表現は、「低 edge インターフェイス」と「上端インターフェイス」のソースです。

### <a name="span-idportdrivergenericspanspan-idportdrivergenericspanspan-idportdrivergenericspanport-driver-generic"></a><span id="Port_Driver__Generic_"></span><span id="port_driver__generic_"></span><span id="PORT_DRIVER__GENERIC_"></span>ポート ドライバー (汎用)

(ジェネリック) のポート ドライバーには、ミニポート ドライバーが囲まれます。

ポート ドライバー:

-   WDM ストリーミングのフィルターを実装します。

-   オペレーティング システムの残りの部分に共通のインターフェイスを提供します。

-   システムからの I/O 要求を処理し、ミニポート ドライバーの関数のテーブルへの呼び出しとしてこれらの要求を recasts します。

-   ミニポート ドライバーのサポート関数 (ポート ドライバーの下位 edge インターフェイス) のライブラリを提供します。

ポート ドライバーは、ミニポート ドライバーからオペレーティング システムの詳細の多くを非表示にし、ミニポート ドライバー、ポート ドライバーから基になるハードウェアの詳細を非表示にします。 ポートのドライバーの実装は、別のオペレーティング システムのリリースの変更を行うこともできますが、ミニポート ドライバーにポート ドライバーのインターフェイスはより未満、変更なしにほとんどのプラットフォームに依存しないミニポート ドライバーを有効にします。

### <a name="span-idminidrivergenericspanspan-idminidrivergenericspanspan-idminidrivergenericspanminidriver-generic"></a><span id="Minidriver__Generic_"></span><span id="minidriver__generic_"></span><span id="MINIDRIVER__GENERIC_"></span>ミニドライバー (汎用)

(ジェネリック) のミニドライバーは、バス上のハードウェア コンポーネントを表します。 ミニドライバーは、バス経由で物理デバイスとの通信に、バス ドライバーを使用し、バス ドライバーと 1 つまたは複数のクラス ドライバーをまとめて、バインドします。

*クラスのドライバー*ヘルプ、ミニドライバーは、論理デバイスの種類としてクライアントに物理デバイスを表示します。 WDM 環境で、ミニドライバーは通常クラスのドライバーから IRP フォームで要求を受信し、バス ドライバーに IRP のフォームで要求を送信します。

ミニドライバーは、いくつかのクラス ドライバーとの通信にもあります。 複数のクラス ドライバーにバインドするミニドライバーの例では、IEEE 1394 バス上の CD-ROM ドライブ、ミニドライバーです。 ドライブは、ファイル システムからアクセスできるように、ファイル システム ドライバーにバインドがあります。 ただしもにバインドする、 [Redbook システム ドライバー](kernel-mode-wdm-audio-components.md#redbook_system_driver) Cd からオーディオをストリーミングできるようにします。

### <a name="span-idbusdrivergenericspanspan-idbusdrivergenericspanspan-idbusdrivergenericspanbus-driver-generic"></a><span id="Bus_Driver__Generic_"></span><span id="bus_driver__generic_"></span><span id="BUS_DRIVER__GENERIC_"></span>バス ドライバー (汎用)

(ジェネリック)、バス ドライバーでは、物理バスにミニドライバー アクセスを提供します。 Microsoft Windows*ハードウェア アブストラクション レイヤー (HAL)* とも呼ば、*システム バス ドライバー*システム バスへのアクセスを提供するためです。 詳細については、[バス ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff540704)を参照してください。

### <a name="span-idclassdrivergenericspanspan-idclassdrivergenericspanspan-idclassdrivergenericspanclass-driver-generic"></a><span id="Class_Driver__Generic_"></span><span id="class_driver__generic_"></span><span id="CLASS_DRIVER__GENERIC_"></span>クラスのドライバー (汎用)

(ジェネリック) のクラス ドライバーは、類似するデバイスのクラス間で共通する動作を実装します。

クラス ドライバー:

-   ハードウェア固有のドライバーの機能の重複を排除します。

-   バスに固有ではありません。

-   リソースの問題 (たとえば、DMA および割り込みなど) の認識しません。

### <a name="span-idminiportdriverwdmaudiospanspan-idminiportdriverwdmaudiospanspan-idminiportdriverwdmaudiospanminiport-driver-wdm-audio"></a><span id="Miniport_Driver__WDM_Audio_"></span><span id="miniport_driver__wdm_audio_"></span><span id="MINIPORT_DRIVER__WDM_AUDIO_"></span>ミニポート ドライバー (WDM オーディオ)

ミニポート ドライバー (WDM オーディオ) は、システム バス上に存在するオーディオ アダプター カードの関数の関数に固有のインターフェイスを実装します。 ミニポート ドライバーは、アダプタのドライバのコンポーネントです。 オペレーティング システムによってドライバーでことはありません。 この点で、オーディオのミニポート ドライバーは、ジェネリック ミニポート ドライバーによって異なります。

ジェネリックのミニポート ドライバーとは異なりオーディオ ミニポート ドライバーを実装しません[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)、登録されていないと、それぞれポート ドライバー サポートを完全に依存しないでください。 複数のオーディオのミニポート ドライバーが複数の関数のアドレスを 1 つのアダプターのドライバーにリンク (でき、1 つのデバイス オブジェクトに関連付けられている)。

### <a name="span-idadapterdriverwdmaudiospanspan-idadapterdriverwdmaudiospanspan-idadapterdriverwdmaudiospanadapter-driver-wdm-audio"></a><span id="Adapter_Driver__WDM_Audio_"></span><span id="adapter_driver__wdm_audio_"></span><span id="ADAPTER_DRIVER__WDM_AUDIO_"></span>アダプターのドライバー (WDM オーディオ)

アダプターのドライバー (WDM オーディオ) は、指定したアダプターに関連付けられているすべてのミニポート ドライバーのコンテナーとして機能します。 このアダプターのドライバーでは、ドライバーとしてオペレーティング システムによって認識され、独自の .sys ファイルに含まれます。

オーディオ ドライバーは、一連のミニポート ドライバーと初期化の問題に対応するコードを追加で構成されます。 たとえば、アダプターのドライバーを実装する、 [ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)エントリ ポイント。

### <a name="span-idportdriverwdmaudiospanspan-idportdriverwdmaudiospanspan-idportdriverwdmaudiospanport-driver-wdm-audio"></a><span id="Port_Driver__WDM_Audio_"></span><span id="port_driver__wdm_audio_"></span><span id="PORT_DRIVER__WDM_AUDIO_"></span>ポート ドライバー (WDM オーディオ)

ポート ドライバー (WDM オーディオ) では、ミニポート ドライバーに代わって KS フィルターを実装し、ポートのクラス ドライバーのコンテキストで動作します。 ポート ドライバーでは、システムに KS フィルターとして、ミニポート ドライバーの関数に固有のコードを公開してがアダプターに依存しない機能を実装する責任を負います。

汎用ポート ドライバーとは異なりオーディオ ポート ドライバーはデバイス オブジェクトを共有し、したがって、異なる方法でインスタンス化します。 類似するジェネリック クラス ドライバー (バスに依存しないではありません) デバイスのクラスの想定される動作を実装するという点では、汎用ポート ドライバーよりも、オーディオ ポート ドライバーもです。

### <a name="span-idportclassdriverwdmaudiospanspan-idportclassdriverwdmaudiospanspan-idportclassdriverwdmaudiospanport-class-driver-wdm-audio"></a><span id="Port_Class_Driver__WDM_Audio_"></span><span id="port_class_driver__wdm_audio_"></span><span id="PORT_CLASS_DRIVER__WDM_AUDIO_"></span>ポート クラス ドライバー (WDM オーディオ)

ポート クラス ドライバー (WDM オーディオ) は、さまざまな種類のオーディオ ハードウェア関数のサポートを提供のポートのドライバーのコレクションのコンテナーとして機能します。 次の図では、オーディオのポートのクラスとアダプターのドライバーの間のリレーションシップを示します。

![オーディオのポートのクラスとアダプターのドライバーの間の関係を示す図](images/wdmaumi.png)

アダプターのドライバーでは、いくつかの異なるハードウェア関数を含む可能性があるアダプター カードを管理します。 上記の図に示すように、アダプターのドライバーには、ハードウェアの機能の種類ごとの管理に、ミニポート ドライバーが含まれています。 同様に、ポートのクラス ドライバーは複数のハードウェア機能にアダプター カードのサポートを提供する設計されています。 ポート クラス ドライバーは、サポートされている適切に定義された関数型の各ポート ドライバーを提供します。 アダプターのドライバーでは、その関数の種類のポートに対応するドライバーを特定の関数に対して、ミニポート ドライバーをバインドします。 各関数のポートのドライバーでは、関数を使用している WDM オーディオ クライアントとの通信を処理します。 ミニポート ドライバーでは、その関数を管理するためのハードウェア固有のコードがすべて含まれます。

ポート クラス ドライバー (WDM オーディオ) は、主に、1 つのデバイス オブジェクトに関連付けられているサブデバイスを複数のコンテナーとして機能します。 バス ドライバーの作成、1 つ*物理デバイス オブジェクト (PDO)* プラグ アンド プレイ (PnP) ノードごとにそれらを列挙します。

PnP の単一のノードには、オーディオのアダプターの場合、複数のオーディオ関数頻繁に含まれています。 ノードに関連付けられた、個別のデバイスとして通常、さまざまな関数を公開するには、アダプター用のバス ドライバーの記述が必要です。 バス ドライバーでは、ハードウェアの機能を列挙し、対応する Pdo を作成します。 このシナリオで 1 つまたは複数の関数に固有のドライバーは、Pdo にバインドし、アダプターの共有リソースにアクセスするため、バス ドライバーとネゴシエートする必要があります。

ポート クラス ドライバーは、オペレーティング システムでは、個別のサブデバイスのセットとして、デバイスを認識する 1 つのデバイス オブジェクトのさまざまな側面を公開するのに、カーネル ドライバーの機能のストリーミングを使用します。

参照文字列は、目的のサブデバイスを指定する、デバイス名に追加されます。 カーネルのストリーミング ドライバーは Irp がこの参照文字列に基づく作成をディスパッチします。 ファイル オブジェクトを作成した後、サブデバイスを表すファイル オブジェクトを対象とする Irp のディスパッチ、カーネル ドライバーのストリーミングを提供します。 さらに、ポートのクラス ドライバーは、パッケージ化サブデバイスの COM ベースのモデルを実装します。

アダプターのドライバーがポート ドライバーとミニポート ドライバーをインスタンス化し、ポート ドライバーの初期化関数のパラメーターとして、ミニポート ドライバーにポインターを渡すことによって、それらをまとめてバインド (のコード例を参照してください[サブデバイス作成](subdevice-creation.md)。). 結果として得られるポート/ミニポート ドライバー スタックは、ポートのクラス ドライバーがサポートするサブデバイス型のいずれかを表す KS フィルターを構成します。

ポート クラス ドライバーの[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)関数は、システムの残りの部分によってデバイスとして認識されていると、サブデバイスを登録します。 ポート ドライバーでは、作成、デバイス オブジェクトが、サブデバイスが登録されている参照文字列で指定されている Irp のみを対象となる Irp を受信します。 ポート ドライバーは Irp をサブデバイスに関連付けられているファイル オブジェクトを対象としても受信します。 ポート ドライバーは、KS フィルターとサブデバイスのように動作し、ミニポート ドライバーを適切に通信するためです。

多機能オーディオ カードのドライバーを設計の詳細については、[多機能オーディオ デバイス](multifunction-audio-devices.md)を参照してください。

 

 




