---
title: 動的なオーディオ サブデバイス
description: 動的なオーディオ サブデバイス
ms.assetid: d8ebd6d9-37ed-4890-aae1-5ecf58f2e22a
keywords:
- WDM オーディオドライバー WDK、動的サブデバイス
- オーディオドライバー WDK、動的サブデバイス
- 動的オーディオサブデバイス WDK オーディオ
- サブデバイス WDK オーディオ
- オーディオコーデック WDK
- ジャック-プレゼンス検出 WDK オーディオ
- サブデバイスの削除
- サブデバイスの削除
- サブデバイスの登録解除
- 動的サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ac1a5656111338c96dea760f196d746a2df1712
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925613"
---
# <a name="dynamic-audio-subdevices"></a>動的なオーディオ サブデバイス


一部のオーディオアダプターは、実行時に内部トポロジを動的に変更できます。 PortCls システムドライバー (Portcls) でシステムによって提供される機能を使用することにより、アダプタードライバーは動的に構成可能なオーディオハードウェアに対してソフトウェアサポートを提供できます。

たとえば、 [Intel High Definition Audio 仕様](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html)では、audio コーデックという用語を使用して、Hd audio Link インターフェイス経由で High definition AUDIO (hd audio) コントローラーに接続する統合オーディオアダプターを参照します。 一般的なオーディオコーデックでは、ジャックのプレゼンス検出がサポートされています。プラグがジャックに挿入されるか、ジャックから削除されると、ハードウェアは割り込みを生成してハードウェア構成の変更をドライバーに通知します。 たとえば、ドライバーは、ヘッドホンのオーディオサブデバイスを表す[KS フィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters)を作成することによって、ヘッドホンジャックへのプラグインの挿入に応答します。 ドライバーによってフィルターにハードウェアリソースが割り当てられます (たとえば、ヘッドホンではボリュームコントロールとデジタルアナログコンバーター (DAC) が必要になる場合があります)。また、フィルターをオーディオデバイスとして登録します。 ユーザーがヘッドフォンを unplugs と、ドライバーはリソースを解放し、フィルターを削除して、レジストリから削除します。

この動作によって、オーディオアプリケーションがどのオーディオデバイスが登録されているかを確認するときに、現在接続されているデバイスのみが検出されるようになります。 デバイスが取り外されている場合、そのデバイスはレジストリに表示されません。

Windows Vista、Windows Server 2003 Service Pack 1 (SP1)、および Windows XP Service Pack 2 (SP2) では、PortCls は[Iunregistersubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregistersubdevice)インターフェイスと[Iunregistersubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iunregisterphysicalconnection)インターフェイスをサポートしています。 オーディオアダプタードライバーは、この2つのインターフェイスを使用して、使用されなくなったオーディオサブデバイスを削除します。 Windows Server 2003 や Windows XP など、以前のバージョンの Windows では、これらのインターフェイスはサポートされていません。 以前のバージョンの Windows では、サブデバイスは作成できますが、削除はできません。サブデバイスが作成されると、アダプタードライバーオブジェクトの有効期間中は存在します。

**Iunregistersubdevice**インターフェイスには、アダプタードライバーが以前の[**pcregiサブデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)ルーチンの呼び出しによって登録されたサブデバイスの "登録解除" に使用できる1つのメソッドが含まれています。

[**IUnregisterSubdevice:: UnregisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)

**Iunregisterphysicalconnection**インターフェイスには、アダプタードライバーがサブデバイス間の物理接続の登録を解除するために使用できる3つのメソッドが含まれています。

[**IUnregisterPhysicalConnection:: UnregisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnection)

[**IUnregisterPhysicalConnection:: UnregisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectionfromexternal)

[**IUnregisterPhysicalConnection:: UnregisterPhysicalConnectionToExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectiontoexternal)

これらのメソッドは、以前に[**Pcregisterphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)、 [**pcregiphysicalphysicalconnectionfromexternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)、および[**Pcregiphysicalphysicalconnectiontoexternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)ルーチンを呼び出して、ドライバーが登録した接続を削除します。 PortCls は、Pcregiphysicalconnection*Xxx*呼び出しからの情報を格納します。これにより、ポートドライバーは、この情報を後で使用して、 [**ksk プロパティ\_\_PIN の physicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)プロパティ要求に応答できます。 アダプターのトポロジからサブデバイスを削除する場合、ドライバーは、サブデバイスの物理接続をトポロジのその部分に登録解除する必要があります。 サブデバイスの物理接続の登録を解除しないと、メモリリークが発生する可能性があります。 PortCls では、Windows 2000 以降*Xxx*および windows Me/98 での PcRegister ルーチンがサポートされています。

このセクションの次のトピックでは、動的トポロジを使用するアダプターのドライバーサポートを実装する方法について説明します。

[動的なトポロジの管理](managing-dynamic-topologies.md)

[動的なサブデバイス用のドライバーのサポート](driver-support-for-dynamic-subdevices.md)

[動的なオーディオ サブデバイスのジャックに関する説明](jack-descriptions-for-dynamic-audio-subdevices.md)

 

 




