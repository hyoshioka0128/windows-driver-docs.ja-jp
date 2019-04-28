---
title: ストレージ ドライバーのサンプル
description: ストレージ ドライバー サンプルでは、このディレクトリは、デバイス用のカスタム ドライバーを記述するための開始点を提供します。
ms.assetid: 4FEB911D-78D5-403E-91AB-8A064E31F4FA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1826460c27c89f359a14929d6027db13950d8b89
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374210"
---
# <a name="storage-driver-samples"></a>ストレージ ドライバーのサンプル


このディレクトリにドライバーのサンプルでは、デバイス用のカスタム ドライバーを記述するための開始点を提供します。

## <a name="storage"></a>ストレージ


| サンプル名                                 | ソリューション                                                     | 説明                                                                                                                                                                                                                                     |
|---------------------------------------------|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| CDROM クラス ドライバー                          | [cdrom](https://go.microsoft.com/fwlink/p/?LinkId=617971)     | CD-ROM クラス ドライバーを使用して、CD、DVD およびブルーレイ ドライブへのアクセスを提供します。 プラグ アンド プレイ、電源管理、および自動実行をサポートしています (メディアは、通知を変更)。                                                                          |
| ClassPnP クラス ドライバー ライブラリ               | [classpnp](https://go.microsoft.com/fwlink/p/?LinkId=617978)  | ライブラリ ストレージ クラス ドライバーです。 プラグ アンド プレイ (PnP)、電源管理、およびその他の機能をサポートするために必要なコードのほとんどで、記憶域クラス ドライバーの記述が簡単になります。 このライブラリは、ディスク、cd-rom ドライブ、およびテープのクラス ドライバーによって使用されます。 |
| ディスク クラス ドライバー                           | [disk](https://go.microsoft.com/fwlink/p/?LinkId=617979)      | ディスク デバイス用のクラス ドライバー。                                                                                                                                                                                                                |
| AddFilter ストレージ フィルター ツール               | [addfilter](https://go.microsoft.com/fwlink/p/?LinkId=617980) | 追加し、特定のドライブまたはボリューム フィルター ドライバーを削除するコマンド ライン アプリケーションです。                                                                                                                                                    |
| iSCSI WMI クライアント                            | [iscsi](https://go.microsoft.com/fwlink/p/?LinkId=617981)     | ISCSICLI.exe ツール、iSCSI イニシエーターのプロパティ ページ、WBEMTEST.exe ツール、およびカスタムの WMI スクリプトを使用してテストできる iSCSI ミニポートに WMI 実装します。                                                               |
| LSI\_U3 StorPort ミニポート                   | [lsi\_u3](https://go.microsoft.com/fwlink/p/?LinkId=617982)   | 並列 SCSI ホスト バス アダプターまたは LSI 53C 1010 SCSI ASIC を使用して、マザーボードのソリューションで使用するためのアダプター ドライバー。                                                                                                                  |
| StorAHCI StorPort ミニポート                  | [storahci](https://go.microsoft.com/fwlink/p/?LinkId=617983)  | サンプル Storport ACHI ミニポート ドライバー。                                                                                                                                                                                                         |
| マルチパス I/O (MPIO) DSM のサンプル             | [msdsm](https://go.microsoft.com/fwlink/p/?LinkId=620203)     | ベンダー固有で、デバイス固有モジュール (DSM) を構築するときに実行する例です。 このサンプルの DSM では、iSCSI とファイバー チャネル デバイスをサポートします。                                                                                                   |
| スーパー フロッピー (sfloppy) 記憶域クラス ドライバー | [sfloppy](https://go.microsoft.com/fwlink/p/?LinkId=617989)   | スーパー フロッピー ディスク ドライブ用のクラス ドライバー。                                                                                                                                                                                                    |
| SCSI パススルー インターフェイス ツール            | [spti](https://go.microsoft.com/fwlink/p/?LinkId=617990)      | DeviceIoControl API を使用して、アプリケーションでの Ioctl パススルーを使用してから、SCSI デバイスと通信する方法を示します。                                                                                                          |

 

 

 




