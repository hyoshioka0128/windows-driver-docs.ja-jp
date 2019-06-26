---
title: 動的なオーディオ サブデバイス
description: 動的なオーディオ サブデバイス
ms.assetid: d8ebd6d9-37ed-4890-aae1-5ecf58f2e22a
keywords:
- WDM オーディオ ドライバー WDK、動的サブデバイス
- オーディオ ドライバー WDK、動的サブデバイス
- 動的なオーディオ サブデバイス WDK オーディオ
- サブデバイス WDK オーディオ
- WDK のオーディオ コーデック
- 回線のモジュラー ジャック プレゼンス検出 WDK オーディオ
- サブデバイスを削除します。
- サブデバイスを削除します。
- サブデバイスの登録を解除
- 動的サブデバイス WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b761fe581a382bd4ec2842b0f0fa5f0599f43c68
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360079"
---
# <a name="dynamic-audio-subdevices"></a>動的なオーディオ サブデバイス


一部のオーディオのアダプターは、実行時に、内部のトポロジを動的に変更できます。 PortCls システム ドライバー (Portcls.sys) のシステム提供の機能を使用すると、アダプターのドライバーは、動的に構成可能なオーディオ ハードウェアのソフトウェアのサポートを提供できます。

たとえば、 [Intel 高度な定義オーディオ仕様](https://go.microsoft.com/fwlink/p/?linkid=42508)用語のオーディオ コーデックを使用して、HD オーディオ リンク インターフェイスを介してオーディオ (HD オーディオ) コント ローラーに接続する統合されたオーディオ アダプターを参照します。 一般的なオーディオ コーデック ジャック プレゼンスの検出をサポートしています: プラグが挿入またはジャックから削除されたと、ハードウェアがハードウェア構成の変更のドライバーに通知する割り込みを生成します。 ドライバーを作成して応答ヘッドフォンのジャックにプラグを挿入するなど、 [KS フィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-filters)ヘッドフォンのオーディオ サブデバイスを表すため。 ドライバーは、フィルターにハードウェア リソースを割り当てます (たとえば、ヘッドホン必要がありますボリューム コントロールやアナログ デジタル コンバーターでは、DAC) と、フィルターをオーディオ デバイスとして登録します。 ユーザーは、ヘッドホンから切り離し、ドライバーは、リソースの解放、フィルターを削除する、レジストリから削除して応答します。

この動作により、オーディオのアプリケーションは、オーディオ デバイスが登録されていることをチェックし、現在接続されているデバイスにのみ検出されます。 デバイスが接続されている場合、レジストリには表示されません。

Windows Vista、Windows Server 2003 Service Pack 1 (SP1)、および Windows XP Service Pack 2 (SP2)、PortCls サポート、 [IUnregisterSubdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregistersubdevice)と[IUnregisterPhysicalConnection](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iunregisterphysicalconnection)インターフェイス。 オーディオのアダプターのドライバーでは、これら 2 つのインターフェイスを使用して、使用されなくなったオーディオ サブデバイスの削除します。 などの Windows Server 2003 および Windows XP、Windows の以前のバージョンでは、これらのインターフェイスはサポートされません。 Windows の以前のバージョン、サブデバイスを作成したが削除されません--ことができます、サブデバイスが作成されると、アダプターのドライバー オブジェクトの有効期間が存在します。

**IUnregisterSubdevice**インターフェイスには、ドライバーが前の呼び出しによって登録されているサブデバイス"登録"を解除するアダプターのドライバーが使用できる 1 つのメソッドが含まれています、 [ **PcRegisterSubdevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregistersubdevice)ルーチン。

[**IUnregisterSubdevice::UnregisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)

**IUnregisterPhysicalConnection**インターフェイスにはアダプター ドライバーがサブデバイス間の物理接続を登録解除に使用できる 3 つのメソッドが含まれています。

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnection)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectionfromexternal)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionToExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnectiontoexternal)

これらのメソッドは、ドライバーが前の呼び出しによって登録された接続を削除、 [ **PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnection)、 [ **PcRegisterPhysicalConnectionFromExternal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectionfromexternal)、および[ **PcRegisterPhysicalConnectionToExternal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcregisterphysicalconnectiontoexternal)ルーチン。 PortCls、PcRegisterPhysicalConnection から情報を格納する*Xxx*ポート ドライバーは、その後に応答する情報を使用するために呼び出す、 [ **KSPROPERTY\_暗証番号(pin)\_PHYSICALCONNECTION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-physicalconnection)プロパティ要求。 アダプターのトポロジから、サブデバイスを削除するときに、ドライバーは、トポロジの一部にサブデバイスの物理的な接続を登録解除する必要があります。 サブデバイスの物理的な接続の登録を解除するエラーは、メモリ リークを起こすことができます。 PortCls サポート、PcRegister*Xxx*ルーチンでは、Windows 2000 以降と Windows Me 98/。

このセクションでは、次のトピックでは、動的なトポロジを持つアダプターのドライバー サポートを実装する方法について説明します。

[動的トポロジを管理します。](managing-dynamic-topologies.md)

[動的サブデバイスのドライバー サポート](driver-support-for-dynamic-subdevices.md)

[動的なオーディオ サブデバイス ジャックの説明](jack-descriptions-for-dynamic-audio-subdevices.md)

 

 




