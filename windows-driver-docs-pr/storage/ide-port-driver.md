---
title: IDE ポート ドライバー
description: IDE ポート ドライバー
ms.assetid: 8e292680-6fa7-4f6b-b4ec-6f0f0d795d03
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efa9dacd5faa39a346baac25e80b70ac8a7fcded
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383068"
---
# <a name="ide-port-driver"></a>IDE ポート ドライバー
**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。

Microsoft Windows NT 4.0 では、IDE バスに関連付けられているポート/ミニポート ドライバーのペアは、SCSI ミニポート ドライバー *atapi.sys*、SCSI ポート ドライバーにリンクされている*scsiport.sys*します。

IDE では、Microsoft Windows 2000 および Windows XP では、ドライバーがポート*atapi.sys*が不要になったにリンクする、独立したドライバー *scsiport.sys*にも、他のドライバーのラッパーにします。

Windows 2000 および Windows XP の IDE ドライバー モデルでは次の 3 つのシステムから提供されたドライバーがある: *atapi.sys* (ポート ドライバー) *pciidex.sys* (コント ローラー ドライバー) と*問題は、pciide.sys*(汎用コント ローラー ミニドライバー)。 次の 3 つすべてのドライバーは、次の図に示します。

![windows 2000 および windows xp の ide ドライバー スタック ](images/idedrvrs.png)

以降、図の下部では、次に示します、スタック内の各ドライバー。

1.  Windows 2000 および Windows XP で IDE スタックは、PCI バス ドライバー上に構築されました。

2.  Microsoft では、ネイティブ IDE コント ローラー ドライバー/ミニドライバー ペアはほとんどの IDE コント ローラーの管理を提供します。 IDE コント ローラー ドライバー *pciidex.sys*、ドライバーのペアと、ミニドライバーのハードウェアに依存しないアスペクトを処理する*問題は、pciide.sys*、ハードウェア依存の側面を処理します。

3.  ネイティブのミニドライバーを使用する代わりに、独自の IDE コント ローラー ミニドライバーを提供することを選択できますベンダー*問題は、pciide.sys*します。 ベンダーのミニドライバーは、コント ローラー ミニドライバー ペアを形成する Microsoft 提供のコント ローラーのドライバーと連動する必要があります。 参照してください[Vendor-Supplied IDE コント ローラーのミニドライバーの要件](requirements-for-vendor-supplied-ide-controller-minidrivers.md)native Microsoft コント ローラー ドライバーで正しく動作する、要件の詳細については、ベンダーのミニドライバーが満たす必要があります。

4.  Microsoft は、IDE ポート ドライバーでは、 *atapi.sys、* とも呼ばれますが、*チャネル ドライバー*が作成され、各 IDE チャネルの機能のデバイス オブジェクト (FDO) を管理するため、します。 ポート ドライバーは、IDE コント ローラー/ミニドライバーのペアの上位層です。 基になる IDE コント ローラーで必要な形式に記憶域クラス ドライバーから受信する、SCSI 要求要素 (SRB) を変換します。 具体的には、SRB 内に含まれるコマンド記述ブロック (CDB) は、ATAPI および SCSI デバイスの異なる方法で定義されます。 ポートのドライバーは、Cdb、ATAPI トランスポート プロトコルのための IDE バスの特性から上位レベルのドライバーの保護に対応できるようにします。

5.  Microsoft では、CD-ROM (タイプ 5 SCSI) のすべてのデバイスを管理できる CD-ROM クラス ドライバーを提供します。

前の図に、ドライバー スタックに対応するデバイス オブジェクトのスタックの図を表示するには、次を参照してください。 [PCI IDE コント ローラーのデバイス オブジェクトの例](device-object-example-for-a-pci-ide-controller.md)します。

Windows Vista およびそれ以降のバージョンのオペレーティング システムでは、IDE のスタックはによって管理、 [ATA ポート ドライバー](ata-port-driver.md)します。

 

 


