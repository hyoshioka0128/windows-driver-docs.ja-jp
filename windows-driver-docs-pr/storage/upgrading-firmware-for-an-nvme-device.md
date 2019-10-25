---
title: NVMe デバイス用ファームウェアのアップグレード
description: NVMe ストレージデバイスのファームウェアに対する更新は、そのデバイスのミニポートドライバーに発行されます。
ms.assetid: A912715A-F82A-41E5-BE14-5B17930C29B7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fae5703910c981967d2ac6a416532e2ea07cc570
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844444"
---
# <a name="upgrading-firmware-for-an-nvme-device"></a>NVMe デバイス用ファームウェアのアップグレード


NVMe ストレージデバイスのファームウェアに対する更新は、そのデバイスのミニポートドライバーに発行されます。 ファームウェア情報を取得したり、ファームウェアイメージをダウンロードしたり、アクティブにしたりするための関数コマンドが、ミニポートに発行されます。

## <a name="span-idfirmware_upgrade_processspanspan-idfirmware_upgrade_processspanspan-idfirmware_upgrade_processspanfirmware-upgrade-process"></a><span id="Firmware_upgrade_process"></span><span id="firmware_upgrade_process"></span><span id="FIRMWARE_UPGRADE_PROCESS"></span>ファームウェアのアップグレードプロセス


Windows 用に認定された NVMe デバイスは、デバイスの操作中にファームウェアを更新できます。 ファームウェアは、SRB でフォーマットされた関連するファームウェアコントロールデータを含む[**IOCTL\_SCSI\_ミニポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_miniport)要求を使用して更新されます。 更新プロセスは次のとおりです。

1.  ファームウェアスロット情報を収集して、更新を配置する場所を決定します。 ファームウェアの更新プログラムが存在する場所を決定する際には、いくつかの考慮事項があります。

    -   使用できるスロットの数を確認できます。
    -   更新プログラムを保持できるスロットの数を確認できます。 一部のスロットは読み取り専用であるか、前のイメージに戻す機能が必要な場合に保持する必要があるイメージを保持しています。
    -   現在アクティブなファームウェアイメージを含むスロット (実行中のファームウェア)

    デバイスを更新するために、書き込み可能で現在アクティブでないスロットが選択されています。 更新が完了すると、選択したスロット内の既存のイメージデータはすべて上書きされます。

2.  選択したスロットの新しいファームウェアイメージをダウンロードします。 イメージのサイズに応じて、1回の転送操作で、またはイメージの複数の部分の連続した転送で発生します。 イメージの一部は、**最小値**(コントローラーの*最大転送サイズ*である 512 KB) によって制限されます。
3.  ダウンロードしたイメージをアクティブなファームウェアイメージにするために、スロットに割り当てられます。 アクティブなファームウェアスロットは、現在使用されているスロットから、ダウンロードしたイメージに割り当てられているスロットに切り替わります。 ダウンロードの種類とファームウェアイメージの変更によっては、システムの再起動が必要になる場合があります。 これは、NVMe コントローラーによって決定されます。

## <a name="span-idminiport_firmware_control_requestsspanspan-idminiport_firmware_control_requestsspanspan-idminiport_firmware_control_requestsspanminiport-firmware-control-requests"></a><span id="Miniport_firmware_control_requests"></span><span id="miniport_firmware_control_requests"></span><span id="MINIPORT_FIRMWARE_CONTROL_REQUESTS"></span>ミニポートファームウェアコントロール要求


各関数コマンドは、**ファームウェア\_要求\_ブロック**構造で設定されます。これは、 [**IOCTL\_SCSI\_ミニポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_scsi_miniport)要求のバッファー内の[**SRB\_IO\_制御**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ns-ntddscsi-_srb_io_control)に含まれています。 **SRB\_IO\_CONTROL**の**controlcode**メンバーは、ミニポートファームウェア操作を示すために、 **SCSI\_ミニポート\_ファームウェア\_IOCTL**に設定されています。 各関数コマンドには、**ファームウェア\_要求\_ブロック**の後にある関連情報構造があります。 次の表は、各関数コマンドと、 **IOCTL\_SCSI\_ミニポート**のシステムバッファーに含まれる構造体を示しています。

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

 

ファームウェアの関数と関連する構造体は、 *ntddscsi*で定義されています。

## <a name="span-idfirmware_slot_informationspanspan-idfirmware_slot_informationspanspan-idfirmware_slot_informationspanfirmware-slot-information"></a><span id="Firmware_slot_information"></span><span id="firmware_slot_information"></span><span id="FIRMWARE_SLOT_INFORMATION"></span>ファームウェアスロットの情報


ファームウェアイメージは、デバイス上のスロットと呼ばれる場所に保持されます。 ダウンロード後にライセンス認証されたファームウェアイメージが存在する場合は、そのスロットを見つける必要があります。 使用可能なスロットを見つけるために、アップグレードユーティリティは、デバイスに情報クエリを送信して、スロット情報記述子を受け取ることができます。 次の関数の例は、選択した NVMe デバイス上のすべてのファームウェアスロットに関する情報を取得する方法を示しています。

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

スロット情報は、**ストレージ\_ファームウェア\_スロット\_情報**構造体の配列に返されます。 各構造体は、ファームウェアスロットのアクティブ化の状態と可用性を示します。 可用性の条件は次のとおりです。

-   **ReadOnly**メンバーは0に設定されます。
-   スロットが、**ストレージ\_ファームウェア\_情報**の**activeslot**メンバーのスロット番号で示されているアクティブなスロットではありません。
-   **Storage\_ファームウェアの\_情報**の**Pendingactiveslot**のメンバーが、無効な\_スロット\_\_ファームウェア\_情報に設定されています。
-   **ストレージ\_ファームウェア\_情報**の**Pendingactiveslot**のメンバーが目的のスロットに設定されていません。

また、スロットの状態が可用性の条件を満たしていても、**情報**文字列に有効なリビジョンデータ (0 以外のバイト) が含まれている場合、スロットに有効なファームウェアイメージが含まれていますが、置き換えられる可能性があります。 **Info**文字列内のすべてのゼロは、空のスロットを示します。

## <a name="span-idexample__firmware_upgrade_-_slot_selection__download__and_activationspanspan-idexample__firmware_upgrade_-_slot_selection__download__and_activationspanspan-idexample__firmware_upgrade_-_slot_selection__download__and_activationspanexample-firmware-upgrade---slot-selection-download-and-activation"></a><span id="Example__Firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="example__firmware_upgrade_-_slot_selection__download__and_activation"></span><span id="EXAMPLE__FIRMWARE_UPGRADE_-_SLOT_SELECTION__DOWNLOAD__AND_ACTIVATION"></span>例: ファームウェアのアップグレード-スロットの選択、ダウンロード、アクティブ化


アップグレードユーティリティは、前に説明した3つの手順を実行して、コントローラーのファームウェアを更新します。 例として、次のアップグレードルーチンには、プロセスの各ステップのコードが含まれています。 *DeviceGetFirmwareInfo*の例に示すスロット検出手順は、使用可能なスロットを選択するためにアップグレードルーチンによって呼び出されます。 イメージのダウンロードとアクティブ化の手順は、スロットの選択に直接従って示されています。 各ステップ内では、対応する関数コマンドの使用方法が示されています。

ダウンロード手順では、割り当てられたバッファーにファームウェアイメージファイルが読み込まれ、バッファーの内容がコントローラーに転送されます。 ファームウェアイメージファイルがバッファーのサイズより大きい場合は、イメージファイルが複数回読み取られ、ファームウェアイメージのその部分がファイル全体が読み取られるまで転送されます。

ファームウェアイメージのダウンロードが完了したら、ライセンス認証の手順を実行するには、コントローラーからの2つの操作が必要です。 まず、選択したスロットがファームウェアイメージに割り当てられ、2番目に選択したスロットがアクティブスロットとして設定されます。

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

複数のファームウェアイメージを同時にダウンロードする**こと**はサポートされていません  。 1つのファームウェアのダウンロードには、常に1つのファームウェアライセンス認証が適用されます。

 

スロットに既に存在するファームウェアイメージを再アクティブ化するには、対応するスロット番号と共に activate function コマンドだけを使用します。

SRB i/o コントロールの**IOCTL\_SCSI\_ミニポート\_ファームウェア**制御コードは、Windows 8.1 以降で使用できます。

 

 




