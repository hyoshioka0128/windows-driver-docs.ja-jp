---
title: ミニフィルター ドライバーで生成された I/O 要求
description: ミニフィルター ドライバーで生成された I/O 要求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- フィルターマネージャー WDK ファイルシステムミニフィルター、ドライバーによって生成された i/o 要求
- I/o 要求 (WDK ファイルシステム)
- Irp WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc433f3de2e15430a3c63edd6cd38ce8184b3432
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841212"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>ミニフィルター ドライバーで生成された I/O 要求


ミニフィルタードライバーは、現在のボリュームまたは別のボリューム上にあるミニフィルタードライバー独自のインスタンスから、IRP ベースの i/o 要求を生成して送信することができます。 生成された i/o は、指定したインスタンスの下、およびファイルシステムによって接続された、ミニフィルタードライバーインスタンスとレガシフィルタードライバーによってのみ表示されます。 これにより、レガシフィルタードライバーモデルの再帰 i/o に関連する多くの問題が解決されます。レガシフィルタードライバーによって生成される i/o 要求は、最上位のドライバーから順にファイルシステムスタック全体を通過する必要があります。

フィルターマネージャーは、未処理のすべての i/o 操作が完了するまでミニフィルタードライバーをアンロードしません。

### <a name="span-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanspan-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanspan-idfilter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>ミニフィルタードライバーによって生成される i/o 要求のフィルターマネージャールーチン

フィルターマネージャーには、ファイルの作成、開く、読み取り、および書き込みを行うための次のサポートルーチンが用意されています。

[**FltClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclose)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[**FltCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefileex)

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreadfile)

[**FltWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltwritefile)

再解析ポイントの設定と削除には、次のサポートルーチンが用意されています。

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltuntagfile)

I/o 要求を生成するために、次のサポートルーチンが用意されています。

[*FltAllocateCallbackData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltallocatecallbackdata)

[**FltFreeCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfreecallbackdata)

[**FltPerformAsynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformasynchronousio)

[*FltPerformSynchronousIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltperformsynchronousio)

[**FltReuseCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreusecallbackdata)

ファイルオープン要求をキャンセルし、i/o 要求を再発行するために、次のサポートルーチンが用意されています。

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltreissuesynchronousio)

フィルターマネージャーには、次の汎用ルーチンも用意されています。

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltflushbuffers)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**FltQuerySecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltquerysecurityobject)

[**FltQueryVolumeInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltqueryvolumeinformationfile)

[**FltSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetinformationfile)

[**FltSetSecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetsecurityobject)

 

 




