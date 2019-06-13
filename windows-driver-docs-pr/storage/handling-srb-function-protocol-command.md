---
title: SRB_FUNCTION_PROTOCOL_COMMAND の処理
description: SRB_FUNCTION_PROTOCOL_COMMAND の処理
ms.assetid: 12e9791b-8ddf-4d42-9d89-243bc38eeeb7
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_PROTOCOL_COMMAND
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 28edfc66ec1b1f1be90b90fd34052b25c79c6377
ms.sourcegitcommit: d2e67f2be9611c583b8b6589b38fe371585b68f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2019
ms.locfileid: "67037989"
---
# <a name="handling-srbfunctionprotocolcommand"></a>SRB_FUNCTION_PROTOCOL_COMMAND の処理

ミニポート ドライバーは、HBA は、ユーザー モード アプリケーションの専用サポートを提供するときに、SRB_FUNCTION_PROTOCOL_COMMAND 要求を処理します。 一連のミニポート ドライバーに直接送信する ("private") プロトコルのドライバーの定義済みのコマンドは、この要求をサポートできます。

使用される Srb の**関数**メンバー SRB_FUNCTION_PROTOCOL_COMMAND、セット、 **DataBuffer**メンバーには、システム定義へのポインターが含まれています[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_protocol_command)。構造体。

ミニポートは、次の操作を行います。

* 適切なプロトコル固有のバス コマンドに STORAGE_PROTOCOL_COMMAND 構造体で提供されるコマンドの情報を変換します。 プロトコルがで識別される **\*データ Buffer.ProtocolType]-> [** します。

* 書き込みの種類の要求のデータを転送する**DataToDeviceBufferOffset**デバイスを指します。

* 読み取りの種類の要求のデータを転送、デバイスからバッファーを**DataFromDeviceBufferOffset**を指します。

* 設定**ReturnStatus** 、要求の状態を反映し、必要に応じて設定を**ErrorCode**します。

## <a name="see-also"></a>関連項目

[IOCTL_STORAGE_PROTOCOL_COMMAND (*winioctl.h*)](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-ioctl_storage_protocol_command)

[IOCTL_STORAGE_PROTOCOL_COMMAND (*ntddstor.h*)](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)

[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_startio)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ns-ntddscsi-_srb_io_control)

[SCSI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_scsi_request_block)

[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddstor/ns-ntddstor-_storage_protocol_command)

[STORAGE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_storage_request_block)
