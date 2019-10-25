---
title: SRB_FUNCTION_PROTOCOL_COMMANDの処理
description: SRB_FUNCTION_PROTOCOL_COMMANDの処理
ms.assetid: 12e9791b-8ddf-4d42-9d89-243bc38eeeb7
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_PROTOCOL_COMMAND
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 72ec9f0ba690b2ea9d9d9e2a1cff0bfaf50d2ebe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833736"
---
# <a name="handling-srb_function_protocol_command"></a>SRB_FUNCTION_PROTOCOL_COMMANDの処理

ミニポートドライバーは、ユーザーモードアプリケーションに対して HBA が専用のサポートを提供するときに、SRB_FUNCTION_PROTOCOL_COMMAND 要求を処理します。 この要求をサポートすることで、ドライバーによって定義された ("プライベート") プロトコルコマンドのセットをミニポートドライバーに直接送信できるようになります。

**関数**メンバーが SRB_FUNCTION_PROTOCOL_COMMAND に設定されている SRBs の場合、 **DataBuffer**メンバーには、システム定義の[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command)構造体へのポインターが含まれています。

ミニポートは、次の操作を実行します。

* STORAGE_PROTOCOL_COMMAND 構造体で指定されたコマンド情報を、適切なプロトコル固有のバスコマンドに変換します。 プロトコルは **\*データ > Buffer. ProtocolType**によって識別されます。

* 書き込み型要求の場合は、 **Datatodevicebufferoffset**が指すデータをデバイスに転送します。

* 読み取り型要求の場合は、 **DataFromDeviceBufferOffset**が指すバッファーにデバイスからデータを転送します。

* 要求の状態を反映するように**Returnstatus**を設定し、必要に応じて**ErrorCode**を設定します。

## <a name="see-also"></a>参照

[IOCTL_STORAGE_PROTOCOL_COMMAND (*winioctl .h*)](https://docs.microsoft.com/windows/desktop/api/winioctl/ni-winioctl-ioctl_storage_protocol_command)

[IOCTL_STORAGE_PROTOCOL_COMMAND (*ntddstor*)](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ni-ntddstor-ioctl_storage_protocol_command)

[HwStorStartIo](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_startio)

[SRB_IO_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)

[SCSI_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)

[STORAGE_PROTOCOL_COMMAND](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddstor/ns-ntddstor-_storage_protocol_command)

[STORAGE_REQUEST_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_storage_request_block)
