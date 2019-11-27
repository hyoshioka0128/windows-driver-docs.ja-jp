---
title: ファイル システムによるコンテキストのサポート
description: ファイル システムによるコンテキストのサポート
ms.assetid: 661ee3ff-3171-4d1e-a8fe-8d1852c5e990
keywords:
- コンテキスト WDK ファイルシステムミニフィルター、ファイルシステムサポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a56fbea6b53554df45492f12b0cdfd29c802484
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841398"
---
# <a name="file-system-support-for-contexts"></a>ファイル システムによるコンテキストのサポート

ファイルコンテキスト (該当する場合)、ストリームコンテキスト、およびファイルオブジェクト (ストリームハンドル) のコンテキストをサポートするには、ファイルシステムで[**FSRTL\_ADVANCED\_FCB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)構造体を使用する必要があります。 すべての Microsoft Windows ファイルシステムはこの構造を使用します。また、すべてのサードパーティのファイルシステム開発者にもこのような構成を行うことを強くお勧めします。 詳細については、「 [**Fsrtlsetupadvanced ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff547257) 」と「 **FSRTL\_ADVANCED\_FCB\_ヘッダー**」を参照してください。

NTFS および FAT ファイルシステムは、ページングファイル、作成前または終了パス、または[**IRP\_MJ\_ネットワーク\_クエリ\_オープン**](https://docs.microsoft.com/windows-hardware/drivers/ifs/flt-parameters-for-irp-mj-network-query-open)操作のために、ファイル、ストリーム、またはファイルオブジェクトコンテキストをサポートしていません。

ミニフィルタードライバーは、 [**Fltsupportsstreamcontexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamcontexts)と[**Fltsupportsstreamhandlテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsstreamhandlecontexts)をそれぞれ呼び出して、ファイルシステムが特定のファイルオブジェクトのストリームコンテキストとファイルオブジェクトコンテキストをサポートするかどうかを判断できます。

ファイルコンテキストは、Windows Vista 以降で使用できます。

ファイルごとに1つのデータストリームのみをサポートするファイルシステム (FAT など) の場合、ファイルコンテキストはストリームコンテキストに相当します。 通常、このようなファイルシステムではストリームコンテキストはサポートされていますが、ファイルコンテキストはサポートしていません。 代わりに、フィルターマネージャーは、ファイルシステムのストリームコンテキストの既存のサポートを使用して、このサポートを提供します。 これらのファイルシステムに接続されているミニフィルタードライバーのインスタンスの場合、 [**Fltsupportsfilecontexts**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsfilecontexts)は**FALSE**を返しますが、は**TRUE**を返します (*インスタンス*パラメーターに有効な**NULL**以外の値が渡された場合)。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsupportsfilecontextsex)

ファイルでコンテキストの種類がサポートされていない場合、ミニフィルターでそのファイルにその種類のコンテキストをアタッチすることはできません。

ファイルのコンテキストをサポートするには、ファイルシステムで次のことを行う必要があります。

* ファイルコンテキスト構造 (通常はファイルコンテキストブロック (FCB)) に PVOID 型の**FileContextSupportPointer**メンバーを埋め込みます。 ファイルシステムは、このメンバーを**NULL**に初期化する必要があります。

* Fsrtlsetupの**Headerex** ( [**fsrtlsetupadvanced ヘッダー**](https://msdn.microsoft.com/library/windows/hardware/ff547257)ではなく) を使用して、ストリームコンテキスト構造を初期化し、 **FileContextSupportPointer**メンバーへの有効なポインターを渡します (対応するファイルコンテキストに埋め込まれています)。*FileContextSupportPointer*パラメーターの構造体)。 詳細については、「 **FsrtlsetupFSRTL Headerex**と[ **\_ADVANCED\_FCB\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsrtl_advanced_fcb_header)」を参照してください。

* **FsRtlTeardownPerFileContexts**を呼び出して、ファイルシステムによってファイルのファイルコンテキスト構造が削除されたときにフィルター処理およびミニフィルタを適用するすべてのファイルコンテキスト構造を解放します。