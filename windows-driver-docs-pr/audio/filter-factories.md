---
title: フィルター ファクトリ
description: フィルター ファクトリ
ms.assetid: e836f941-274f-4e27-8069-753ef9ef2a06
keywords:
- オーディオフィルター WDK オーディオ、フィルターファクトリ
- ファクトリ WDK オーディオをフィルター処理する
- WDK オーディオ、ファクトリをフィルター処理します
- KS WDK オーディオ、フィルターファクトリのフィルター処理
- オーディオジャック WDK
- スピーカー WDK オーディオ、フィルターファクトリ
- フィルターのインスタンス化 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ce48e86dede6b17e3e80836058ab5b9974a1edb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833375"
---
# <a name="filter-factories"></a>フィルター ファクトリ


## <span id="filter_factories"></span><span id="FILTER_FACTORIES"></span>


オーディオアダプタードライバーは、フィルターファクトリを提供してフィルターのインスタンス化を管理します。 各フィルターファクトリは、特定の型の1つ以上の KS フィルターをインスタンス化できます。 フィルターの種類が特定のハードウェア機能をカプセル化している場合、ファクトリがインスタンス化できるその型のフィルターの数は、基になるハードウェアリソースによって制限されます。

フィルターファクトリは主に独立したハードウェア機能ブロックを管理するため、各フィルターファクトリはデバイスドライバーとして独自の権限を持つものと見なすことができます。 実際には、前の段落で使用されているという用語アダプタードライバーは、アダプターカード上のさまざまなハードウェア機能を管理するためにパッケージ化された関連ドライバー (フィルターファクトリ) のコレクションを指します。

他の Microsoft Windows Driver Model (WDM) ドライバーと同様に、フィルターファクトリは電源管理とセットアップ機能を処理します。 インストール中、ドライバーの INF ファイルによって1つまたは複数のフィルターデバイス名が登録されます (「[デバイス識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings)」を参照してください)。 このプロセスでは、システムレジストリに名前が読み込まれ、各フィルターファクトリが1つまたは複数の KS フィルターカテゴリに関連付けられます。詳細については、「[オーディオアダプターのデバイスインターフェイスのインストール](installing-device-interfaces-for-an-audio-adapter.md)」を参照してください。 すべてのオーディオデバイスは KSCATEGORY\_AUDIO に分類されますが、オーディオデバイスは KSCATEGORY\_RENDER (オーディオレンダリングデバイスの場合) または KSCATEGORY\_CAPTURE (オーディオキャプチャの場合) などの追加のカテゴリで分類される場合もあります。デバイス)。 ドライバーは、デバイスのフィルターを登録するさまざまなカテゴリを使用して、デバイスの一般的な機能をアドバタイズします。 たとえば、 [sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)が特定の種類のオーディオデバイスを必要とする場合、適切なカテゴリに分類されるデバイスのレジストリを検索します。

オペレーティングシステムは、「[デバイスのインストールコンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)」で説明されているセットアップ API を使用して、レジストリ内のすべての KSCATEGORY\_オーディオフィルターファクトリを検出して列挙します。 各ファクトリのレジストリエントリは、フィルターファクトリのフレンドリ名とそのデバイス名の両方を指定します。これは、フィルターをインスタンス化するファイルの作成呼び出しにクライアントが渡す長い文字列です。 この呼び出しは、カーネルモードからの[**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile) 、またはユーザーモードからの**CreateFile**に対して行われる場合があります。 フィルターはカーネルモードオブジェクトであり、カーネルハンドルによって識別されます。 ファイルの作成呼び出しでは、クライアントがフィルターを参照するために使用できるインスタンスハンドルが返されます。 オーディオグラフのユーザーモードクライアントまたは上流フィルターでは、このハンドルを使用して、IOCTL 要求をフィルターに送信または転送できます。 **CreateFile**の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

典型的な WDM オーディオアダプターカードは、たとえば PCI バス上に存在することがあります。また、には、wave データをレンダリングまたはキャプチャするための i/o コネクタがいくつか含まれています。 このカードの1つのオーディオデバイスには、スピーカーと lineout ケーブルのセットを運転するアナログオーディオ出力ジャックと、マイクと linein ケーブルから信号を受信するためのアナログオーディオ入力ジャックが含まれている場合があります。 WDM オーディオシステムは、デバイスをフィルターとして表し、オーディオジャックをそのフィルターのピンとして表します。

オーディオデバイスのフィルターは、個別のポートとミニポートドライバーとして実装されます。これらのドライバーは、連携して動作するために結合されます。

-   ミニポートドライバーには、ハードウェア固有のコードが含まれています。

-   ポートドライバーには、特定の種類のすべてのフィルターに共通の汎用コードが含まれています。

ベンダーは、フィルターがオーディオハードウェアを管理するために必要なすべての専用コードを含むミニポートドライバーを書き込みます。 オペレーティングシステムには、PortCls システムドライバー (Portcls を介してアクセスできるポートドライバーが用意されています。[ポートクラスアダプタードライバーおよび PortCls システムドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver)を参照してください)。 フィルター実装をポートとミニポートドライバーに分割することで、独自のデバイス用のドライバーを作成する作業が容易になります。

フィルターファクトリは、フィルターをインスタンス化するときに、まずフィルターのミニポートドライバーオブジェクトを作成します。 フィルターファクトリは、適切なポートオブジェクトのインスタンスを作成し、そのインスタンスにミニポートドライバーオブジェクトをバインドして、完全に機能するフィルターを形成します。 [サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、明確に定義されたソフトウェアインターフェイスを介して相互に通信します。 これらのインターフェイスの詳細については、「[ミニポートインターフェイス](miniport-interfaces.md)」と「[デバイスのサポート](supporting-a-device.md)」を参照してください。

オーディオフィルターは、基になるオーディオデバイスの構造を、ピンファクトリ、ノード、および内部接続のコレクションとして公開します。 ミニポートドライバーは、この情報をフィルター記述子に統合します。これは、 [**Pcfilter\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcfilter_descriptor)型の構造体です。 この構造には、フィルターのファクトリ、ノード、および内部接続の個々の記述子が含まれています。 これらの記述子は、次の型の構造体です。

[**PCPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)

[**PCNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcnode_descriptor)

[**PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))

ミニポートドライバーからフィルター記述子を取得するために、ポートドライバーは[**IMiniport:: GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-getdescription)メソッドを呼び出します。

ドライバーが PCFILTER\_記述子の構造を設定する方法の例については、Windows Driver Kit (WDK) の sb16 サンプルオーディオドライバーのヘッダーファイル .h を参照してください。

 

 




