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
ms.openlocfilehash: d62eeae42a398208407d120df7be4a193041728f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574824"
---
# <a name="dynamic-audio-subdevices"></a>動的なオーディオ サブデバイス


一部のオーディオのアダプターは、実行時に、内部のトポロジを動的に変更できます。 PortCls システム ドライバー (Portcls.sys) のシステム提供の機能を使用すると、アダプターのドライバーは、動的に構成可能なオーディオ ハードウェアのソフトウェアのサポートを提供できます。

たとえば、 [Intel 高度な定義オーディオ仕様](https://go.microsoft.com/fwlink/p/?linkid=42508)用語のオーディオ コーデックを使用して、HD オーディオ リンク インターフェイスを介してオーディオ (HD オーディオ) コント ローラーに接続する統合されたオーディオ アダプターを参照します。 一般的なオーディオ コーデック ジャック プレゼンスの検出をサポートしています: プラグが挿入またはジャックから削除されたと、ハードウェアがハードウェア構成の変更のドライバーに通知する割り込みを生成します。 ドライバーを作成して応答ヘッドフォンのジャックにプラグを挿入するなど、 [KS フィルター](https://msdn.microsoft.com/library/windows/hardware/ff567644)ヘッドフォンのオーディオ サブデバイスを表すため。 ドライバーは、フィルターにハードウェア リソースを割り当てます (たとえば、ヘッドホン必要がありますボリューム コントロールやアナログ デジタル コンバーターでは、DAC) と、フィルターをオーディオ デバイスとして登録します。 ユーザーは、ヘッドホンから切り離し、ドライバーは、リソースの解放、フィルターを削除する、レジストリから削除して応答します。

この動作により、オーディオのアプリケーションは、オーディオ デバイスが登録されていることをチェックし、現在接続されているデバイスにのみ検出されます。 デバイスが接続されている場合、レジストリには表示されません。

Windows Vista、Windows Server 2003 Service Pack 1 (SP1)、および Windows XP Service Pack 2 (SP2)、PortCls サポート、 [IUnregisterSubdevice](https://msdn.microsoft.com/library/windows/hardware/ff537030)と[IUnregisterPhysicalConnection](https://msdn.microsoft.com/library/windows/hardware/ff537022)インターフェイス。 オーディオのアダプターのドライバーでは、これら 2 つのインターフェイスを使用して、使用されなくなったオーディオ サブデバイスの削除します。 などの Windows Server 2003 および Windows XP、Windows の以前のバージョンでは、これらのインターフェイスはサポートされません。 Windows の以前のバージョン、サブデバイスを作成したが削除されません--ことができます、サブデバイスが作成されると、アダプターのドライバー オブジェクトの有効期間が存在します。

**IUnregisterSubdevice**インターフェイスには、ドライバーが前の呼び出しによって登録されているサブデバイス"登録"を解除するアダプターのドライバーが使用できる 1 つのメソッドが含まれています、 [ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)ルーチン。

[**IUnregisterSubdevice::UnregisterSubdevice**](https://msdn.microsoft.com/library/windows/hardware/ff537032)

**IUnregisterPhysicalConnection**インターフェイスにはアダプター ドライバーがサブデバイス間の物理接続を登録解除に使用できる 3 つのメソッドが含まれています。

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537024)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537027)

[**IUnregisterPhysicalConnection::UnregisterPhysicalConnectionToExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537029)

これらのメソッドは、ドライバーが前の呼び出しによって登録された接続を削除、 [ **PcRegisterPhysicalConnection**](https://msdn.microsoft.com/library/windows/hardware/ff537726)、 [ **PcRegisterPhysicalConnectionFromExternal**](https://msdn.microsoft.com/library/windows/hardware/ff537728)、および[ **PcRegisterPhysicalConnectionToExternal** ](https://msdn.microsoft.com/library/windows/hardware/ff537729)ルーチン。 PortCls、PcRegisterPhysicalConnection から情報を格納する*Xxx*ポート ドライバーは、その後に応答する情報を使用するために呼び出す、 [ **KSPROPERTY\_暗証番号(pin)\_PHYSICALCONNECTION** ](https://msdn.microsoft.com/library/windows/hardware/ff565205)プロパティ要求。 アダプターのトポロジから、サブデバイスを削除するときに、ドライバーは、トポロジの一部にサブデバイスの物理的な接続を登録解除する必要があります。 サブデバイスの物理的な接続の登録を解除するエラーは、メモリ リークを起こすことができます。 PortCls サポート、PcRegister*Xxx*ルーチンでは、Windows 2000 以降と Windows Me 98/。

このセクションでは、次のトピックでは、動的なトポロジを持つアダプターのドライバー サポートを実装する方法について説明します。

[動的トポロジを管理します。](managing-dynamic-topologies.md)

[動的サブデバイスのドライバー サポート](driver-support-for-dynamic-subdevices.md)

[動的なオーディオ サブデバイス ジャックの説明](jack-descriptions-for-dynamic-audio-subdevices.md)

 

 




