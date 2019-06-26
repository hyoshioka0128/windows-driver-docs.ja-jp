---
title: ミニフィルター ドライバーで生成された I/O 要求
description: ミニフィルター ドライバーで生成された I/O 要求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター ドライバーによって生成される I/O 要求
- I/O 要求の WDK ファイル システム
- Irp WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde83f45cf2c9ff7ba6bdbe0b5a328383920e9a7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375705"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>ミニフィルター ドライバーで生成された I/O 要求


ミニフィルター ドライバーでは、生成でき、現在のボリュームまたは別のボリューム ドライバーのインスタンス、ミニフィルターのいずれかから IRP ベースの I/O 要求を送信することができます。 生成される I/O とファイル システム ミニフィルター ドライバーのインスタンスと、指定したインスタンスの下に接続されているレガシ フィルター ドライバーによってのみが表示されます。 これは、レガシ フィルター ドライバー モデルが表示され、以降、最上位のドライバーでは、全体のファイル システム スタックを介して移動する必要がある I/O レガシ フィルター ドライバーによって生成された要求で再帰 I/O に関連する多くの問題を解決します。

フィルター マネージャーは、その未処理の I/O 操作のすべてが完了するまで、ミニフィルター ドライバーをアンロードしません。

### <a name="span-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>ミニフィルター ドライバーによって生成される I/O 要求のフィルター マネージャー ルーチン

フィルター マネージャーでは、作成、開く、読み取り、およびファイルの書き込みの次のサポート ルーチンを提供します。

[**FltClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltclose)

[**FltCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefile)

[**FltCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcreatefileex)

[**FltReadFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreadfile)

[**FltWriteFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltwritefile)

設定し、再解析ポイントを削除するのには、次のサポート ルーチンが用意されています。

[**FltTagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-flttagfile)

[**FltUntagFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltuntagfile)

次のサポート ルーチンは、I/O 要求を生成するために用意されています。

[*FltAllocateCallbackData*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltallocatecallbackdata)

[**FltFreeCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfreecallbackdata)

[**FltPerformAsynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltperformasynchronousio)

[*FltPerformSynchronousIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltperformsynchronousio)

[**FltReuseCallbackData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreusecallbackdata)

ファイルのオープン要求をキャンセルして、I/O 要求を再発行の次のサポート ルーチンが提供されます。

[**FltCancelFileOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltcancelfileopen)

[**FltReissueSynchronousIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltreissuesynchronousio)

フィルター マネージャーは、次の汎用ルーチンを提供しています。

[**FltDeviceIoControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltdeviceiocontrolfile)

[**FltFlushBuffers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltflushbuffers)

[**FltFsControlFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)

[**FltQueryInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryinformationfile)

[**FltQuerySecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltquerysecurityobject)

[**FltQueryVolumeInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltqueryvolumeinformationfile)

[**FltSetInformationFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetinformationfile)

[**FltSetSecurityObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsetsecurityobject)

 

 




