---
title: IDE ポート ドライバー
description: IDE ポート ドライバー
ms.assetid: 8e292680-6fa7-4f6b-b4ec-6f0f0d795d03
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4220ef34e4a3fe48fe0caf2de3c85e21741c07fa
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72262392"
---
# <a name="ide-port-driver"></a>IDE ポート ドライバー

>[!NOTE]
> ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](storport-driver-overview.md)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。

Microsoft Windows NT 4.0 では、IDE バスに関連付けられているポート/ミニポートドライバーのペアは SCSI ミニポートドライバーである*atapi. sys*で、scsi ポートドライバー ( *scsiport*) にリンクされています。

Microsoft Windows 2000 および Windows XP では、IDE ポートドライバー *atapi*は、 *scsiport*または他のラッパードライバーへのリンクがなくなった独立したドライバーです。

Windows 2000 と Windows XP の IDE ドライバーモデルには、次の3つのシステム指定ドライバーがあります。 *.sys* (ポートドライバー)、 *pciidex* (コントローラードライバー)、および*pciide* (汎用コントローラーミニドライバー)。 次の図は、3つのドライバーすべてを示しています。

![windows 2000 および windows xp ide ドライバースタック ](images/idedrvrs.png)

図の一番下から、スタック内の各ドライバーについて説明します。

1. Windows 2000 および Windows XP の IDE スタックは、PCI バスドライバーによって階層化されています。

2. Microsoft では、ほとんどの IDE コントローラーを管理できるネイティブ IDE コントローラードライバー/ミニドライバーペアを提供しています。 IDE コントローラードライバー *pciidex*は、ドライバーペアのハードウェアに依存しない部分を処理し、ミニドライバー、 *pciide*はハードウェアに依存する側面を処理します。

3. ベンダーは、native ミニドライバー ( *pciide*) を使用する代わりに、独自の IDE コントローラーミニドライバーを提供することができます。 ベンダーのミニドライバーは、コントローラーとミニドライバーのペアを形成するために、Microsoft が提供するコントローラードライバーと連携する必要があります。 ベンダのミニドライバーがネイティブの Microsoft コントローラードライバーで正常に動作するために満たす必要がある要件の説明については、「[ベンダーが提供する IDE コントローラーの要件ミニドライバー](requirements-for-vendor-supplied-ide-controller-minidrivers.md) 」を参照してください。

4. Microsoft では、ide ポートドライバーである*atapi を*提供しています。これは、*チャネルドライバー*とも呼ばれます。これは、各 ide チャネルに対して機能デバイスオブジェクト (FDO) を作成および管理するためです。 ポートドライバーは、IDE コントローラーとミニドライバーのペアの上にあります。 ストレージクラスドライバーから受け取った SCSI 要求ブロック (SRB) を、基になる IDE コントローラーが必要とする形式に変換します。 特に、SRB 内に含まれるコマンド記述子ブロック (CDB) は、ATAPI および SCSI デバイスに対して異なる方法で定義されます。 ポートドライバーは、ATAPI トランスポートプロトコルとの互換性を確保するために再パッケージ化 CDBs を使用して、上位レベルのドライバーを IDE バスの特性から独立させます。

5. Microsoft は、すべての CD-ROM (type 5 SCSI) デバイスを管理できる CD-ROM クラスドライバーを提供しています。

前の図のドライバースタックに対応するデバイスオブジェクトスタックの図を表示するには、「 [PCI IDE コントローラーのデバイスオブジェクトの例](device-object-example-for-a-pci-ide-controller.md)」を参照してください。

Windows Vista 以降のバージョンのオペレーティングシステムでは、IDE スタックは[ATA ポートドライバー](ata-port-driver-overview.md)によって管理されます。
