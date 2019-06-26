---
title: NVMe デバイス用ファームウェアのアップグレード
description: NVMe の記憶域デバイスのファームウェアの更新は、そのデバイスのミニポート ドライバーに発行されます。
ms.assetid: A912715A-F82A-41E5-BE14-5B17930C29B7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9437d51baa99095c6381f939983757fa2e06bf3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386811"
---
# <a name="upgrading-firmware-for-an-nvme-device"></a>NVMe デバイス用ファームウェアのアップグレード


NVMe の記憶域デバイスのファームウェアの更新は、そのデバイスのミニポート ドライバーに発行されます。 ファームウェアの情報を取得するためのコマンドを関数、ダウンロード、およびファームウェア イメージをアクティブ化は、ミニポートに発行されます。

## <a name="span-idfirmwareupgradeprocessspanspan-idfirmwareupgradeprocessspanspan-idfirmwareupgradeprocessspanfirmware-upgrade-process"></a><span id="Firmware_upgrade_process"></span><span id="firmware_upgrade_process"></span><span id="FIRMWARE_UPGRADE_PROCESS"></span>ファームウェアのアップグレード プロセス


Windows 用に認定 NVMe デバイスは、デバイスが操作中にファームウェアを更新できます。 ファームウェアの更新を使用して、 [ **IOCTL\_SCSI\_ミニポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_miniport)ファームウェアが関連付けられているコントロールのデータを含む、SRB で書式設定を要求します。 更新プロセスが含まれます。

1.  更新プログラムを配置する場所を特定するファームウェア スロットの情報を収集します。 ファームウェアの更新プログラムが配置を決定するときに、いくつかの考慮事項があります。

    -   スロットの数があるでしょうか。
    -   スロットの数は、更新プログラムを保持できますか。 いくつかのスロットは読み取り専用または前のイメージに戻す機能が必要な場合に保持する必要がありますイメージを格納します。
    -   どのスロットには、現在のアクティブなファームウェア イメージ (実行中のファームウェア) が含まれていますか。

    デバイスを更新するには、書き込み可能であり、現在アクティブでないスロットが選択されます。 更新プログラムが完了すると、選択したスロットのすべての既存のイメージ データが上書きされます。

2.  選択したスロット用に新しいファームウェア イメージをダウンロードします。 によって、イメージのサイズには、1 つの転送操作で、または画像の部分を複数の連続する転送に発生します。 によって、イメージの一部が制限**min**(*コント ローラーの最大転送サイズ*、512 KB)。
3.  ダウンロードしたイメージをアクティブなファームウェア イメージにするには、するにはスロットに割り当てられます。 アクティブなファームウェア スロットは、現在使用されているスロットからダウンロードしたイメージに割り当てられているスロットに切り替えられます。 、ダウンロードして、ファームウェア イメージの変更の種類に応じて、システムを再起動する必要があります。 これは、NVMe コント ローラーによって決まります。

## <a name="span-idminiportfirmwarecontrolrequestsspanspan-idminiportfirmwarecontrolrequestsspanspan-idminiportfirmwarecontrolrequestsspanminiport-firmware-control-requests"></a><span id="Miniport_firmware_control_requests"></span><span id="miniport_firmware_control_requests"></span><span id="MINIPORT_FIRMWARE_CONTROL_REQUESTS"></span>ミニポート ファームウェア コントロール要求


各関数のコマンドで設定されて、**ファームウェア\_要求\_ブロック**構造に含まれています、 [ **SRB\_IO\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ns-ntddscsi-_srb_io_control)のバッファーで、 [ **IOCTL\_SCSI\_ミニポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_miniport)要求。 **ControlCode**のメンバー **SRB\_IO\_コントロール**に設定されている**IOCTL\_SCSI\_ミニポート\_ファームウェア**をミニポートのファームウェア操作を示します。 各関数のコマンドが後にある関連情報構造、**ファームウェア\_要求\_ブロック**します。 次の表は、各関数のコマンドとシステムのバッファーに含まれる構造体**IOCTL\_SCSI\_ミニポート**します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">入力データ</th>
<th align="left">出力データ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FIRMWARE_FUNCTION_GET_INFO</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_SLOT_INFO</p></td>
</tr>
<tr class="even">
<td align="left"><p>FIRMWARE_FUNCTION_DOWNLOAD</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_DOWNLOAD</p></td>
<td align="left"><p>SRB_IO_CONTROL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FIRMWARE_FUNCTION_ACTIVATE</p></td>
<td align="left"><p>SRB_IO_CONTROL +</p>
<p>FIRMWARE_REQUEST_BLOCK +</p>
<p>STORAGE_FIRMWARE_ACTIVATE</p></td>
<td align="left"><p>SRB_IO_CONTROL</p></td>
</tr>
</tbody>
</table>

 

ファームウェア関数と関連付けられている構造体で定義されます*ntddscsi.h*します。

## <a name="span-idfirmwareslotinformationspanspan-idfirmwareslotinformationspanspan-idfirmwareslotinformationspanfirmware-slot-information"></a><span id="Firmware_slot_information"></span><span id="firmware_slot_information"></span><span id="FIRMWARE_SLOT_INFORMATION"></span>ファームウェア スロット情報


スロットと呼ばれる場所のデバイスでは、ファームウェア イメージが維持されます。 アクティブ化すると、ダウンロードした後に存在するファームウェア イメージの使用可能なスロットを探す必要があります。 使用可能なスロットを探すには、アップグレードのユーティリティは、スロット情報の記述子を受信するデバイスに情報の照会を送信できます。 次の関数の例では、すべてのファームウェア スロットの選択の NVMe デバイスでの情報を取得する方法を示します。

```ManagedCPlusPlus
// A device list item structure for an adapter

typedef struct _DEVICE_LIST {
    HANDLE                      Handle;
    STORAGE_ADAPTER_DESCRIPTOR  AdapterDescriptor;
} DEVICE_LIST, *PDEVICE_LIST;

BOOL
DeviceGetFirmwareInfo(
    _In_ PDEVICE_LIST DeviceList,
    _In_ DWORD        Index,
    _Inout_ PUCHAR    Buffer,
    _In_ DWORD        BufferLength,
    _In_ BOOLEAN      DisplayResult
    )
/*++

Routine Description:

    Retrieve the firmware and firmware slot information from NVMe controller.


Arguments:

    DeviceList    – a pointer to device array that contains disks information.
    Index         – the index of NVMe device in DeviceList array.
    Buffer        – a buffer for input and output.
    BufferLength  – the size of the buffer.
    DisplayResult – print information on screen or not.
  
Return Value:

    BOOLEAN

--*/
{
    BOOL    result;
    ULONG   returnedLength;
    ULONG   firmwareInfoOffset;

    PSRB_IO_CONTROL         srbControl;
    PFIRMWARE_REQUEST_BLOCK firmwareRequest;
    PSTORAGE_FIRMWARE_INFO  firmwareInfo;

    srbControl = (PSRB_IO_CONTROL)Buffer;
    firmwareRequest = (PFIRMWARE_REQUEST_BLOCK)(srbControl + 1);

    //
    // The STORAGE_FIRMWARE_INFO is located after SRB_IO_CONTROL and FIRMWARE_RESQUEST_BLOCK
    //
    firmwareInfoOffset = ((sizeof(SRB_IO_CONTROL) + sizeof(FIRMWARE_REQUEST_BLOCK) - 1) / sizeof(PVOID) + 1) * sizeof(PVOID);

    //
    // Setup the SRB control with the firmware ioctl control info
    //
    srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
    srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
    RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
    srbControl->Timeout = 30;
    srbControl->Length = BufferLength - sizeof(SRB_IO_CONTROL);

    //
    // Set firmware request fields for FIRMWARE_FUNCTION_GET_INFO. This request is to the controller so
    // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
    //
    firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
    firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
    firmwareRequest->Function = FIRMWARE_FUNCTION_GET_INFO;
    firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
    firmwareRequest->DataBufferOffset = firmwareInfoOffset;
    firmwareRequest->DataBufferLength = BufferLength - firmwareInfoOffset;

    //
    // Send the request to get the device firmware info
    //
    result = DeviceIoControl(DeviceList[Index].Handle,
                              IOCTL_SCSI_MINIPORT,
                              Buffer,
                              BufferLength,
                              Buffer,
                              BufferLength,
                              &returnedLength,
                              NULL
                              );

    //
    // Format and display the firmware info
    //
    if (DisplayResult) {
        if (!result) {
            _tprintf(_T("\t Get Firmware Information Failed: 0x%X\n"), GetLastError());
        } else {
            UCHAR   i;
            TCHAR   revision[16] = {0};

            firmwareInfo = (PSTORAGE_FIRMWARE_INFO)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

            _tprintf(_T("\t ----Firmware Information----\n"));
            _tprintf(_T("\t Support upgrade command: %s\n"), firmwareInfo->UpgradeSupport ? _T("Yes") : _T("No"));
            _tprintf(_T("\t Slot Count: %d\n"), firmwareInfo->SlotCount);
            _tprintf(_T("\t Current Active Slot: %d\n"), firmwareInfo->ActiveSlot);

            if (firmwareInfo->PendingActivateSlot == STORAGE_FIRMWARE_INFO_INVALID_SLOT) {
                _tprintf(_T("\t Pending Active Slot: %s\n\n"),  _T("No"));
            } else {
                _tprintf(_T("\t Pending Active Slot: %d\n\n"), firmwareInfo->PendingActivateSlot);
            }

            for (i = 0; i < firmwareInfo->SlotCount; i++) {
                RtlCopyMemory(revision, &firmwareInfo->Slot[i].Revision.AsUlonglong, 8);

                _tprintf(_T("\t\t Slot Number: %d\n"), firmwareInfo->Slot[i].SlotNumber);
                _tprintf(_T("\t\t Slot Read Only: %s\n"), firmwareInfo->Slot[i].ReadOnly ? _T("Yes") : _T("No"));
                _tprintf(_T("\t\t Revision: %s\n"), revision);
                _tprintf(_T("\n"));
            }
        }

        _tprintf(_T("\n"));
    }

    return result;
}
```

配列のスロットの情報が返されます**ストレージ\_ファームウェア\_スロット\_情報**構造体。 各構造体は、アクティブ化の状態およびファームウェア スロットの可用性を示します。 可用性のための条件は次のとおりです。

-   **ReadOnly**メンバーは 0 に設定します。
-   スロットがないアクティブなスロットでスロット番号によって示される、 **ActiveSlot**のメンバー**ストレージ\_ファームウェア\_情報**します。
-   **PendingActiveSlot**のメンバー**ストレージ\_ファームウェア\_情報**記憶域に設定されている\_ファームウェア\_情報\_が無効です\_スロットです。
-   **PendingActiveSlot**のメンバー**ストレージ\_ファームウェア\_情報**目的のスロットに設定されていません。

また、スロットの状態は、可用性のための条件を満たしている場合は、**情報**文字列には、0 以外のバイトである、有効なリビジョン データが含まれていますが、スロットには、有効なファームウェア イメージが含まれていますし、置き換えることができます。 すべての 0 を**情報**文字列が空のスロットを指定します。

## <a name="span-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanspan-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanspan-idexamplefirmwareupgrade-slotselectiondownloadandactivationspanexample-firmware-upgrade---slot-selection-download-and-activation"></a><span id="Example__Firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="example__firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="EXAMPLE__FIRMWARE_UPGRADE_-_SLOT_SELECTION__DOWNLOAD__AND_ACTIVATION"></span>例:ファームウェアのアップグレードのスロットの選択、ダウンロード、およびアクティブ化


アップグレードのユーティリティでは、コント ローラーのファームウェアを更新する前に説明した 3 つの手順を実行します。 たとえば、次のアップグレードのルーチンには、プロセスの各手順のコードが含まれています。 示すように、スロット検出手順、 *DeviceGetFirmwareInfo*の例では、使用可能なスロットを選択するアップグレード ルーチンによって呼び出されます。 イメージのダウンロードとアクティブ化の手順では、スロットの選択範囲の直後を説明します。 ステップごとに関数の対応するコマンドの使用が表示されます。

ダウンロードの手順の中にファームウェア イメージのファイルは、割り当てられたバッファーに読み取るし、バッファーの内容は、コント ローラーに転送されます。 ファームウェア イメージのファイルが、バッファーのサイズよりも大きい場合は、イメージ ファイルには、複数回は読み取り専用し、ファイル全体が読み取られるまで、ファームウェア イメージの部分は転送されます。

ファームウェア イメージのダウンロードが完了した後、アクティブ化の手順には、コント ローラーから 2 つのアクションが必要です。 最初に、ファームウェア イメージを選択したスロットが割り当てられているし、アクティブなスロットとして選択したスロットを設定する第 2 に、します。

```ManagedCPlusPlus
VOID
DeviceFirmwareUpgrade(
    _In_ PDEVICE_LIST DeviceList,
    _In_ DWORD        Index,
    _In_ TCHAR*       FileName
    )
/*++

Routine Description:

    Performs a firmware upgrade to the NVMe controller. The an available firmware
    slot is selected, the firmware is downloaded to the controller from an image
    file, and the new firmware is activated.


Arguments:

    DeviceList    – a pointer to device array that contains disks information.
    Index         – the index of NVMe device in DeviceList array.
    FileName      – the name of the firmware upgrade image file.
  
Return Value:

    None

--*/
{
    BOOL                    result;
    PUCHAR                  buffer = NULL;
    ULONG                   bufferSize;
    ULONG                   firmwareStructureOffset;
    ULONG                   imageBufferLength;

    PSRB_IO_CONTROL         srbControl;
    PFIRMWARE_REQUEST_BLOCK firmwareRequest;

    PSTORAGE_FIRMWARE_INFO      firmwareInfo;
    PSTORAGE_FIRMWARE_DOWNLOAD  firmwareDownload;
    PSTORAGE_FIRMWARE_ACTIVATE  firmwareActivate;

    ULONG                   slotNumber;
    ULONG                   returnedLength;
    ULONG                   i;

    HANDLE                  fileHandle = NULL;
    ULONG                   imageOffset;
    ULONG                   readLength;
    BOOLEAN                 moreToDownload;

    //
    // The STORAGE_FIRMWARE_INFO is located after SRB_IO_CONTROL and FIRMWARE_RESQUEST_BLOCK
    //
    firmwareStructureOffset = ((sizeof(SRB_IO_CONTROL) + sizeof(FIRMWARE_REQUEST_BLOCK) - 1) / sizeof(PVOID) + 1) * sizeof(PVOID);

    //
    // The Max Transfer Length limits the part of buffer that may need to transfer to controller, not the whole buffer.
    //
    bufferSize = min(DeviceList[Index].AdapterDescriptor.MaximumTransferLength, 2 * 1024 * 1024);
    bufferSize += firmwareStructureOffset;
    bufferSize += FIELD_OFFSET(STORAGE_FIRMWARE_DOWNLOAD, ImageBuffer);

    buffer = (PUCHAR)malloc(bufferSize);
    if (buffer == NULL) {
        _tprintf(_T("\t FirmwareUpgrade - Allocate buffer failed: 0x%X\n"), GetLastError());
        return;
    }

    //
    // calculate the space available for the firmware image portion of the buffer allocation
    // 
    imageBufferLength = bufferSize - firmwareStructureOffset - sizeof(STORAGE_FIRMWARE_DOWNLOAD);

    RtlZeroMemory(buffer, bufferSize);

    // ---------------------------------------------------------------------------
    // ( 1 ) SELECT A SUITABLE FIRMWARE SLOT
    // ---------------------------------------------------------------------------

    //
    // Get firmware slot information data.
    //
    result = DeviceGetFirmwareInfo(DeviceList, Index, buffer, bufferSize, FALSE);

    if (result == FALSE) {
        _tprintf(_T("\t FirmwareUpgrade: Get Firmware Information Failed: 0x%X\n"), GetLastError());
        goto Exit;
    }

    //
    // Set the request structure pointers
                //
    srbControl = (PSRB_IO_CONTROL)buffer;
    firmwareRequest = (PFIRMWARE_REQUEST_BLOCK)(srbControl + 1);
    firmwareInfo = (PSTORAGE_FIRMWARE_INFO)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

    if (srbControl->ReturnCode != FIRMWARE_STATUS_SUCCESS) {
        _tprintf(_T("\t FirmwareUpgrade - get firmware info failed. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        goto Exit;
    }

    //
    // SelectFind the first writable slot.
    //
    slotNumber = (ULONG)-1;

    if (firmwareInfo->UpgradeSupport) {
        for (i = 0; i < firmwareInfo->SlotCount; i++) {
            if (firmwareInfo->Slot[i].ReadOnly == FALSE) {
                slotNumber = firmwareInfo->Slot[i].SlotNumber;
                break;
            }
        }
    }

    //
    // If no writable slot is found, bypass downloading and activation
    //
    if (slotNumber == (ULONG)-1) {
        _tprintf(_T("\t FirmwareUpgrade - No writable Firmware slot.\n"));
        goto Exit;
    }

    // ---------------------------------------------------------------------------
    // ( 2 ) DOWNLOAD THE FIRMWARE IMAGE TO THE CONTROLLER
    // ---------------------------------------------------------------------------

    //
    // initialize image length and offset
    //
    imageBufferLength = (imageBufferLength / sizeof(PVOID)) * sizeof(PVOID);
    imageOffset = 0;
    readLength = 0;
    moreToDownload = TRUE;

    //
    // Open image file and download it to controller.
    //
    if (FileName == NULL) {
        _tprintf(_T("\t FirmwareUpgrade - No firmware file specified.\n"));
        goto Exit;
    }

    fileHandle = CreateFile(FileName,              // file to open
                            GENERIC_READ,          // open for reading
                            FILE_SHARE_READ,       // share for reading
                            NULL,                  // default security
                            OPEN_EXISTING,         // existing file only
                            FILE_ATTRIBUTE_NORMAL, // normal file
                            NULL);                 // no attr. template

    if (fileHandle == INVALID_HANDLE_VALUE) {
        _tprintf(_T("\t FirmwareUpgrade - unable to open file \"%s\" for read.\n"), FileName);
        goto Exit;
    }

    //
    // Read and download the firmware from the image file into image buffer length portions. Send the
    // image portion to the controller.
    //
    while (moreToDownload) {

        RtlZeroMemory(buffer, bufferSize);

        //
        // Setup the SRB control with the firmware ioctl control info
        //
        srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
        srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
        RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
        srbControl->Timeout = 30;
        srbControl->Length = bufferSize - sizeof(SRB_IO_CONTROL);

        //
        // Set firmware request fields for FIRMWARE_FUNCTION_DOWNLOAD. This request is to the controller so
        // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
        //
        firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
        firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
        firmwareRequest->Function = FIRMWARE_FUNCTION_DOWNLOAD;
        firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
        firmwareRequest->DataBufferOffset = firmwareStructureOffset;
        firmwareRequest->DataBufferLength = bufferSize - firmwareStructureOffset;

        //
        // Initialize the firmware data buffer pointer to the proper position after the request structure
        //
        firmwareDownload = (PSTORAGE_FIRMWARE_DOWNLOAD)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

        if (ReadFile(fileHandle, firmwareDownload->ImageBuffer, imageBufferLength, &readLength, NULL) == FALSE) {
            _tprintf(_T("\t FirmwareUpgrade - Read firmware file failed.\n"));
            goto Exit;
        }

        if (readLength == 0) {
            moreToDownload = FALSE;
            break;
        }

        if ((readLength % sizeof(ULONG)) != 0) {
            _tprintf(_T("\t FirmwareUpgrade - Read firmware file failed.\n"));
        }

        //
        // Set the download parameters and adjust the offset for this portion of the firmware image
        //
        firmwareDownload->Version = 1;
        firmwareDownload->Size = sizeof(STORAGE_FIRMWARE_DOWNLOAD);
        firmwareDownload->Offset = imageOffset;
        firmwareDownload->BufferSize = readLength;

        //
        // download this portion of firmware to the device
        //
        result = DeviceIoControl(DeviceList[Index].Handle,
                                 IOCTL_SCSI_MINIPORT,
                                 buffer,
                                 bufferSize,
                                 buffer,
                                 bufferSize,
                                 &returnedLength,
                                 NULL
                                 );

        if (result == FALSE) {
            _tprintf(_T("\t FirmwareUpgrade - IOCTL - firmware download failed. 0x%X.\n"), GetLastError());
            goto Exit;
        }

        if (srbControl->ReturnCode != FIRMWARE_STATUS_SUCCESS) {
            _tprintf(_T("\t FirmwareUpgrade - firmware download failed. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
            goto Exit;
        }

        //
        // Update Image Offset for next iteration.
        //
        imageOffset += readLength;
    }

    // ---------------------------------------------------------------------------
    // ( 3 ) ACTIVATE THE FIRMWARE SLOT ASSIGNED TO THE UPGRADE
    // ---------------------------------------------------------------------------

    //
    // Activate the newly downloaded image with the assigned slot.
    //
    RtlZeroMemory(buffer, bufferSize);

    //
    // Setup the SRB control with the firmware ioctl control info
    //
    srbControl->HeaderLength = sizeof(SRB_IO_CONTROL);
    srbControl->ControlCode = IOCTL_SCSI_MINIPORT_FIRMWARE;
    RtlMoveMemory(srbControl->Signature, IOCTL_MINIPORT_SIGNATURE_FIRMWARE, 8);
    srbControl->Timeout = 30;
    srbControl->Length = bufferSize - sizeof(SRB_IO_CONTROL);

    //
    // Set firmware request fields for FIRMWARE_FUNCTION_ACTIVATE. This request is to the controller so
    // FIRMWARE_REQUEST_FLAG_CONTROLLER is set in the flags
    //
    firmwareRequest->Version = FIRMWARE_REQUEST_BLOCK_STRUCTURE_VERSION;
    firmwareRequest->Size = sizeof(FIRMWARE_REQUEST_BLOCK);
    firmwareRequest->Function = FIRMWARE_FUNCTION_ACTIVATE;
    firmwareRequest->Flags = FIRMWARE_REQUEST_FLAG_CONTROLLER;
    firmwareRequest->DataBufferOffset = firmwareStructureOffset;
    firmwareRequest->DataBufferLength = bufferSize - firmwareStructureOffset;

    //
    // Initialize the firmware activation structure pointer to the proper position after the request structure
    //
    firmwareActivate = (PSTORAGE_FIRMWARE_ACTIVATE)((PUCHAR)srbControl + firmwareRequest->DataBufferOffset);

    //
    // Set the activation parameters with the available slot selected
    //
    firmwareActivate->Version = 1;
    firmwareActivate->Size = sizeof(STORAGE_FIRMWARE_ACTIVATE);
    firmwareActivate->SlotToActivate = (UCHAR)slotNumber;

    //
    // Send the activation request
    //
    result = DeviceIoControl(DeviceList[Index].Handle,
                                IOCTL_SCSI_MINIPORT,
                                buffer,
                                bufferSize,
                                buffer,
                                bufferSize,
                                &returnedLength,
                                NULL
                                );


    if (result == FALSE) {
        _tprintf(_T("\t FirmwareUpgrade - IOCTL - firmware activate failed. 0x%X.\n"), GetLastError());
        goto Exit;
    }

    //
    // Display status result from firmware activation
    //
    switch (srbControl->ReturnCode) {
    case FIRMWARE_STATUS_SUCCESS:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate succeeded.\n"));
        break;

    case FIRMWARE_STATUS_POWER_CYCLE_REQUIRED:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate succeeded. PLEASE REBOOT COMPUTER.\n"));
        break;

    case FIRMWARE_STATUS_ILLEGAL_REQUEST:
    case FIRMWARE_STATUS_INVALID_PARAMETER:
    case FIRMWARE_STATUS_INPUT_BUFFER_TOO_BIG:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate parameter error. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        break;

    case FIRMWARE_STATUS_INVALID_SLOT:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, slot number invalid.\n"));
        break;

    case FIRMWARE_STATUS_INVALID_IMAGE:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, invalid firmware image.\n"));
        break;

    case FIRMWARE_STATUS_ERROR:
    case FIRMWARE_STATUS_CONTROLLER_ERROR:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, error returned.\n"));
        break;

    default:
        _tprintf(_T("\t FirmwareUpgrade - firmware activate, unexpected error. srbControl->ReturnCode %d.\n"), srbControl->ReturnCode);
        break;
   }

Exit:

    if (fileHandle != NULL) {
        CloseHandle(fileHandle);
    }

    if (buffer != NULL) {
        free(buffer);
    }

    return;
}
```

**注**  同時に複数のファームウェア イメージをダウンロードすることはできません。 1 つのファームウェアのダウンロードでは 1 つのファームウェアのアクティブ化を常が続きます。

 

既にスロットに常駐しているファームウェア イメージは、対応するスロット番号をアクティブ化関数のコマンドだけを使用して再びアクティブにできます。

**IOCTL\_SCSI\_ミニポート\_ファームウェア**SRB I/O コントロールのコントロールのコードは、Windows 8.1 以降から使用できます。

 

 




