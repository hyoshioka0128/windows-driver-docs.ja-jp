---
title: フィルター ファクトリ
description: フィルター ファクトリ
ms.assetid: e836f941-274f-4e27-8069-753ef9ef2a06
keywords:
- オーディオ フィルター WDK オーディオ フィルター ファクトリ
- フィルター ファクトリ WDK オーディオ
- WDK のオーディオ、ファクトリをフィルター処理します。
- KS は、WDK オーディオ、フィルター ファクトリをフィルター処理します。
- WDK のオーディオ ジャック
- スピーカー WDK オーディオ フィルター ファクトリ
- フィルターの WDK オーディオをインスタンス化します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d9f3a317b9d5869f8b3db4f4b380f1884441bf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360027"
---
# <a name="filter-factories"></a>フィルター ファクトリ


## <span id="filter_factories"></span><span id="FILTER_FACTORIES"></span>


オーディオ ドライバーは、フィルターをインスタンス化を管理するフィルター ファクトリを提供します。 各フィルター ファクトリは、特定の種類の 1 つ以上の KS フィルターをインスタンス化できます。 フィルターの種類には、特定のハードウェア機能がカプセル化する場合、ファクトリがインスタンス化できる型のフィルターの数は、基になるハードウェア リソースによって制限されます。

フィルター ファクトリがハードウェアの機能の大部分に自律的なブロックを管理するため、各フィルター ファクトリは、自身の権限のデバイス ドライバーを検討できます。 実際には、関連するドライバーは--のコレクションとは、前の段落で使用されるため、アダプターのドライバーでは、--ファクトリがアダプター カードでさまざまなハードウェア機能を管理するパッケージ化されているフィルター処理します。

他の Microsoft Windows Driver Model (WDM) ドライバーとは、フィルター ファクトリは、電源管理とセットアップ機能を処理します。 ドライバーの INF ファイルをインストール中に、1 つまたは複数のフィルター デバイス名を登録します (を参照してください[識別文字列](https://docs.microsoft.com/windows-hardware/drivers/install/device-identification-strings))。 このプロセスは、名前をシステム レジストリにロードし、」の説明に従って、各フィルター ファクトリを 1 つまたは複数の KS フィルターのカテゴリに関連付けます[オーディオ アダプターのデバイスのインターフェイスをインストールする](installing-device-interfaces-for-an-audio-adapter.md)します。 すべてのオーディオ デバイスに分類されます KSCATEGORY\_KSCATEGORY などの他のカテゴリの下で、オーディオがオーディオ デバイスを分類することがありますも\_(オーディオのレンダリング デバイス) のレンダリングまたは KSCATEGORY\_(のキャプチャオーディオ キャプチャ デバイス)。 ドライバーは、そのデバイスのフィルターを登録するさまざまなカテゴリを使用して、デバイスの一般的な機能をアドバタイズします。 ときに、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)、オーディオ デバイスが必要ですたとえば、特定の型の適切なカテゴリに分類されるデバイスのレジストリに見えます。

」の説明に従って、オペレーティング システムは、セットアップ API を使用して[デバイス インストール コンポーネント](https://docs.microsoft.com/windows-hardware/drivers/install/system-provided-device-installation-components)検出およびすべての KSCATEGORY を列挙する、\_レジストリにオーディオ フィルター ファクトリ。 各ファクトリのレジストリ エントリには、フィルター ファクトリのフレンドリ名と、クライアントは、フィルターをインスタンス化するファイルの作成の呼び出しに渡される長い文字列であるデバイス名の両方を指定します。 この呼び出しを行った可能性があります[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)カーネル モードからまたは**CreateFile**ユーザー モードから。 フィルターは、カーネル モードのオブジェクトし、カーネル ハンドルによって識別されます。 ファイルの作成の呼び出しでは、フィルターを参照するクライアントが使用できるインスタンス ハンドルを返します。 ユーザー モードのクライアントまたはオーディオのグラフのアップ ストリームのフィルターは、送信またはフィルターに IOCTL 要求を転送する、このハンドルを使用することができます。 詳細については**CreateFile**、Microsoft Windows SDK のドキュメントを参照してください。

一般的な WDM オーディオ アダプター カード可能性があります、PCI バス上に存在などとレンダリングまたは wave データのキャプチャのいくつかの I/O コネクタが含まれています。 このカードに 1 つのオーディオ デバイスには、一連のスピーカーとライン出力、ケーブルを推進するためのアナログのオーディオ出力ジャックとマイクとライン入力ケーブルからシグナルを受信するためのアナログのオーディオ ジャックが含まれます。 WDM オーディオ システムは、フィルターとしてデバイスを表し、そのフィルターを pin としてオーディオ ジャックを表します。

オーディオ デバイスのフィルターがバインドされている別のポートおよびミニポート ドライバーとして実装されている同時に動作します。

-   ミニポート ドライバーには、ハードウェア固有のコードが含まれています。

-   ポート ドライバーには、特定の種類のすべてのフィルターに共通する汎用的なコードが含まれています。

仕入先は、フィルターがオーディオ ハードウェアを管理する必要があるすべての専用コードを含むミニポート ドライバーを書き込みます。 オペレーティング システムが、PortCls システム ドライバーを通じてアクセス可能なポート ドライバーを提供します (Portcls.sys; を参照してください[ポート クラスのアダプターのドライバーと PortCls システム ドライバー](kernel-mode-wdm-audio-components.md#port_class_adapter_driver_and_portcls_system_driver))。 ポートおよびミニポート ドライバー、フィルターの実装を分割するには、独自のデバイスのドライバーの記述のタスクが簡略化します。

フィルター ファクトリでは、フィルターをインスタンス化、ときに最初に、フィルターのミニポート ドライバー オブジェクトを作成します。 フィルター ファクトリに、適切なポート オブジェクトのインスタンスを作成し、そのインスタンスに完全に機能しているフィルターを形成するために、ミニポート ドライバー オブジェクトをバインドします。 コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポート ドライバーでは、ソフトウェアを適切に定義されたインターフェイスを介して互いと通信します。 これらのインターフェイスの詳細については、次を参照してください。[ミニポート インターフェイス](miniport-interfaces.md)と[デバイスをサポートしている](supporting-a-device.md)します。

オーディオのフィルターは、暗証番号 (pin) ファクトリ、ノード、および内部接続のコレクションとして、基になるオーディオ デバイスの構造を公開します。 この情報は、型の構造体であるフィルター記述子には、ミニポート ドライバーに統合されています[ **PCFILTER\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcfilter_descriptor)します。 この構造体には、さらに、フィルターの暗証番号 (pin) ファクトリ、ノード、および内部接続の個々 の記述子が含まれています。 これらの記述子は、次の種類の構造体です。

[**PCPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcpin_descriptor)

[**PCNODE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcnode_descriptor)

[**PCCONNECTION\_記述子**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537688(v=vs.85))

ポート ドライバーが呼び出しミニポート ドライバーのフィルター記述子を取得するのには、 [ **IMiniport::GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-getdescription)メソッド。

ドライバーがその PCFILTER を設定する方法の例については\_記述子構造体、sb16 サンプル オーディオ ドライバー、Windows Driver Kit (WDK) でのヘッダー ファイル Table.h を参照してください。

 

 




