---
title: ファイル システム フィルター ドライバーのメモリ マップ ファイル
description: ファイル システム フィルター ドライバーのメモリ マップ ファイル
ms.assetid: 0915167a-f8ac-4222-bece-76d7fc8a3823
keywords:
- セキュリティの WDK ファイル システム、メモリ マップト ファイル
- メモリ マップト ファイル WDK ファイル システム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce168853bb0b10046a1e97bc5f65118582e41d8a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384312"
---
# <a name="memory-mapped-files-in-a-file-system-filter-driver"></a>ファイル システム フィルター ドライバーのメモリ マップ ファイル


## <span id="ddk_memory_mapped_files_in_a_file_system_filter_driver_if"></span><span id="DDK_MEMORY_MAPPED_FILES_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


ファイル システム フィルター ドライバー ファイルが読み取りを介してではなく、ファイルの仮想メモリ マッピングを使用してアクセスできるし、書き込みパスのファクトの理解している必要があります。 ファイル内の変更を監視するファイル システム フィルター ドライバーには、このようなファイルへの変更が不足します。 一般にメモリ マップ I/O を処理する必要があるファイル システム フィルター ドライバーをページング I/O のフィルターを適用する必要があります。 これに対処するための手法は、Windows ファイル システムの開発者の一覧で説明[(NTFSD)](http://www.osronline.com/cf.cfm?PageURL=showlists.cfm?list=NTFSD)ニュースグループ OSR によってホストされています。

 

 




