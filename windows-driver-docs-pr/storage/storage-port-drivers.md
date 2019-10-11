---
title: 記憶域ポート ドライバー
description: 記憶域ポート ドライバー
ms.assetid: 5ff4916c-7d1f-4b61-a332-6ed89df9db56
keywords:
- ストレージポートドライバー WDK
- ストレージポートドライバー WDK, ストレージポートドライバーについて
- ポートドライバー WDK ストレージ
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 83a1a645d650a588e223f4e885dadc227de4add2
ms.sourcegitcommit: 0610366df5de756bf8aa6bfc631eba5e3cd84578
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/11/2019
ms.locfileid: "72262175"
---
# <a name="storage-port-drivers"></a>記憶域ポート ドライバー

Microsoft Windows には、システムによって提供される3つのストレージポートドライバーが含まれています。

- Windows Server 2003 およびそれ以降のバージョンのオペレーティングシステムで使用可能な[Storport ドライバー](storport-driver-overview.md) (*storport*) (推奨)

- [SCSI ポートドライバー](scsi-port-driver-overview.md) (*Scsiport*)

- Windows Vista 以降のバージョンのオペレーティングシステムで使用可能な[ATA ポートドライバー](ata-port-driver-overview.md) (*Ataport*)

Storport ドライバーは、SCSI ポートよりも効率的で高パフォーマンスのドライバーです。 そのため、可能な場合は、Storport ドライバーで動作するミニポートドライバーを開発する必要があります。 特に、ホストベースの RAID やファイバーチャネルアダプターなど、高パフォーマンスのデバイスで Storport を使用することが重要です。 Storport は、プラグアンドプレイ (PnP) をサポートしていない、またはシステム DMA を使用する必要があるアダプターまたはデバイスでは使用できません。 Storport ドライバーの使用に関する制限の詳細な一覧については、「[アダプターで Storport を使用するための要件](requirements-for-using-storport-with-an-adapter.md)」を参照してください。

ATA ポートドライバーは、ポートドライバーが記憶域クラスドライバーなどの上位レベルのドライバーと通信するために使用する、SCSI ベースのプロトコルから ATA ミニポートドライバーをシールドします。 たとえば、SCSI ポートまたは Storport に接続されているミニポートドライバーは、SCSI sense データをポートドライバーに提供する必要があります。 これは、ATA ミニポートドライバーには必要ありません。 Ata ポートドライバーは、ata コマンドを使用して ata ミニポートドライバーから必要なデータを収集し、そのデータを SCSI sense データ形式に準拠するように整理して、SCSI sense データであるかのように上位レベルのドライバーにデータを渡します。 また、ATA ポートドライバーは、上位レベルのドライバーから受信した各[SCSI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)を[IDE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_request_block)という ata ベースの同等のものに変換します。

各ポートドライバーは、ベンダーが提供する一連の記憶域ミニポートドライバーと通信し、ミニポートドライバーが呼び出す一連のサポートルーチンを提供します。 各ポートドライバーは、すべての記憶域ミニポートドライバーが実装する必要がある標準のルーチンセットを呼び出すことによって、ミニポートドライバーと通信します。 SCSI ポートドライバー、Storport ドライバー、および ATA ポートドライバーによって呼び出されるミニポートドライバールーチンは、互いによく似ています。 ポートドライバーのサポートルーチンとミニポートドライバーのルーチンの一覧については、次のセクションを参照してください。

| ポートドライバー | サポートルーチン | ミニポートドライバールーチン |
| ----------- | ---------------- | ------------------------ |
| Storport ドライバー | [Storport ドライバーのサポートルーチン](storport-driver-support-routines.md) | [Storport ドライバーミニポートルーチン](storport-miniport-driver-routines.md) |
| SCSI ポートドライバー | [SCSI ポートドライバーのサポートルーチン](scsi-port-driver-support-routines.md) | [SCSI ミニポートドライバールーチン](scsi-miniport-driver-routines.md) |
| ATA ポートドライバー | [ATA ポートドライバーのサポートルーチン](ata-miniport-drivers.md) | [ATA ミニポートドライバールーチン](ata-miniport-drivers.md) |

クライアントの Windows 製品で、または Windows Server 2003 より前のサーバー製品でストレージデバイスをサポートする場合は、SCSI ポートミニポートドライバーを指定する必要があります。

Windows Server 2003 以降のバージョンのサーバー製品ファミリで記憶装置をサポートする場合は、Storport ミニポートドライバーまたは SCSI ミニポートドライバーを指定できます。 Windows Vista 以降のバージョンのオペレーティングシステムに ATA ストレージデバイスをインストールする場合は、ATA ポートミニポートドライバーを指定する必要があります。

以下のセクションでは、Storport、SCSI ポート、および ATA ポートドライバーと、それらの違いについて説明します。
