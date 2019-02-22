---
title: ミニフィルター ドライバーによって生成される I/O 要求
description: ミニフィルター ドライバーによって生成される I/O 要求
ms.assetid: cf06dcb9-58e2-4341-8229-8f172f37c176
keywords:
- フィルター マネージャー WDK ファイル システム ミニフィルター ドライバーによって生成される I/O 要求
- I/O 要求の WDK ファイル システム
- Irp WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cee420f417f842a34155f79361d96329b68c03a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527771"
---
# <a name="io-requests-generated-by-the-minifilter-driver"></a>ミニフィルター ドライバーによって生成される I/O 要求


ミニフィルター ドライバーでは、生成でき、現在のボリュームまたは別のボリューム ドライバーのインスタンス、ミニフィルターのいずれかから IRP ベースの I/O 要求を送信することができます。 生成される I/O とファイル システム ミニフィルター ドライバーのインスタンスと、指定したインスタンスの下に接続されているレガシ フィルター ドライバーによってのみが表示されます。 これは、レガシ フィルター ドライバー モデルが表示され、以降、最上位のドライバーでは、全体のファイル システム スタックを介して移動する必要がある I/O レガシ フィルター ドライバーによって生成された要求で再帰 I/O に関連する多くの問題を解決します。

フィルター マネージャーは、その未処理の I/O 操作のすべてが完了するまで、ミニフィルター ドライバーをアンロードしません。

### <a name="span-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanspan-idfiltermanagerroutinesforiorequestsgeneratedbytheminifilterdriverspanfilter-manager-routines-for-io-requests-generated-by-the-minifilter-driver"></a><span id="Filter_Manager_Routines_for_I_O_Requests_Generated_by_the_Minifilter_Driver"></span><span id="filter_manager_routines_for_i_o_requests_generated_by_the_minifilter_driver"></span><span id="FILTER_MANAGER_ROUTINES_FOR_I_O_REQUESTS_GENERATED_BY_THE_MINIFILTER_DRIVER"></span>ミニフィルター ドライバーによって生成される I/O 要求のフィルター マネージャー ルーチン

フィルター マネージャーでは、作成、開く、読み取り、およびファイルの書き込みの次のサポート ルーチンを提供します。

[**FltClose**](https://msdn.microsoft.com/library/windows/hardware/ff541863)

[**FltCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff541935)

[**FltCreateFileEx**](https://msdn.microsoft.com/library/windows/hardware/ff541937)

[**FltReadFile**](https://msdn.microsoft.com/library/windows/hardware/ff544286)

[**FltWriteFile**](https://msdn.microsoft.com/library/windows/hardware/ff544610)

設定し、再解析ポイントを削除するのには、次のサポート ルーチンが用意されています。

[**FltTagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544589)

[**FltUntagFile**](https://msdn.microsoft.com/library/windows/hardware/ff544608)

次のサポート ルーチンは、I/O 要求を生成するために用意されています。

[*FltAllocateCallbackData*](https://msdn.microsoft.com/library/windows/hardware/ff541703)

[**FltFreeCallbackData**](https://msdn.microsoft.com/library/windows/hardware/ff542949)

[**FltPerformAsynchronousIo**](https://msdn.microsoft.com/library/windows/hardware/ff543420)

[*FltPerformSynchronousIo*](https://msdn.microsoft.com/library/windows/hardware/ff543421)

[**FltReuseCallbackData**](https://msdn.microsoft.com/library/windows/hardware/ff544358)

ファイルのオープン要求をキャンセルして、I/O 要求を再発行の次のサポート ルーチンが提供されます。

[**FltCancelFileOpen**](https://msdn.microsoft.com/library/windows/hardware/ff541784)

[**FltReissueSynchronousIo**](https://msdn.microsoft.com/library/windows/hardware/ff544311)

フィルター マネージャーは、次の汎用ルーチンを提供しています。

[**FltDeviceIoControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542046)

[**FltFlushBuffers**](https://msdn.microsoft.com/library/windows/hardware/ff542099)

[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**FltQueryInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff543439)

[**FltQuerySecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff543441)

[**FltQueryVolumeInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff543446)

[**FltSetInformationFile**](https://msdn.microsoft.com/library/windows/hardware/ff544516)

[**FltSetSecurityObject**](https://msdn.microsoft.com/library/windows/hardware/ff544538)

 

 




