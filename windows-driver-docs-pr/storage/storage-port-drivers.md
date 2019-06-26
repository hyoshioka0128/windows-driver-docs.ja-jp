---
title: 記憶域ポート ドライバー
description: 記憶域ポート ドライバー
ms.assetid: 5ff4916c-7d1f-4b61-a332-6ed89df9db56
keywords:
- 記憶域ポート ドライバー WDK
- 記憶域に関するポート ドライバー WDK、記憶域ドライバーを移植します。
- ポート ドライバー WDK ストレージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fcdb83e6478b72a3d6592f638ecaaf34de6ed3d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368184"
---
# <a name="storage-port-drivers"></a>記憶域ポート ドライバー


## <span id="ddk_storage_port_drivers_kg"></span><span id="DDK_STORAGE_PORT_DRIVERS_KG"></span>


Microsoft Windows には、次の 3 つのシステムが指定したストレージ ポート ドライバーが含まれています。

-   [SCSI ポート ドライバー](scsi-port-driver.md) (*Scsiport.sys*)

-   [Storport ドライバー](storport-driver.md) (*Storport.sys*)、Windows Server 2003 およびそれ以降のバージョンのオペレーティング システムとして利用可能

-   [ATA ポート ドライバー](ata-port-driver.md) (*Ataport.sys*)、Windows Vista およびそれ以降のバージョンのオペレーティング システムとして利用可能

Storport ドライバーは、SCSI ポートよりも効率的で高パフォーマンス ドライバーです。 そのため可能であれば、Storport ドライバーを使用するミニポート ドライバーを開発する必要があります。 Storport を使用して、ホスト ベースの RAID のファイバー チャネル アダプターなどの高パフォーマンスのデバイスで特に重要ですが。 Storport は、アダプターまたはデバイスのプラグ アンド プレイ (PnP) をサポートしていない、またはシステム DMA を使用する必要がありますには使用できません。 Storport ドライバーの使用に関する制限の詳細な一覧についてを参照してください。[を使用しての Storport のアダプターを使用するための要件](requirements-for-using-storport-with-an-adapter.md)します。

ATA ポート ドライバーでは、記憶域クラス ドライバーなどのより高度なドライバーとの通信にポート ドライバーを使用する、SCSI ベースのプロトコルからの ATA ミニポート ドライバーを保護します。 たとえば、SCSI ポートまたは Storport のいずれかにアタッチされているミニポート ドライバーでは、ポート ドライバーに SCSI センスのデータを提供する必要があります。 これは、ATA のミニポート ドライバーの必要はありません。 ATA ポート ドライバーでは、ATA コマンドを使用して、ATA のミニポート ドライバーから必要なデータを収集します。、SCSI センス データ形式に準拠し、SCSI センス データと同様より高度なドライバーにデータを渡すようにデータが整理されます。 ATA のポートのドライバーの各変換も[ **SCSI\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block) ATA ベースの等価と呼ばれる高度なドライバーから受信した、 [**IDE\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_request_block)します。

各ポート ドライバーは、一連のベンダーから提供された記憶域ミニポート ドライバーと通信しを呼び出す、ミニポート ドライバーのサポート ルーチンのセットを提供します。 SCSI ポート ドライバーによって提供されるサポート ルーチンが記載されて[SCSI ポート ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 Storport ドライバーによって提供されるサポート ルーチンが記載されて[Storport ドライバー サポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。 ATA ポート ドライバーによって提供されるサポート ルーチンが記載されて[ATA ポート ライブラリ ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

各ポート ドライバーは、標準的な一連のすべての記憶域ミニポート ドライバーを実装する必要があるルーチンを呼び出すことによって、ミニポート ドライバーと通信します。 SCSI ポート ドライバー、Storport ドライバー、および ATA ポート ドライバーと呼ばれる、ミニポート ドライバー ルーチンは、互いに非常に似ています。 これらのルーチンの説明が記載[SCSI ミニポート ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、 [Storport ドライバー ミニポート ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、および[ATA ミニポート ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)、それぞれ.

サポート、クライアントの Windows の製品にやサーバー製品に Windows Server 2003 より前に、ストレージ デバイスを設定する場合は、SCSI ポート ミニポート ドライバーを指定してください。

Windows Server 2003 およびサーバーの製品ファミリの以降のバージョンでサポートされる記憶域デバイスを設定する場合は、SCSI ポート ミニポート ドライバーまたは Storport ミニポート ドライバーのいずれかを行うことができます。 Windows Vista およびそれ以降のバージョンのオペレーティング システムで ATA ストレージ デバイスをインストールする場合は、ATA ポート ミニポート ドライバーを提供する必要があります。

次のセクションでは、SCSI ポート、Storport、および ATA ポート ドライバーとの違いについて説明します。

 

 




