---
title: ストレージ ドライバーのサンプル
description: このディレクトリのストレージドライバーサンプルは、デバイスのカスタムドライバーを作成するための開始点となります。
ms.assetid: 4FEB911D-78D5-403E-91AB-8A064E31F4FA
ms.date: 12/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: c5340cbba706e30c3e5ef49374de8ebabe5b6b75
ms.sourcegitcommit: 30fa63ad13fd5e2e883b76a44f0703e01049ffa1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74735258"
---
# <a name="storage-driver-samples"></a>ストレージ ドライバーのサンプル

このディレクトリのドライバーサンプルは、デバイスのカスタムドライバーを作成するための開始点となります。

| サンプル | 説明 |
| --- | --- |
| [CDROM クラスドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/cdrom-storage-class-driver) | Cd ROM クラスドライバーは、CD、DVD、およびブルーレイドライブへのアクセスを提供するために使用されます。 プラグアンドプレイ、電源管理、および自動実行 (メディア変更通知) をサポートしています。 |
| [ClassPnP クラスドライバーライブラリ](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/classpnp-storage-class-driver-library) | ライブラリストレージクラスドライバー。 プラグアンドプレイ (PnP)、電源管理、およびその他の機能をサポートするために必要なほとんどのコードにより、ストレージクラスドライバーを簡単に記述できます。 このライブラリは、disk、CDROM、および tape class ドライバーによって使用されます。 |
| [ディスククラスドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/disk-class-driver) | ディスクデバイス用のクラスドライバー。 |
| [AddFilter ストレージフィルターツール](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/addfilter-storage-filter-tool) | 特定のドライブまたはボリュームのフィルタードライバーを追加および削除するコマンドラインアプリケーションです。 |
| [iSCSI WMI クライアント](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/iscsi-wmi-client) | Iscsicli.exe ツール、[iSCSI イニシエーターのプロパティ] ページ、WBEMTEST ツール、およびカスタマイズされた WMI スクリプトを使用してテストできる、iSCSI ミニポートでの WMI の実装。 |
| [LSI_U3 StorPort ミニポート](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/lsi_u3-storport-miniport-driver) | パラレル SCSI ホストバスアダプターまたは LSI 53C1010 SCSI ASIC を使用するマザーボード上のソリューションで使用するアダプタードライバー。 |
| [StorAHCI のミニポート](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/storahci-storport-miniport-driver) | サンプルの Storport ACHI ミニポートドライバー。 |
| [マルチパス i/o (MPIO) DSM サンプル](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/multipath-io-mpio-dsm-sample)     | ベンダー固有のデバイス固有モジュール (DSM) を構築するときに従う例。 このサンプル DSM は、iSCSI デバイスとファイバーチャネルデバイスをサポートしています。 |
| [Super フロッピー (sfloppy) ストレージクラスドライバー](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/super-floppy-sfloppy-storage-class-driver) | スーパーフロッピーディスクドライブ用のクラスドライバー。 |
| [SCSI パススルーインターフェイスツール](https://docs.microsoft.com/samples/microsoft/windows-driver-samples/scsi-pass-through-interface-tool) | DeviceIoControl API を使用して、アプリケーションでパススルー Ioctl を使用してから SCSI デバイスと通信する方法を示します。 |
