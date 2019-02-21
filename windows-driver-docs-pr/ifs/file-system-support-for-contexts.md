---
title: コンテキストのファイル システムのサポート
description: コンテキストのファイル システムのサポート
ms.assetid: 661ee3ff-3171-4d1e-a8fe-8d1852c5e990
keywords:
- コンテキストの WDK のファイル システム ミニフィルター、ファイル システムのサポートします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c30420f431141880fde51b43a24720639408660c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550240"
---
# <a name="file-system-support-for-contexts"></a>コンテキストのファイル システムのサポート


## <span id="ddk_registering_the_minifilter_if"></span><span id="DDK_REGISTERING_THE_MINIFILTER_IF"></span>


使用する必要があります (該当する) 場合は、ファイルのコンテキストをサポートするには、ストリームのコンテキスト、およびファイル オブジェクト (ストリームのハンドル) のコンテキスト、ファイル システム、 [ **FSRTL\_詳細\_FCB\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff547334)構造体。 すべての Microsoft Windows ファイル システムは、この構造体を使用して、サード パーティ製のファイル システムのすべての開発者はでもを強くお勧めします。 詳細については、次を参照してください。 [ **FsRtlSetupAdvancedHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff547257)と**FSRTL\_詳細\_FCB\_ヘッダー**します。

NTFS および FAT ファイル システムはサポートしませんファイル、ストリーム、またはファイル オブジェクトのコンテキストの pre-create または閉じる後のパス、または、ページング ファイルに[ **IRP\_MJ\_ネットワーク\_クエリ\_開いている**](https://msdn.microsoft.com/library/windows/hardware/ff544731)操作。

ミニフィルター ドライバーをファイル システムがサポートするかストリーム コンテキストやファイル オブジェクトの指定されたファイル オブジェクト呼び出すことによって調べる[ **FltSupportsStreamContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff544581)と[ **FltSupportsStreamHandleContexts**](https://msdn.microsoft.com/library/windows/hardware/ff544586)、それぞれします。

ファイルのコンテキストとは、以降 Windows Vista で利用可能です。

ファイルあたり 1 つのデータ ストリームのみをサポートする (例: FAT) ファイル システム、ファイルのコンテキストでは、ストリームのコンテキストと同じです。 通常、このようなファイル システムは、ストリーム コンテキストをサポートが、ファイルのコンテキストをサポートしていません。 代わりに、フィルター マネージャーでは、このサポートが提供ストリーム コンテキストをファイル システムの既存のサポートを使用します。 ミニフィルター ドライバーのインスタンスがこれらのファイル システムに接続されている[ **FltSupportsFileContexts** ](https://msdn.microsoft.com/library/windows/hardware/ff544574)返します**FALSE**、中に[ **FltSupportsFileContextsEx** ](https://msdn.microsoft.com/library/windows/hardware/ff544576)返します**TRUE** (有効な場合以外**NULL**値が渡される、*インスタンス*パラメーターの場合)。

ファイルのコンテキストをサポートするために、ファイル システムが必要です。

-   埋め込みを**FileContextSupportPointer**型 PVOID でそのファイルの context 構造は、通常、ファイル コンテキスト ブロック (FCB) のメンバー。 ファイル システムにこのメンバーを初期化する必要があります**NULL**します。

-   使用**FsRtlSetupAdvancedHeaderEx** (の代わりに[ **FsRtlSetupAdvancedHeader**](https://msdn.microsoft.com/library/windows/hardware/ff547257))、に有効なポインターを渡すストリームコンテキスト構造を初期化するために**FileContextSupportPointer** (ファイル コンテキストの対応する構造体に埋め込まれた) のメンバー、 *FileContextSupportPointer*パラメーター。 詳細については、次を参照してください。 **FsRtlSetupAdvancedHeaderEx**と[ **FSRTL\_詳細\_FCB\_ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff547334)します。

-   呼び出す**FsRtlTeardownPerFileContexts**をファイル システムがファイルのファイル コンテキスト構造を削除するときにファイルを使用してフィルターとミニフィルター ドライバーが関連付けられているすべてのファイル コンテキスト構造体を解放します。

 

 




