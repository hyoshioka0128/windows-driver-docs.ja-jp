---
title: ドライバーでのファイルの使用
description: ドライバーでのファイルの使用
ms.assetid: 721bf336-1d1d-4677-843d-8af04c6f434d
keywords:
- ファイル WDK カーネル
- ファイルオブジェクト WDK カーネル
- オブジェクト WDK ファイルオブジェクト
- ファイルが WDK カーネルを処理する
- WDK カーネルファイルへのハンドル
- 読み取り (ファイルからデータを)
- ファイルへのデータの書き込み
- ファイルのメタデータを読み取っています
- ファイルのメタデータを書き込んでいます
- ドライバーファイルオブジェクト WDK カーネル
- 複数ファイルオブジェクト WDK カーネル
- カーネルモードドライバー WDK、ファイル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7416b6674bf475763624eb45bfba89073fd704
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838357"
---
# <a name="using-files-in-a-driver"></a>ドライバーでのファイルの使用





Microsoft Windows executive は、オブジェクトマネージャーによって管理される executive オブジェクトである*ファイルオブジェクト*ごとのファイルを表します。 (ディレクトリはファイルオブジェクトによっても表されます)。

カーネルモードコンポーネントでは、オブジェクト名を使用してファイルを参照します。これは、ファイルの完全なパスに連結された **\\DosDevices**です。 (Microsoft Windows 2000 およびそれ以降のバージョンのオペレーティングシステムでは、 **\\** しますか? は **\\DosDevices**と同じです)。たとえば、C:\\WINDOWS\\example .txt ファイルのオブジェクト名は **\\DosDevices\\C:\\WINDOWS\\example .txt のよう**になります。 ファイルへのハンドルを開くには、オブジェクト名を使用します。 オブジェクト名の詳細については、「[オブジェクト名](object-names.md)」を参照してください。

### <a name="to-use-a-file"></a>ファイルを使用するには

1.  ファイルへのハンドルを開きます。

    詳細については、「[ファイルへのハンドルのオープン](opening-a-handle-to-a-file.md)」を参照してください。

2.  適切な**Zw*Xxx*ファイル**ルーチンを呼び出して、目的の操作を実行します。

    詳細については、「[ファイルハンドルの使用](using-a-file-handle.md)」を参照してください。

3.  [**Zwclose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)を呼び出してハンドルを閉じます。

ファイルへのハンドルを開くたびに、Windows executive によってファイルを表すファイルオブジェクトが作成され、そのオブジェクトへの開いているハンドルが返されます。 そのため、1つのファイルに対して複数のファイルオブジェクトを存在できます。 (ユーザーモードアプリケーションではハンドルをコピーできるため、同じファイルオブジェクトに対して複数のハンドルが存在する場合もあります)。ファイルオブジェクトに対して開いているハンドルがすべて閉じられると、Windows executive はファイルオブジェクトを削除します。

 

 




