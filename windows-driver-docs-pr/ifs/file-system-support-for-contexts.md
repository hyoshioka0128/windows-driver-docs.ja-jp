---
title: ファイル システムによるコンテキストのサポート
description: ファイル システムによるコンテキストのサポート
ms.assetid: 661ee3ff-3171-4d1e-a8fe-8d1852c5e990
keywords:
- コンテキストの WDK のファイル システム ミニフィルター、ファイル システムのサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b4b007414586d130a5df91204fbf19dce08fc1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369253"
---
# <a name="file-system-support-for-contexts"></a>ファイル システムによるコンテキストのサポート

使用する必要があります (該当する) 場合は、ファイルのコンテキストをサポートするには、ストリームのコンテキスト、およびファイル オブジェクト (ストリームのハンドル) のコンテキスト、ファイル システム、 [ **FSRTL\_詳細\_FCB\_ヘッダー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造体。 すべての Microsoft Windows ファイル システムは、この構造体を使用して、サード パーティ製のファイル システムのすべての開発者はでもを強くお勧めします。 詳細については、次を参照してください。 [ **FsRtlSetupAdvancedHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff547257)と**FSRTL\_詳細\_FCB\_ヘッダー**します。

NTFS および FAT ファイル システムはサポートしませんファイル、ストリーム、またはファイル オブジェクトのコンテキストの pre-create または閉じる後のパス、または、ページング ファイルに[ **IRP\_MJ\_ネットワーク\_クエリ\_開いている**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-network-query-open)操作。

ミニフィルター ドライバーをファイル システムがサポートするかストリーム コンテキストやファイル オブジェクトの指定されたファイル オブジェクト呼び出すことによって調べる[ **FltSupportsStreamContexts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)と[ **FltSupportsStreamHandleContexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)、それぞれします。

ファイルのコンテキストとは、以降 Windows Vista で利用可能です。

ファイルあたり 1 つのデータ ストリームのみをサポートする (例: FAT) ファイル システム、ファイルのコンテキストでは、ストリームのコンテキストと同じです。 通常、このようなファイル システムは、ストリーム コンテキストをサポートが、ファイルのコンテキストをサポートしていません。 代わりに、フィルター マネージャーでは、このサポートが提供ストリーム コンテキストをファイル システムの既存のサポートを使用します。 ミニフィルター ドライバーのインスタンスがこれらのファイル システムに接続されている[ **FltSupportsFileContexts** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsfilecontexts)返します**FALSE**、中に[ **FltSupportsFileContextsEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltsupportsfilecontextsex)返します**TRUE** (有効な場合以外**NULL**値が渡される、*インスタンス*パラメーターの場合)。

コンテキストの種類がファイルでサポートされていない場合、ミニフィルターはそのファイルにその型のコンテキストをアタッチできません。

ファイルのコンテキストをサポートするために、ファイル システムが必要です。

* 埋め込みを**FileContextSupportPointer**型 PVOID でそのファイルの context 構造は、通常、ファイル コンテキスト ブロック (FCB) のメンバー。 ファイル システムにこのメンバーを初期化する必要があります**NULL**します。

* 使用**FsRtlSetupAdvancedHeaderEx** (の代わりに[ **FsRtlSetupAdvancedHeader**](https://msdn.microsoft.com/library/windows/hardware/ff547257))、に有効なポインターを渡すストリームコンテキスト構造を初期化するために**FileContextSupportPointer** (ファイル コンテキストの対応する構造体に埋め込まれた) のメンバー、 *FileContextSupportPointer*パラメーター。 詳細については、次を参照してください。 **FsRtlSetupAdvancedHeaderEx**と[ **FSRTL\_詳細\_FCB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)します。

* 呼び出す**FsRtlTeardownPerFileContexts**をファイル システムがファイルのファイル コンテキスト構造を削除するときにファイルを使用してフィルターとミニフィルター ドライバーが関連付けられているすべてのファイル コンテキスト構造体を解放します。